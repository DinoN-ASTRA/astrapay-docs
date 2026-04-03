# Webhook Payloads

When an event occurs, AstraPay sends a `POST` request to your webhook URL with the following structure.

---

## Payload format

```json
{
  "event": "payment.completed",
  "timestamp": "2026-03-31T12:05:00.000Z",
  "data": {
    "payment_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "amount": 25.00,
    "token": "USDC",
    "network": "BASE",
    "status": "completed",
    "transaction_hash": "0xabc123...",
    "test_mode": false
  }
}
```

---

## Request headers

| Header | Description |
|--------|-------------|
| `Content-Type` | `application/json` |
| `X-AstraPay-Signature` | HMAC signature for verification |
| `X-AstraPay-Event` | Event type (e.g. `payment.completed`) |

---

## Payload by event type

### `payment.completed`

```json
{
  "event": "payment.completed",
  "timestamp": "2026-03-31T12:05:00.000Z",
  "data": {
    "payment_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "amount": 25.00,
    "token": "USDC",
    "network": "BASE",
    "status": "completed",
    "transaction_hash": "0xabc123...",
    "test_mode": false
  }
}
```

### `payment.expired`

```json
{
  "event": "payment.expired",
  "timestamp": "2026-04-01T12:00:00.000Z",
  "data": {
    "payment_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "amount": 25.00,
    "token": "USDC",
    "network": "BASE",
    "status": "expired",
    "transaction_hash": null,
    "test_mode": false
  }
}
```

### `payment.canceled`

```json
{
  "event": "payment.canceled",
  "timestamp": "2026-03-31T12:02:00.000Z",
  "data": {
    "payment_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "amount": 25.00,
    "token": "USDC",
    "network": "BASE",
    "status": "canceled",
    "transaction_hash": null,
    "test_mode": false
  }
}
```

### `payment.partially_paid`

```json
{
  "event": "payment.partially_paid",
  "timestamp": "2026-03-31T12:03:00.000Z",
  "data": {
    "payment_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "amount": 25.00,
    "token": "USDC",
    "network": "BASE",
    "status": "partially_paid",
    "transaction_hash": "0xabc123...",
    "test_mode": false
  }
}
```

{% hint style="info" %}
Always use `metadata` in the original payment creation to attach your internal `order_id` or `user_id`. These are returned in the full payment object when you fetch it via the API after receiving a webhook — giving you the context to fulfill the order.
{% endhint %}
