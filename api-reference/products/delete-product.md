# Delete Product

```
DELETE /v1/api/products/:id
```

**Required scope:** `products:manage`

---

## Example

```bash
curl -X DELETE https://apipay.byastra.ai/v1/api/products/b2c3d4e5-f6a7-8901-bcde-f23456789012 \
  -H "X-Api-Key: ap_live_your_api_key"
```

## Response `200 OK`

```json
{ "success": true, "data": { "deleted": true } }
```
