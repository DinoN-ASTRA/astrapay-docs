# Get Webhook

```
GET /v1/api/webhooks/:id
```

**Required scope:** `webhooks:manage`

---

## Path parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | `string` | Webhook UUID |

---

## Example

```bash
curl https://apipay.byastra.ai/v1/api/webhooks/c3d4e5f6-a7b8-9012-cdef-345678901234 \
  -H "X-Api-Key: ap_live_your_api_key"
```

Response is the same shape as [List Webhooks](./list-webhooks.md) (single object, no `secret`).
