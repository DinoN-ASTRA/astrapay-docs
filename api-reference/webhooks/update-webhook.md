# Update Webhook

```
PATCH /v1/api/webhooks/:id
```

**Required scope:** `webhooks:manage`

---

## Request body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | `string` | No | New endpoint URL |
| `events` | `string[]` | No | New event subscriptions (min 1) |
| `active` | `boolean` | No | Enable or disable the webhook |

---

## Example

```bash
curl -X PATCH https://apipay.byastra.ai/v1/api/webhooks/c3d4e5f6-a7b8-9012-cdef-345678901234 \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "events": ["payment.completed", "payment.expired", "payment.canceled", "payment.partially_paid"],
    "active": true
  }'
```

Returns the updated webhook object.
