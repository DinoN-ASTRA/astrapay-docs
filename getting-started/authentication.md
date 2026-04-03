# Authentication

All API requests require an API key passed in the `X-Api-Key` header.

```http
X-Api-Key: ap_live_your_api_key_here
```

---

## Generating API keys

1. Log in to the [AstraPay Dashboard](https://pay.byastra.ai)
2. Go to **Settings → API Keys**
3. Click **Create API Key**
4. Select scopes and choose Test or Live mode
5. Copy the key immediately — it is only shown once

---

## Key prefixes

| Prefix | Environment |
|--------|-------------|
| `ap_live_` | Production — processes real payments |
| `ap_test_` | Test mode — payments auto-complete, no blockchain |

---

## Scopes

Each key has one or more scopes that control which endpoints it can access.

| Scope | Endpoints | Description |
|-------|-----------|-------------|
| `payments:create` | `POST /payments`, `POST /payments/:id/cancel` | Create and cancel payments |
| `payments:read` | `GET /payments`, `GET /payments/:id` | Read payment data |
| `products:manage` | All `/products` endpoints | Full CRUD on products |
| `webhooks:manage` | All `/webhooks` endpoints | Full CRUD on webhooks |

{% hint style="warning" %}
The account associated with the API key must be **activated** and have a **merchant profile** set up. Requests from banned or incomplete accounts return `401`.
{% endhint %}
