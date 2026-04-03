# Get Payment

Retrieves a payment by its full UUID or short ID.

```
GET /v1/api/payments/:id
```

**Required scope:** `payments:read`

---

## Path parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | `string` | Payment UUID or short ID (e.g. `pXk9mQ`) |

---

## Example

```bash
curl https://apipay.byastra.ai/v1/api/payments/pXk9mQ \
  -H "X-Api-Key: ap_live_your_api_key"
```

## Response `200 OK`

Same shape as the [Create Payment](./create-payment.md) response.
