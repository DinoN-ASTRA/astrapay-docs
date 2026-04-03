# Create Webhook

```
POST /v1/api/webhooks
```

**Required scope:** `webhooks:manage`

---

## Request body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | `string` | Yes | HTTPS endpoint to receive webhook events |
| `events` | `string[]` | Yes | Event types to subscribe to (at least one required) |

---

## Example

```bash
curl -X POST https://apipay.byastra.ai/v1/api/webhooks \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://yourapp.com/webhooks/astrapay",
    "events": ["payment.completed", "payment.canceled"]
  }'
```

## Response `201 Created`

```json
{
  "success": true,
  "statusCode": 201,
  "data": {
    "id": "c3d4e5f6-a7b8-9012-cdef-345678901234",
    "url": "https://yourapp.com/webhooks/astrapay",
    "events": ["payment.completed", "payment.canceled"],
    "active": true,
    "secret": "whsec_a1b2c3d4e5f6...",
    "created_at": "2026-03-31T12:00:00.000Z"
  }
}
```

{% hint style="danger" %}
Store the `secret` immediately — it is only returned at creation and cannot be retrieved again. Use it to [verify webhook signatures](./signature-verification.md).
{% endhint %}
