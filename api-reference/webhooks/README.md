# Webhooks

Webhooks notify your server in real time when payment events occur. AstraPay sends a `POST` request with a signed JSON payload to your registered URL.

---

## Webhook object

```json
{
  "id": "c3d4e5f6-a7b8-9012-cdef-345678901234",
  "url": "https://yourapp.com/webhooks/astrapay",
  "events": ["payment.completed", "payment.canceled"],
  "active": true,
  "created_at": "2026-03-31T12:00:00.000Z",
  "updated_at": "2026-03-31T12:00:00.000Z"
}
```

{% hint style="warning" %}
The webhook `secret` is only returned once — when the webhook is created. Store it securely. It is never returned in list or get responses.
{% endhint %}

---

## Event types

| Event | Description |
|-------|-------------|
| `payment.completed` | Payment received and confirmed on-chain |
| `payment.expired` | Payment expired without being completed |
| `payment.canceled` | Payment was canceled via API or dashboard |
| `payment.partially_paid` | Partial payment received (less than full amount) |

---

## Delivery & retries

| Setting | Value |
|---------|-------|
| Max attempts | 3 (1 initial + 2 retries) |
| Retry backoff | Exponential — 5s, 30s, 120s |
| Timeout | 10 seconds per attempt |
| Success | Any `2xx` response |
