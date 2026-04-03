# List Products

Returns all products for the authenticated merchant.

```
GET /v1/api/products
```

**Required scope:** `products:manage`

---

## Example

```bash
curl https://apipay.byastra.ai/v1/api/products \
  -H "X-Api-Key: ap_live_your_api_key"
```

## Response `200 OK`

```json
{
  "success": true,
  "statusCode": 200,
  "data": [
    {
      "id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
      "name": "Pro Plan",
      "price": 49.00,
      "currency_type": "FIAT",
      "active": true,
      "share_link": "https://pay.byastra.ai/products/b2c3d4e5",
      "created_at": "2026-03-31T12:00:00.000Z"
    }
  ]
}
```
