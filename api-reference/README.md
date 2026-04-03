# API Reference

**Base URL:** `https://apipay.byastra.ai/v1/api`

All requests require an `X-Api-Key` header. All request and response bodies are JSON.

---

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/payments` | Create a payment |
| `GET` | `/payments/:id` | Get a payment |
| `GET` | `/payments` | List payments |
| `POST` | `/payments/:id/cancel` | Cancel a payment |
| `POST` | `/products` | Create a product |
| `GET` | `/products` | List products |
| `GET` | `/products/:id` | Get a product |
| `PATCH` | `/products/:id` | Update a product |
| `DELETE` | `/products/:id` | Delete a product |
| `POST` | `/webhooks` | Create a webhook |
| `GET` | `/webhooks` | List webhooks |
| `GET` | `/webhooks/:id` | Get a webhook |
| `PATCH` | `/webhooks/:id` | Update a webhook |
| `DELETE` | `/webhooks/:id` | Delete a webhook |
