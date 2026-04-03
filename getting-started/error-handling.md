# Error Handling

All API errors return a consistent JSON structure.

```json
{
  "error": {
    "code": "NOT_FOUND",
    "message": "Payment not found",
    "status": 404
  }
}
```

---

## Error codes

| HTTP status | Code | Description |
|-------------|------|-------------|
| `400` | `BAD_REQUEST` | Missing required field, invalid format, or missing merchant account |
| `401` | `UNAUTHORIZED` | Missing or invalid API key, account not activated, or user banned |
| `403` | `FORBIDDEN` | Insufficient scope, resource belongs to another merchant, or test/live mode mismatch |
| `404` | `NOT_FOUND` | Payment, product, or webhook not found |
| `409` | `CONFLICT` | Duplicate idempotency key with different parameters |
| `422` | `UNPROCESSABLE_ENTITY` | Validation error — e.g. unsupported token/network combination |
| `429` | `RATE_LIMIT_EXCEEDED` | Exceeded 100 requests per minute |
| `500` | `INTERNAL_ERROR` | Server error — contact support if persistent |

---

## Handling errors in code

{% tabs %}
{% tab title="JavaScript" %}
```javascript
const res = await fetch("https://apipay.byastra.ai/v1/api/payments", {
  method: "POST",
  headers: { "X-Api-Key": "ap_live_xxx", "Content-Type": "application/json" },
  body: JSON.stringify({ amount: 25, token: "USDC", network: "BASE" }),
});

if (!res.ok) {
  const { error } = await res.json();
  console.error(`[${error.code}] ${error.message}`);
  // Handle specific codes
  if (error.code === "RATE_LIMIT_EXCEEDED") {
    // retry with backoff
  }
}
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

res = requests.post(
    "https://apipay.byastra.ai/v1/api/payments",
    headers={"X-Api-Key": "ap_live_xxx"},
    json={"amount": 25, "token": "USDC", "network": "BASE"},
)

if not res.ok:
    error = res.json()["error"]
    print(f"[{error['code']}] {error['message']}")
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
For `429` errors, implement exponential backoff. Retrying immediately will not help and may extend your lockout window.
{% endhint %}
