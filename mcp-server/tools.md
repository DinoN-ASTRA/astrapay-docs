# MCP Server — Available Tools

13 tools across three categories.

---

## Payment tools

| Tool | Description |
|------|-------------|
| `create_payment` | Create a new crypto payment. Returns a checkout URL. Accepts `amount` or `product_id`, `token`, `network`, `customer_email`, `customer_name`, `redirect_url`, `cancel_url`, `metadata`. |
| `get_payment` | Get payment status and details by UUID or short ID. |
| `list_payments` | List payments with optional `status`, `search`, `page`, `pageSize` filters. |
| `cancel_payment` | Cancel a pending payment by ID. |

---

## Product tools

| Tool | Description |
|------|-------------|
| `create_product` | Create a product with `name`, `price`, `currency_type` (`FIAT` or `CRYPTO`), optional `token`, `network`, `description`, `active`. |
| `list_products` | List all products for the merchant. |
| `update_product` | Update a product's name, description, price, currency type, token, network, or active status. |
| `delete_product` | Delete a product by ID. |

---

## Webhook tools

| Tool | Description |
|------|-------------|
| `create_webhook` | Register a webhook URL with event subscriptions. Returns a signing secret. |
| `get_webhook` | Get webhook details by ID. |
| `list_webhooks` | List all registered webhooks. |
| `update_webhook` | Update a webhook's URL, events, or active status. |
| `delete_webhook` | Delete a webhook by ID. |

---

## Example prompts

```
"Create a $49.99 USDC payment on Base for john@example.com, redirect to https://myapp.com/success"
"Check the status of payment pXk9mQ"
"Show me all completed payments from this week"
"Cancel payment a1b2c3d4-e5f6-7890-abcd-ef1234567890"
"Create a Pro Plan product at $49 USD"
"Set up a webhook at https://myapp.com/hooks for payment.completed and payment.canceled"
"Disable my webhook c3d4e5f6-a7b8-9012-cdef-345678901234"
```
