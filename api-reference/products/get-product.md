# Get Product

```
GET /v1/api/products/:id
```

**Required scope:** `products:manage`

---

## Path parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | `string` | Product UUID |

---

## Example

```bash
curl https://apipay.byastra.ai/v1/api/products/b2c3d4e5-f6a7-8901-bcde-f23456789012 \
  -H "X-Api-Key: ap_live_your_api_key"
```

Response is the same shape as [Create Product](./create-product.md).
