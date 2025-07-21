
## 2. Bonus Task — Mock API Server

### Goal
Simulate a working version of the CashBox API based on the provided `cashbox.yaml` specification.  
This task is optional but highly recommended, as it demonstrates your ability to bridge documentation and implementation.

### Why it’s useful

Creating a mock server helps in multiple real-world scenarios:

- ✅ **Engineers** can start developing and testing against your API contract even before backend is ready.
- 🧪 **QA teams** can use it to test client behavior with predictable responses.
- 🧠 **Product managers and stakeholders** can interact with the future system early via tools like Postman.
- 📐 **You**, as a system analyst, validate your own API design for completeness and realism.

> In a real project, API mocks improve team velocity and communication between frontend/backend, analysts, and QA.

---

### What to do

- Use [Mockoon](https://mockoon.com/) (or any other tool) to create a mock server based on `cashbox.yaml`.
- The mock server should support at least the endpoint `POST /cash/transactions`.
- Provide one or more predictable responses (e.g. 201 Created and 400 Bad Request).
- Submit either:
  - A link to the exported mock configuration file (e.g. `cashbox_mockoon.json`), **or**
  - Setup instructions in `README.md` (or `docker-compose.yml`) so the mock server can be launched locally.

---

### Resources

- [Mockoon Getting Started](https://mockoon.com/docs/latest/getting-started/)
- [How to use OpenAPI with Mockoon](https://mockoon.com/docs/latest/openapi/)
- [Postman Mock Servers](https://learning.postman.com/docs/designing-and-developing-your-api/mocking-data/)

