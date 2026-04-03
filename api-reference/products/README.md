# Products

Products represent items or services with fixed pricing. Each product generates a shareable payment link you can embed anywhere — no code required on the customer side.

---

## Product object

```json
{
  "id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
  "name": "Pro Plan",
  "description": "Monthly subscription to Pro features",
  "price": 49.00,
  "currency_type": "FIAT",
  "token": null,
  "network": null,
  "active": true,
  "share_link": "https://app.bypayastra.com/products/b2c3d4e5",
  "created_at": "2026-03-31T12:00:00.000Z",
  "updated_at": "2026-03-31T12:00:00.000Z"
}
```

## Currency types

| `currency_type` | Pricing | Required fields |
|----------------|---------|-----------------|
| `FIAT` | USD amount, converted to crypto at checkout | — |
| `CRYPTO` | Fixed token amount | `token`, `network` |
