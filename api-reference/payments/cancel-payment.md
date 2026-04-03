# Cancel Payment

Cancels a pending payment. Triggers the `payment.canceled` webhook event.

```
POST /v1/api/payments/:id/cancel
```

**Required scope:** `payments:create`

---

## Path parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | `string` | Payment UUID or short ID |

---

## Example

```bash
curl -X POST https://apipay.byastra.ai/v1/api/payments/pXk9mQ/cancel \
  -H "X-Api-Key: ap_live_your_api_key"
```

## Response `200 OK`

Returns the updated payment object with `"status": "CANCELED"`.

{% hint style="warning" %}
Only `PENDING` payments can be canceled. Attempting to cancel a `COMPLETED` or `EXPIRED` payment returns `422`.
{% endhint %}
