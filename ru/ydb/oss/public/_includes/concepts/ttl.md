# Time to Live (TTL)

В разделе описан принцип работы TTL, его ограничения, а также приведены примеры команд и фрагменты кода, с помощью которых можно включить, настроить и выключить TTL.

## Принцип работы {#how-it-works}

{{ ydb-short-name }} позволяет указать для таблицы колонку (TTL-колонка), значения которой будут использоваться для определения времени жизни строк. TTL автоматически удаляет из таблицы строки, когда проходит указанное количество секунд от времени, записанного в TTL-колонку.

{% note warning %}

Строка с `NULL` в TTL-колонке никогда не будет удалена.

{% endnote %}

Момент времени, когда строка таблицы может быть удалена, определяется по следующей формуле:

```
expiration_time = valueof(ttl_column) + expire_after_seconds
```

{% note info %}

Не гарантируется, что удаление произойдет именно в `expiration_time` — оно может случиться позже. Если важно исключить из выборки логически устаревшие, но пока еще физически неудаленные строки, нужно использовать фильтрацию уровня запроса.

{% endnote %}

Непосредственно удалением данных занимается фоновая операция удаления — *Background Removal Operation* (*BRO*), состоящая из 2 стадий:
1. Проверка значений в TTL-колонке.
2. Удаление устаревших данных.

*BRO* обладает следующими свойствами:
* Единицей параллельности является [партиция таблицы](../../../../concepts/datamodel.md#partitioning).
* Для таблиц со [вторичными индексами](../../develop/concepts/secondary_indexes.md) стадия удаления является [распределенной транзакцией](../../develop/concepts/transactions.md#distributed-tx).

## Гарантии {#guarantees}

* В каждый момент времени *BRO* запущен не более, чем в 1 экземпляре на таблицу.
* *BRO* запускается не чаще одного раза в час для одной и той же партиции.
* Гарантируется согласованность данных. Значение в TTL-колонке повторно проверяется во время стадии удаления. Таким образом, если между стадиями 1 и 2 значение в TTL-колонке модифицируется (например, запросом `UPDATE`) и перестает соответствовать критерию удаления, такая строка не будет удалена.

## Ограничения {#restrictions}

* TTL-колонка должна быть одного из следующих типов:
  - `Date`;
  - `Datetime`;
  - `Timestamp`;
  - `Uint32`;
  - `Uint64`;
  - `DyNumber`.
* Значение TTL-колонки с числовым типом (`Uint32`, `Uint64`, `DyNumber`) интерпретируется как величина от [Unix-эпохи](https://ru.wikipedia.org/wiki/Unix-время) заданная в:
  - секундах;
  - миллисекундах;
  - микросекундах;
  - наносекундах.
* Нельзя указать несколько TTL-колонок.
* Нельзя удалить TTL-колонку. Если это все же требуется, сначала нужно [выключить TTL](#disable) на таблице.

## Настройка {#setting}

Управление настройками TTL в настоящий момент возможно с использованием:

* [YQL](../../../../yql/reference/overview.md).
* [Консольного клиента {{ ydb-short-name }}](https://cloud.yandex.ru/docs/ydb/quickstart/yql-api/ydb-cli).
* [{{ ydb-short-name }} Python SDK](https://github.com/yandex-cloud/ydb-python-sdk).

{% note info %}

Настройка TTL с использованием YQL возможна для колонок типа `Date`, `Datetime`, и `Timestamp`.

{% endnote %}

### Включение TTL для существующей таблицы {#enable-on-existent-table}

В приведенном ниже примере строки таблицы `mytable` будут удаляться спустя час после наступления времени, записанного в колонке `created_at`:

{% list tabs %}

- YQL
  ```yql
  ALTER TABLE `mytable` SET (TTL = Interval("PT1H") ON created_at);
  ```

- CLI
  ```bash
  $ {{ ydb-cli }} -e <endpoint> -d <database> table ttl set --column created_at --expire-after 3600 mytable
  ```


- Python
  ```python
  session.alter_table('mytable', set_ttl_settings=ydb.TtlSettings().with_date_type_column('created_at', 3600))
  ```

{% endlist %}

{% note tip %}

При настройке TTL с использованием YQL, `Interval` создается из строкового литерала в формате [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).

{% endnote %}

### Включение TTL для вновь создаваемой таблицы {#enable-for-new-table}

Для вновь создаваемой таблицы можно передать настройки TTL вместе с ее описанием:

{% list tabs %}

- YQL
  ```yql
  CREATE TABLE `mytable` (
      id Uint64,
      expire_at Timestamp,
      PRIMARY KEY (id)
  ) WITH (
      TTL = Interval("PT0S") ON expire_at
  );
  ```


- Python
  ```python
  session.create_table(
      'mytable',
      ydb.TableDescription()
      .with_column(ydb.Column('id', ydb.OptionalType(ydb.DataType.Uint64)))
      .with_column(ydb.Column('expire_at', ydb.OptionalType(ydb.DataType.Timestamp)))
      .with_primary_key('id')
      .with_ttl(ydb.TtlSettings().with_date_type_column('expire_at'))
  )
  ```

{% endlist %}

### Выключение TTL {#disable}

{% list tabs %}

- YQL
  ```yql
  ALTER TABLE `mytable` RESET (TTL);
  ```

- CLI
  ```bash
  $ {{ ydb-cli }} -e <endpoint> -d <database> table ttl drop mytable
  ```


- Python
  ```python
  session.alter_table('mytable', drop_ttl_settings=True)
  ```

{% endlist %}

### Получение настроек TTL {#describe}

Текущие настройки TTL можно получить из описания таблицы:

{% list tabs %}

- CLI
  ```bash
  $ {{ ydb-cli }} -e <endpoint> -d <database> scheme describe mytable
  ```


- Python
  ```python
  desc = session.describe_table('mytable')
  ttl = desc.ttl_settings
  ```

{% endlist %}

