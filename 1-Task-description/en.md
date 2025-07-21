
# Assignment: CashBox API — ATM Evening Clearing

## Goal
Evaluate the candidate’s ability to:
- read and clarify API specifications,
- design business processes using BPMN,
- model system interactions (UML),
- create basic DB models (ER / SQL),
- define non-functional requirements (NFR).

---

## Task Description

1. Review the OpenAPI specification in `cashbox.yaml`, which describes the `/cash/transactions` endpoint.

2. Formulate **3–5 clarifying questions** about the API and process.
   Then, provide **your own assumptions and answers** to those questions.

3. Create a **BPMN diagram** for the business process:
   - Closing the ATM shift
   - Counting cash
   - Reconciling with the New General Ledger (NGL)
   - Generating entries
   - Finishing the day

4. Build a **UML Sequence Diagram** showing the interaction between:
   `ATM → CashBox → New General Ledger (NGL)`

5. Propose an **ER model** for the CashBox database:
   - Tables: `cash_operations`, `atm_balances`
   - Keys, indexes, foreign keys

6. Write an **NFR.md** document with:
   - REST API latency ≤ 200 ms
   - Kafka throughput ≥ 200 messages/sec
   - Retry policy: 3 retries, then move to DLQ (Dead Letter Queue)
   - Data retention ≥ 365 days

7. 🏅 **Bonus (optional)**:
   - Set up a mock server based on `cashbox.yaml` using [Mockoon](https://mockoon.com/) or another tool.
   - Provide a link or setup instructions (`README` / `docker-compose`).

---

## Expected Deliverables

| Artifact | Format |
|----------|--------|
| `cashbox.yaml` | OpenAPI YAML |
| `evening_clearing.bpmn` | BPMN 2.0 |
| `sequence.png` | UML Sequence Diagram |
| `schema.sql` | SQL (DDL) |
| `NFR.md` | Markdown |
| `assumptions.md` | Your clarifications & assumptions |
| `mock-server/` | *(optional)* mock server config or Mockoon export

---

## Useful Resources

- [Mockoon](https://mockoon.com/) — Local REST API mocking
- [Swagger Editor](https://editor.swagger.io/) — OpenAPI editing in browser
- [Camunda Modeler](https://camunda.com/download/modeler/) — BPMN 2.0 editor
- [draw.io (diagrams.net)](https://app.diagrams.net/) — UML, BPMN, ER diagrams
- [Kafka retry mechanisms](https://www.confluent.io/blog/kafka-error-handling/) — DLQ and backoff strategies

---

## API Overview

POST `/cash/transactions` — registers a cash operation from an ATM.  
Example request body:

```json
{
  "atmId": "ATM-MSK-001",
  "type": "CASH_IN",
  "amount": 5000.00,
  "currency": "RUB",
  "ts": "2025-07-21T15:30:00Z"
}
```

Upon success, the transaction is published to Kafka topic `cash.tx.accepted.v1`.
