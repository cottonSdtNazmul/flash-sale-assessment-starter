# Senior Backend Take-Home Assessment: Flash Sale API

Welcome! This task evaluates architectural decision-making, concurrency control, and backend reliability under high load.

---

## 🎯 The Challenge
You are building the core backend service for a high-concurrency **Flash Sale System**. 

The database contains an item with **10 units in stock**. During the flash sale, **50+ concurrent requests** will hit the server at the exact same millisecond trying to reserve/buy the remaining stock.

### Your Objectives
1. **Implement `GET /items/{id}`**: Returns the current stock status.
2. **Implement `POST /items/{id}/buy`**: Accepts `{"user_id": "string"}` and processes the order.
3. **Prevent Overselling**: Ensure stock **never goes below 0** and total created orders **never exceed stock**.
4. **Prevent Double Purchase**: A single user should only be allowed to purchase the item once.
5. **Concurrency Test**: Write an automated integration/unit test (or use `test_concurrency.py`) demonstrating concurrent safety.

---

## 🛠️ Requirements & Constraints
* **Timebox:** Estimated **3–4 hours**. Please do **not** spend more than 5 hours.
* **Stack:** Use your preferred language/framework (Node.js/TypeScript, Python, Go, Laravel, etc.).
* **Database:** PostgreSQL & Redis are available via Docker. You can use DB locks, transactions, or Redis atomic operations.
* **Code Structure:** Organize your code into clean layers (Controller, Service, Repository/DB).

---

## 🚀 Getting Started

1. **Start Environment Services:**
   ```bash
   docker compose up -d
   ```
   * PostgreSQL runs on `localhost:5432` (User: `dev_user`, Pass: `dev_password`, DB: `flash_sale`)
   * Redis runs on `localhost:6379`

2. **Verify Database:**
   The initial item (`id = 1`) with `available_stock = 10` is pre-seeded in the database.

3. **Build & Run Your Application** on your chosen framework.

4. **Verify Concurrency Handling:**
   Run the load testing script to test race conditions against your endpoint:
   ```bash
   python3 test_concurrency.py
   ```

---

## 📋 Submission Guidelines
1. Push your code to a private GitHub repository and invite us, or submit a ZIP file.
2. Include a **`SUBMISSION.md`** file answering:
   * **Concurrency Strategy:** How did you handle race conditions and prevent double-selling?
   * **Trade-offs & Alternatives:** What alternative approaches did you consider and why did you pick this one?
   * **Production Readiness:** What would you add if this were deploying to production for 100,000 requests/sec?
