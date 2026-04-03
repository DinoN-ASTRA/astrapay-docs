# Test Mode

Test mode lets you build and test your integration without processing real blockchain transactions.

---

## How it works

1. Create a test API key in **Settings → API Keys** (enable Test Mode)
2. Use your `ap_test_` key in API requests
3. Payments auto-complete after **10 seconds** — no real crypto is sent or received
4. The `transaction_hash` is set to `test_tx_simulated`

---

## Test vs live isolation

Test and live data are completely separated. A test key can never read or modify live payments, and vice versa.

| Action | Test key | Live key |
|--------|----------|----------|
| Create payment | Creates test payment (auto-completes) | Creates real payment |
| List payments | Returns only test payments | Returns only live payments |
| Get payment | Can only access test payments | Can only access live payments |
| Cancel payment | Can only cancel test payments | Can only cancel live payments |

---

## Test webhook payloads

Test mode payments trigger webhooks normally, with `"test_mode": true`:

```json
{
  "event": "payment.completed",
  "timestamp": "2026-03-31T12:00:10.000Z",
  "data": {
    "payment_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "amount": 25.00,
    "token": "USDC",
    "network": "BASE",
    "status": "completed",
    "transaction_hash": "test_tx_simulated",
    "test_mode": true
  }
}
```

{% hint style="info" %}
Use test mode to fully exercise your webhook handler and fulfillment logic before going live.
{% endhint %}
