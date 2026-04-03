# Payments

Payments are the core object in AstraPay. Each payment represents a single crypto checkout session with a hosted page, wallet address, QR code, and countdown timer.

---

## Payment object

```json
{
  "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "short_id": "pXk9mQ",
  "amount": 25.00,
  "token": "USDC",
  "network": "BASE",
  "status": "PENDING",
  "checkout_url": "https://app.bypayastra.com/purchases/pXk9mQ",
  "transaction_hash": null,
  "customer_email": "john@example.com",
  "customer_name": "John Doe",
  "metadata": { "order_id": "ORD-12345" },
  "test_mode": false,
  "redirect_url": "https://yourapp.com/success",
  "cancel_url": null,
  "expires_at": "2026-04-01T12:00:00.000Z",
  "created_at": "2026-03-31T12:00:00.000Z"
}
```

## Status values

| Status | Description |
|--------|-------------|
| `PENDING` | Awaiting payment |
| `COMPLETED` | Payment confirmed on-chain |
| `PARTIALLY_PAID` | Less than the full amount received |
| `EXPIRED` | Timer elapsed, no payment received |
| `CANCELED` | Canceled via API or dashboard |
