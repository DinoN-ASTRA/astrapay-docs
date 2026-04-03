# TypeScript SDK

The official TypeScript/JavaScript SDK for the AstraPay API. Zero runtime dependencies — uses native `fetch`.

**Package:** `@astralabs/sdk`\
**Requires:** Node.js >= 18.0.0

---

## Installation

```bash
npm install @astralabs/sdk
# or
yarn add @astralabs/sdk
```

---

## Quick start

```typescript
import { AstraPayClient } from "@astralabs/sdk";

const client = new AstraPayClient("ap_live_your_api_key");

const payment = await client.payments.create({
  amount: 49.99,
  token: "USDC",
  network: "BASE",
  customer_email: "john@example.com",
  redirect_url: "https://yourapp.com/success",
});

console.log(payment.checkout_url);
// => "https://app.bypayastra.com/purchases/pXk9mQ"
```

---

## Constructor

```typescript
const client = new AstraPayClient(apiKey: string, options?: ClientOptions);
```

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `apiKey` | `string` | — | Your API key (required) |
| `options.baseUrl` | `string` | `https://apipay.byastra.ai` | Override API base URL |
| `options.prefix` | `string` | `/v1` | API route prefix |

---

## Available modules

| Module | Description |
|--------|-------------|
| [`client.payments`](./payments.md) | Create, get, list, cancel payments |
| [`client.products`](./products.md) | Full CRUD on products |
| [`client.webhooks`](./webhooks.md) | Register and manage webhooks |
