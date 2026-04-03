# Create Payment

Creates a new crypto payment and returns a hosted checkout URL.

```
POST /v1/api/payments
```

**Required scope:** `payments:create`

---

## Request body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `amount` | `number` | Conditional | Amount in USD. Required if `product_id` is not provided. Min: `0.01`. |
| `product_id` | `string` | Conditional | Product ID to charge for. Required if `amount` is not provided. |
| `token` | `string` | Yes | Crypto token to accept. See [Supported Tokens](../../reference/tokens-networks.md). |
| `network` | `string` | Yes | Blockchain network. See [Supported Tokens](../../reference/tokens-networks.md). |
| `customer_email` | `string` | No | Customer's email address. |
| `customer_name` | `string` | No | Customer's name. |
| `redirect_url` | `string` | No | URL to redirect the customer after successful payment. |
| `cancel_url` | `string` | No | URL to redirect if the customer cancels. |
| `metadata` | `object` | No | Custom key-value pairs stored with the payment. Returned in webhook payloads. |

---

## Example

{% tabs %}
{% tab title="cURL" %}
```bash
curl -X POST https://apipay.byastra.ai/v1/api/payments \
  -H "Content-Type: application/json" \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Idempotency-Key: order_12345" \
  -d '{
    "amount": 49.99,
    "token": "USDC",
    "network": "BASE",
    "customer_email": "john@example.com",
    "redirect_url": "https://yourapp.com/success",
    "metadata": {
      "order_id": "ORD-12345",
      "plan": "pro"
    }
  }'
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const res = await fetch("https://apipay.byastra.ai/v1/api/payments", {
  method: "POST",
  headers: {
    "X-Api-Key": "ap_live_your_api_key",
    "Content-Type": "application/json",
    "Idempotency-Key": "order_12345",
  },
  body: JSON.stringify({
    amount: 49.99,
    token: "USDC",
    network: "BASE",
    redirect_url: "https://yourapp.com/success",
    metadata: { order_id: "ORD-12345" },
  }),
});

const { data } = await res.json();
window.location.href = data.checkout_url;
```
{% endtab %}

{% tab title="Python" %}
```python
import requests

res = requests.post(
    "https://apipay.byastra.ai/v1/api/payments",
    headers={
        "X-Api-Key": "ap_live_your_api_key",
        "Idempotency-Key": "order_12345",
    },
    json={
        "amount": 49.99,
        "token": "USDC",
        "network": "BASE",
        "redirect_url": "https://yourapp.com/success",
        "metadata": {"order_id": "ORD-12345"},
    },
)

checkout_url = res.json()["data"]["checkout_url"]
```
{% endtab %}
{% endtabs %}

---

## Response `201 Created`

```json
{
  "success": true,
  "statusCode": 201,
  "data": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "amount": 49.99,
    "token": "USDC",
    "network": "BASE",
    "status": "PENDING",
    "checkout_url": "https://app.bypayastra.com/purchases/pXk9mQ",
    "transaction_hash": null,
    "customer_email": "john@example.com",
    "customer_name": null,
    "metadata": { "order_id": "ORD-12345", "plan": "pro" },
    "test_mode": false,
    "redirect_url": "https://yourapp.com/success",
    "cancel_url": null,
    "expires_at": "2026-04-01T12:00:00.000Z",
    "created_at": "2026-03-31T12:00:00.000Z"
  }
}
```

{% hint style="info" %}
Use the `Idempotency-Key` header with your order ID to safely retry failed requests without creating duplicate payments. See [Idempotency](../../getting-started/idempotency.md).
{% endhint %}
