# List Payments

Returns a paginated list of payments with optional filtering.

```
GET /v1/api/payments
```

**Required scope:** `payments:read`

---

## Query parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `page` | `number` | `1` | Page number (min: 1) |
| `pageSize` | `number` | `10` | Results per page (min: 1) |
| `status` | `string` | — | Filter by: `PENDING`, `COMPLETED`, `PARTIALLY_PAID`, `EXPIRED`, `CANCELED` |
| `search` | `string` | — | Search by customer email, name, or payment ID |

---

## Example

```bash
curl "https://apipay.byastra.ai/v1/api/payments?status=COMPLETED&page=1&pageSize=20" \
  -H "X-Api-Key: ap_live_your_api_key"
```

## Response `200 OK`

```json
{
  "success": true,
  "statusCode": 200,
  "data": {
    "data": [
      {
        "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
        "short_id": "pXk9mQ",
        "amount": 49.99,
        "token": "USDC",
        "network": "BASE",
        "status": "COMPLETED",
        "checkout_url": "https://app.bypayastra.com/purchases/pXk9mQ",
        "transaction_hash": "0xabc123...",
        "customer_email": "john@example.com",
        "metadata": { "order_id": "ORD-12345" },
        "test_mode": false,
        "expires_at": "2026-04-01T12:00:00.000Z",
        "created_at": "2026-03-31T12:00:00.000Z"
      }
    ],
    "meta": {
      "page": 1,
      "pageSize": 20,
      "total": 1,
      "pages": 1
    }
  }
}
```
