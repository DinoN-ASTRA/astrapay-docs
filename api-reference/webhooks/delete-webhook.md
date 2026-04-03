# Delete Webhook

```
DELETE /v1/api/webhooks/:id
```

**Required scope:** `webhooks:manage`

---

## Example

```bash
curl -X DELETE https://apipay.byastra.ai/v1/api/webhooks/c3d4e5f6-a7b8-9012-cdef-345678901234 \
  -H "X-Api-Key: ap_live_your_api_key"
```

## Response `200 OK`

```json
{ "success": true, "data": { "deleted": true } }
```
