# List Webhooks

```
GET /v1/api/webhooks
```

**Required scope:** `webhooks:manage`

---

## Example

```bash
curl https://apipay.byastra.ai/v1/api/webhooks \
  -H "X-Api-Key: ap_live_your_api_key"
```

## Response `200 OK`

```json
{
  "success": true,
  "data": [
    {
      "id": "c3d4e5f6-a7b8-9012-cdef-345678901234",
      "url": "https://yourapp.com/webhooks/astrapay",
      "events": ["payment.completed", "payment.canceled"],
      "active": true,
      "created_at": "2026-03-31T12:00:00.000Z"
    }
  ]
}
```

> The `secret` is never included in list or get responses.
