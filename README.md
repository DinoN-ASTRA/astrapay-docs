# AstraPay API

AstraPay is a non-custodial crypto payment processing platform. Accept USDC, USDT, ETH, BTC, and more — with no KYC requirements on your customers.

**Base URL**

```
https://apipay.byastra.ai/v1/api
```

**Dashboard:** [pay.byastra.ai](https://pay.byastra.ai)

---

## How it works

1. Your server calls `POST /payments` with an amount, token, and network
2. The API returns a `checkout_url`
3. You redirect your customer to that URL
4. AstraPay displays the wallet address, QR code, and live payment tracking
5. On confirmation, a webhook fires and the customer is redirected to your `redirect_url`

It works like Stripe Checkout — create a payment, get a link, send your customer there.

---

## Quick example

```bash
curl -X POST https://apipay.byastra.ai/v1/api/payments \
  -H "X-Api-Key: ap_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "amount": 49.99,
    "token": "USDC",
    "network": "BASE",
    "redirect_url": "https://yourapp.com/success"
  }'
```

**Response:**

```json
{
  "success": true,
  "data": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "short_id": "pXk9mQ",
    "checkout_url": "https://pay.byastra.ai/purchases/pXk9mQ",
    "status": "PENDING",
    "expires_at": "2026-04-01T12:00:00.000Z"
  }
}
```

Redirect your customer to `checkout_url`. Done.

---

## Integration options

| Option | Best for |
|--------|----------|
| [REST API](api-reference/README.md) | Any backend language — direct HTTP calls |
| [TypeScript SDK](sdk/README.md) | Node.js / TypeScript projects |
| [MCP Server](mcp-server/README.md) | AI agents — Claude, Cursor, VS Code Copilot |
