# Update Product

Partially updates a product. Only include fields you want to change.

```
PATCH /v1/api/products/:id
```

**Required scope:** `products:manage`

---

## Request body

All fields are optional. Same types as [Create Product](./create-product.md).

---

## Example

```bash
curl -X PATCH https://apipay.byastra.ai/v1/api/products/b2c3d4e5-f6a7-8901-bcde-f23456789012 \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "price": 59.00,
    "description": "Updated Pro Plan with new features"
  }'
```

Returns the updated product object.
