
# Задание: CashBox API — Вечерний клиринг банкомата

## Цель
Проверить навыки системного аналитика по части:
- чтения и уточнения API-спецификаций,
- проектирования бизнес-процессов (BPMN),
- построения взаимодействия систем (UML),
- базового моделирования БД (ER / SQL),
- документирования нефункциональных требований (NFR).

---

## Что нужно сделать

1. Ознакомьтесь с OpenAPI-спецификацией `cashbox.yaml`, в которой описан REST-эндпойнт `/cash/transactions`.

2. Сформулируйте **3–5 уточняющих вопросов** по API и процессу.
   Затем предложите **свои предположения и ответы** на них.

3. Нарисуйте **BPMN-диаграмму** бизнес-процесса:
   - Закрытие смены банкомата
   - Подсчёт остатка
   - Сверка с НГЛ
   - Генерация проводок
   - Завершение дня

4. Постройте **UML Sequence Diagram** взаимодействия:
   `ATM → CashBox → New General Ledger (NGL)`

5. Опишите **ER-модель** базы данных CashBox:
   - Таблицы `cash_operations`, `atm_balances`
   - Ключи, индексы, внешние ключи

6. Подготовьте документ **NFR.md**, включающий:
   - Время отклика REST API (`latency`) ≤ 200 мс
   - Пропускная способность Kafka (`throughput`) ≥ 200 msg/s
   - Retry-policy: 3 попытки, затем DLQ
   - Хранение данных ≥ 365 дней

7. 🏅 **Бонус (необязательно)**:
   https://github.com/kobzevvv/CashBox-API-homework/blob/main/2-Bonus-Task-mock-api-server/ru.md
   


---

## Что прислать на выходе

| Артефакт | Формат |
|----------|--------|
| `cashbox.yaml` | OpenAPI YAML |
| `evening_clearing.bpmn` | BPMN 2.0 |
| `sequence.png` | UML Sequence Diagram |
| `schema.sql` | SQL (DDL) |
| `NFR.md` | Markdown |
| `assumptions.md` | Уточнения и ваши ответы |
| `mock-server/` | *(необязательно)* mock-сервер / экспорт Mockoon

---

## Полезные ресурсы

- [Mockoon](https://mockoon.com/) — mock API сервер
- [Swagger Editor](https://editor.swagger.io/) — OpenAPI редактор
- [Camunda Modeler](https://camunda.com/download/modeler/) — редактор BPMN 2.0
- [draw.io (diagrams.net)](https://app.diagrams.net/) — UML, BPMN, ER
- [Kafka retry mechanisms](https://www.confluent.io/blog/kafka-error-handling/) — Dead-letter queue и backoff

---

## Логика API

POST `/cash/transactions` — фиксирует операцию в банкомате.  
Пример тела запроса:

```json
{
  "atmId": "ATM-MSK-001",
  "type": "CASH_IN",
  "amount": 5000.00,
  "currency": "RUB",
  "ts": "2025-07-21T15:30:00Z"
}
```

После регистрации операция публикуется в Kafka-топик `cash.tx.accepted.v1`.

