---
editable: false
---

# ALL_CONCAT

_Агрегатные функции_

#### Синтаксис {#syntax}


```
ALL_CONCAT( expression [ , separator ] )
```

#### Описание {#description}
Возвращает строку, которая содержит все попавшие в группу значения `expression`, с разделителем `separator` (по умолчанию разделитель — запятая).

**Типы аргументов:**
- `expression` — `Любой`
- `separator` — `Строка`


**Возвращаемый тип**: `Строка`

{% note info %}

Значения аргументов (`separator`) должны быть константами.

{% endnote %}


#### Примеры {#examples}

```
ALL_CONCAT([Profit])
```

```
ALL_CONCAT([Profit], '; ')
```


#### Поддержка источников данных {#data-source-support}

`Материализованный датасет`, `ClickHouse 1.1`, `PostgreSQL 9.3`.
