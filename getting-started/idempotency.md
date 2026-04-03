# Idempotency

The Payments API supports idempotent requests so you can safely retry failed operations without creating duplicate payments.

---

## Usage

Include an `Idempotency-Key` header with a unique string — your order ID is a good choice:

```http
Idempotency-Key: order_12345
```

If a request with the same key was already processed, the original cached response is returned immediately. No duplicate payment is created.

---

## Behavior

- Keys are **scoped per merchant** — different merchants can use the same key
- Cached responses expire after **24 hours**
- Only applies to `POST /v1/api/payments`
- A `409 CONFLICT` is returned if the same key is used with **different parameters**

---

## Example

```bash
# First request — creates the payment
curl -X POST https://apipay.byastra.ai/v1/api/payments \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Idempotency-Key: order_12345" \
  -H "Content-Type: application/json" \
  -d '{"amount": 25, "token": "USDC", "network": "BASE"}'

# Retry with same key — returns cached response, no duplicate created
curl -X POST https://apipay.byastra.ai/v1/api/payments \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Idempotency-Key: order_12345" \
  -H "Content-Type: application/json" \
  -d '{"amount": 25, "token": "USDC", "network": "BASE"}'
```

{% hint style="info" %}
Use your internal order ID or a UUID generated at checkout session creation as the idempotency key. This ensures that even if your server crashes mid-request, retrying is always safe.
{% endhint %}
