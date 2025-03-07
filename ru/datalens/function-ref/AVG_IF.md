---
editable: false
sourcePath: ru/_api-ref/datalens/function-ref/AVG_IF.md
---


# AVG_IF

_Функция `AVG_IF` также доступна как [оконная](AVG_IF_WINDOW.md)._

#### Синтаксис {#syntax}


```
AVG_IF( expression, condition )
```

#### Описание {#description}
Возвращает среднее для всех значений, которые удовлетворяют условию `condition`. Если значения отсутствуют, то возвращается `NULL`. Работает только с числовыми типами данных.

**Типы аргументов:**
- `expression` — `Дробное число | Целое число`
- `condition` — `Логический`


**Возвращаемый тип**: `Дробное число`

#### Пример {#examples}

```
AVG_IF([Profit], [Profit] > 5)
```


#### Поддержка источников данных {#data-source-support}

`Материализованный датасет`, `ClickHouse 19.13`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`, `YDB`.
