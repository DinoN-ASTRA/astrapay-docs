# Create Product

```
POST /v1/api/products
```

**Required scope:** `products:manage`

---

## Request body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | `string` | Yes | Product name |
| `description` | `string` | No | Shown at checkout |
| `price` | `number` | Yes | Min: `0.01`. USD for FIAT, token amount for CRYPTO. |
| `currency_type` | `string` | Yes | `FIAT` or `CRYPTO` |
| `token` | `string` | Conditional | Required if `currency_type` is `CRYPTO` |
| `network` | `string` | Conditional | Required if `currency_type` is `CRYPTO` |
| `active` | `boolean` | No | Default: `true` |

---

## Examples

{% tabs %}
{% tab title="FIAT product" %}
```bash
curl -X POST https://apipay.byastra.ai/v1/api/products \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Pro Plan",
    "description": "Monthly subscription",
    "price": 49.00,
    "currency_type": "FIAT"
  }'
```
{% endtab %}

{% tab title="CRYPTO product" %}
```bash
curl -X POST https://apipay.byastra.ai/v1/api/products \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "NFT Pass",
    "price": 1.00,
    "currency_type": "CRYPTO",
    "token": "USDC",
    "network": "BASE"
  }'
```
{% endtab %}
{% endtabs %}

## Response `201 Created`

```json
{
  "success": true,
  "statusCode": 201,
  "data": {
    "id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
    "name": "Pro Plan",
    "description": "Monthly subscription",
    "price": 49.00,
    "currency_type": "FIAT",
    "token": null,
    "network": null,
    "active": true,
    "share_link": "https://pay.byastra.ai/products/b2c3d4e5",
    "created_at": "2026-03-31T12:00:00.000Z",
    "updated_at": "2026-03-31T12:00:00.000Z"
  }
}
```
