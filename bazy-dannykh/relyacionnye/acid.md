---
order: 0.5
title: ACID
---

Атомарность - это свойсво транзакций, либо у нас выполняется транзакция либо не выполняется

Согласованность - после выполенения транзакции база данных остается в корректном состоянии, выполняются все ограничения и условия.

Изоляция - выполняются изоляция данных при разных уровнях изоляции

1. Read comitted - исключает грязное чтение например

**Сессия 1:**

```
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE owner = 'Иванов';
-- не делаем COMMIT
```

**Сессия 2 (если бы уровень был READ UNCOMMITTED):**

```
SELECT balance FROM accounts WHERE owner = 'Иванов';
-- видит уже уменьшенный баланс, хотя изменения ещё не зафиксированы
```

2. Non-repeatable Read - исключает *неповторяющееся чтение*.

**Сессия 1:**

```
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
BEGIN;
SELECT balance FROM accounts WHERE owner = 'Иванов';  -- видим 1000
```

**Сессия 2:**

```
UPDATE accounts SET balance = 1200 WHERE owner = 'Иванов';
COMMIT;
```

**Сессия 1:**

```
SELECT balance FROM accounts WHERE owner = 'Иванов';  -- теперь видим 1200
COMMIT;
```

➡️ Два чтения в одной транзакции дали **разные результаты**.\
Это и есть *неповторяющееся чтение*.

На уровне `REPEATABLE READ` PostgreSQL защищает от этого -- ты всегда видишь один и тот же snapshot.



seriazable read - уровень изоляции когда одновременно две транзакции работают с одними и теми же данными, и одна откатится потому что данные уже не актуальны. Исключает фантомные вставки.

Сессия 1

```
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN;

-- Считаем сумму заказов дороже 1000
SELECT SUM(amount) FROM orders WHERE amount > 1000;
-- результат = 1500 + 1200 = 2700
```

(оставь транзакцию открытой -- **не делай COMMIT**)

---

### Сессия 2

```
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN;

-- Добавляем новый заказ, который попадёт под то же условие
INSERT INTO orders (customer, amount) VALUES ('Новый клиент', 2000);
COMMIT;
```

---

### Вернись в Сессию 1

```
-- Снова считаем сумму заказов дороже 1000
SELECT SUM(amount) FROM orders WHERE amount > 1000;
COMMIT;
```

---

## Ожидаемый результат

В Сессии 1 ты **можешь получить ошибку:**

```
ERROR: could not serialize access due to concurrent update
```