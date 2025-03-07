# Управление эндпоинтом для приемника

[Эндпоинт](../concepts/index.md#endpoint) для приемника описывает настройки базы данных, в которую будет перенесена информация с помощью {{ data-transfer-name }}. Вы можете [создать](#create), [изменить](#update) или [удалить](#delete) такой эндпоинт.

## Создать эндпоинт для приемника {#create}

{% list tabs %}

* Консоль управления

    1. Перейдите на страницу каталога и выберите сервис **{{ data-transfer-name}}**.
    1. На вкладке **Эндпоинты** нажмите кнопку **Создать эндпоинт**.
    1. В поле **Направление** выберите `Приемник`.
    1. Укажите имя эндпоинта. Используйте строчные латинские буквы и цифры.
    1. (Опционально) Укажите описание эндпоинта.
    1. В поле **Тип базы данных** выберите тип приемника, в который вы хотите передавать данные.
    1. Задайте параметры эндпоинта:

        * [{#T}](#settings-clickhouse);
        * [{#T}](#settings-mongodb);
        * [{#T}](#settings-mysql);
        * [{#T}](#settings-storage);
        * [{#T}](#settings-postgresql);
        * [{#T}](#settings-yandex-database).

    1. Нажмите кнопку **Создать**.

{% endlist %}

## Изменить эндпоинт для приемника {#update}

{% list tabs %}

* Консоль управления

    1. Перейдите на страницу каталога и выберите сервис **{{ data-transfer-name }}**.
    1. На вкладке **Эндпоинты** выберите эндпоинт и нажмите кнопку ![pencil](../../_assets/pencil.svg) **Редактировать** на панели сверху.
    1. Отредактируйте параметры эндпоинта:

        * [{#T}](#settings-clickhouse);
        * [{#T}](#settings-mongodb);
        * [{#T}](#settings-mysql);
        * [{#T}](#settings-storage);
        * [{#T}](#settings-postgresql);
        * [{#T}](#settings-yandex-database).

    1. Нажмите кнопку **Применить**.

{% endlist %}

## Удалить эндпоинт для приемника {#delete}

{% include [delete-endpoint](../../_includes/data-transfer/delete-endpoint.md) %}

## Параметры эндпоинта для приемника {#settings}

### {{ CH }} {#settings-clickhouse}

* **Тип подключения** — выбор типа подключения к БД:

    {% include [ClickHouse required settings](../../_includes/data-transfer/necessary-settings/clickhouse.md) %}

* Дополнительные настройки:

    * **Имя кластера ClickHouse** — укажите имя кластера, в который будут передаваться данные.
    * **Переопределение имен таблиц** — заполните, если необходимо переименовать таблицы источника при переносе в базу-приемник.
    * **Колонка шардирования** — имя колонки в таблицах, по которой следует [шардировать](../../managed-clickhouse/concepts/sharding.md) данные.
    * **Шардирование по идентификатору трансфера** — данные по шардам будут распределяться на основе значения идентификатора трансфера.

        {% note warning %}

        Если одновременно включены настройки **Колонка шардирования** и **Шардирование по идентификатору трансфера**, то шардирование будет осуществляться только по идентификатору трансфера.

        {% endnote %}

    * **Мапинг шардов** — если используется шардирование по колонке, настройте распределение значений по шардам кластера-приемника.

    * **Загружать данные в JSON формате** — для необязательных полей будут использованы значения по умолчанию, если они определены. Включите эту настройку, если трансфер будет подключаться к приемнику через HTTP-порт, а не нативный.

    * **Интервал записи** — укажите задержку, с которой данные должны поступать в кластер-приемник. Увеличьте значение в этом поле, если {{ CH }} не успевает делать слияние кусков данных.
    * {% include [Field Cleanup policy](../../_includes/data-transfer/fields/cleanup-policy-disabled-drop.md) %}

### {{ MG }} {#settings-mongodb}

* **Настройки подключения** — выбор типа подключения к БД:

    {% include [Required MongoDB settings](../../_includes/data-transfer/necessary-settings/mongodb.md) %}

* Дополнительные настройки:
    
        
    * {% include [Field Subnet ID](../../_includes/data-transfer/fields/subnet-id.md) %}
    
    * **Сертификат CA** — для шифрования передаваемых данных загрузите файл [PEM-сертификата](../../managed-mongodb/operations/connect.md#get-ssl-cert) или добавьте его содержимое в текстовом виде.
    * {% include [Field Cleanup policy](../../_includes/data-transfer/fields/cleanup-policy-disabled-drop-truncate.md) %}

### {{ MY }} {#settings-mysql}

* **Настройки подключения** — выбор типа подключения к БД:

    {% include [Required MySQL settings](../../_includes/data-transfer/necessary-settings/mysql.md) %}

* Дополнительные настройки:

    * **Режим sql_mod** — укажите настройки, переопределяющие [стандартное поведение {{ MY }}](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html).

    * **Отключение проверки констрейтов** — используется для ускорения репликации: настройки `FOREIGN_KEY_CHECKS` и `UNIQUE_CHECKS` устанавливаются в значение `0` (проверки не производятся).

        {% note warning %}

        Отключение проверки констрейтов ускорит репликацию, но может привести к нарушению целостности данных при использовании каскадных операций.

        {% endnote %}

    * {% include [Field Timezone](../../_includes/data-transfer/fields/timezone.md) %}

    * {% include [Field Cleanup policy](../../_includes/data-transfer/fields/cleanup-policy-disabled-drop-truncate.md) %}

### {{ objstorage-name }} {#settings-storage}


* **Бакет** — имя [бакета](../../storage/concepts/bucket.md), в который будут загружаться данные из источника.

* **SA Аккаунт** — [сервисный аккаунт](../../iam/concepts/users/service-accounts.md) с ролью `storage.uploader`, под которым будет осуществляться доступ к [{{ yds-full-name }}](../../data-streams).

* **Выходной формат** — формат, в котором данные будут записаны в бакет, `JSON` или `CSV`.

* **Паттерн раскладки данных** — путь к каталогу в бакете, в который будут сохранены данные.

* **Размер файла** — разделение данных на файлы указанного размера.

* **Интервал отправки** — интервал отправки данных в бакет, в секундах.

* **Формат сжатия** — сжатие выходных данных, `GZIP` или `UNCOMPRESSED` (отключено).

### {{ PG }} {#settings-postgresql}

* **Настройки подключения** — выбор типа подключения к БД:

{% include [PostgreSQL required settings](../../_includes/data-transfer/necessary-settings/postgresql.md) %}

* Дополнительные настройки:
    
        
    * **Сетевой интерфейс для эндпоинта** — выберите или [создайте](../../vpc/operations/subnet-create.md) подсеть в нужной [зоне доступности](../../overview/concepts/geo-scope.md).
    
        Если источник и приемник географически близки, подключение через выбранную подсеть ускорит работу трансфера.
    
    * {% include [Field Cleanup policy](../../_includes/data-transfer/fields/cleanup-policy-disabled-drop-truncate.md) %}

    * Сохранение границ транзакций — включите, чтобы сервис записывал данные в базу-приемник только после полного чтения данных транзакции из базы-источника.

        {% note warning %}

        Эта функциональность находится на стадии [Preview](../../overview/concepts/launch-stages.md).

        {% endnote %}

### {{ ydb-name }} {#settings-yandex-database}

Для подключения настройте обязательные параметры:

{% include [Обязательные настройки YDB](../../_includes/data-transfer/necessary-settings/ydb.md) %}

Дополнительные настройки:

* **Количество шардов для разделения трафика** — укажите нужное количество шардов `N`.

    Если настройка задана, в таблицы добавляется колонка <q>_shard_col</q>. Значения в ней вычисляются как остаток от деления `H/N`, где `H` — результат хеш-функции от текущего времени, а `N` — указанное настройкой количество шардов.

* **Ротация таблиц**:

    * **Единица измерения** — час, день или месяц.
    * **Размер таблицы** — в выбранных единицах измерения.

        По истечении временного интервала, равного выбранной единице измерения, будет удалена самая старая таблица базы и создана новая.

    * **Количество таблиц** — необходимое количество таблиц в базе-приемнике.
    * **Разбивать по колонке** — по значениям какой колонки разбивать (_партицировать_) таблицу. Колонка должна иметь тип <q>время</q>.

        
        Подробнее о партицировании таблиц см. в документации [{{ ydb-full-name }}](../../ydb/concepts/datamodel.md#partitioning)

    Если используется эта настройка, в базе-приемнике создается указанное количество таблиц для данных за различные интервалы времени. Имя каждой таблицы выбирается автоматически по дате и времени начала интервала. В зависимости от значений в указанной колонке таблицы-источника, исходные строки распределяются по соответствующим таблицам базы-приемника.

* **Переопределение имен таблиц** — заполните, если необходимо переименовать таблицы базы-источника при переносе в базу-приемник.
* **Поддиректория куда разместить таблицы** — укажите [поддиректорию](../../ydb/concepts/databases.md#directory) для размещения таблиц.

    Итоговый путь размещения таблицы: `<Путь в Yandex Database>/<Поддиректория>/<Таблица>`.

* {% include [Field Cleanup policy](../../_includes/data-transfer/fields/cleanup-policy-disabled-drop.md) %}
