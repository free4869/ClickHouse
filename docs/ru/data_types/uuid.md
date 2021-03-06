# UUID {#uuid-data-type}

Универсальный уникальный идентификатор (UUID) - это 16-байтовое число, используемое для идентификации записей. Подробнее про UUID читайте на [Википедии](https://en.wikipedia.org/wiki/Universally_unique_identifier).

Пример UUID значения представлен ниже:

```text
61f0c404-5cb3-11e7-907b-a6006ad3dba0
```

Если при вставке новой записи значение для UUID-колонки не указано, UUID идентификатор будет заполнен нулями:

```text
00000000-0000-0000-0000-000000000000
```

## Как сгенерировать UUID

Для генерации UUID-значений предназначена функция [generateUUIDv4](../query_language/functions/uuid_functions.md).

## Примеры использования

Ниже представлены примеры работы с UUID.

**Пример 1**

Этот пример демонстрирует, как создать таблицу с UUID-колонкой и добавить в нее сгенерированный UUID.

```sql
CREATE TABLE t_uuid (x UUID, y String) ENGINE=TinyLog
```
```sql
INSERT INTO t_uuid SELECT generateUUIDv4(), 'Example 1'
```
```sql
SELECT * FROM t_uuid
```
```text
┌────────────────────────────────────x─┬─y─────────┐
│ 417ddc5d-e556-4d27-95dd-a34d84e46a50 │ Example 1 │
└──────────────────────────────────────┴───────────┘
```

**Пример 2**

В этом примере, при добавлении записи в таблицу значение для UUID-колонки не задано. UUID будет заполнен нулями.

```sql
INSERT INTO t_uuid (y) VALUES ('Example 2')
```
```sql
SELECT * FROM t_uuid
```
```text
┌────────────────────────────────────x─┬─y─────────┐
│ 417ddc5d-e556-4d27-95dd-a34d84e46a50 │ Example 1 │
│ 00000000-0000-0000-0000-000000000000 │ Example 2 │
└──────────────────────────────────────┴───────────┘
```

## Ограничения

Тип данных UUID можно использовать только с функциями, которые поддерживаются типом данных [String](string.md) (например, [min](../query_language/agg_functions/reference.md#agg_function-min), [max](../query_language/agg_functions/reference.md#agg_function-max), и [count](../query_language/agg_functions/reference.md#agg_function-count)).

Тип данных UUID не поддерживается арифметическими операциями  (например, [abs](../query_language/functions/arithmetic_functions.md#arithm_func-abs)) или агрегатными функциями, такими как [sum](../query_language/agg_functions/reference.md#agg_function-sum) и [avg](../query_language/agg_functions/reference.md#agg_function-avg).

[Original article](https://clickhouse.yandex/docs/en/data_types/uuid/) <!--hide-->

