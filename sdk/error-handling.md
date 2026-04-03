# SDK — Error Handling

The SDK throws `AstraPayError` for all API and network failures.

```typescript
import { AstraPayClient, AstraPayError } from "@astra-pay/sdk";

try {
  const payment = await client.payments.get("invalid-id");
} catch (err) {
  if (err instanceof AstraPayError) {
    console.error(`[${err.code}] ${err.message}`);
    // e.g. [NOT_FOUND] Payment not found

    console.error(`HTTP status: ${err.status}`);
    // e.g. 404
  }
}
```

---

## Error properties

| Property | Type | Description |
|----------|------|-------------|
| `status` | `number` | HTTP status code. `0` for network errors. |
| `code` | `string` | Machine-readable error code |
| `message` | `string` | Human-readable description |

---

## Error codes

| Code | Status | Description |
|------|--------|-------------|
| `NOT_FOUND` | 404 | Resource not found |
| `UNAUTHORIZED` | 401 | Invalid or missing API key |
| `FORBIDDEN` | 403 | Insufficient scope |
| `VALIDATION_ERROR` | 422 | Invalid parameters |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests |
| `NETWORK_ERROR` | 0 | Connection failed |
| `TIMEOUT` | 0 | Request timed out |

---

## Handling rate limits

```typescript
async function createPaymentWithRetry(params, maxRetries = 3) {
  for (let attempt = 0; attempt < maxRetries; attempt++) {
    try {
      return await client.payments.create(params);
    } catch (err) {
      if (err instanceof AstraPayError && err.status === 429) {
        const delay = Math.pow(2, attempt) * 1000; // 1s, 2s, 4s
        await new Promise((r) => setTimeout(r, delay));
        continue;
      }
      throw err;
    }
  }
}
```
