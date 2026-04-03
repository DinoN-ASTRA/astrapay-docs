# SDK — Payments

## `client.payments.create(params)`

```typescript
const payment = await client.payments.create({
  amount: 49.99,               // or product_id: "b2c3d4e5-..."
  token: "USDC",
  network: "BASE",
  customer_email: "john@example.com",
  customer_name: "John Doe",
  redirect_url: "https://yourapp.com/success",
  cancel_url: "https://yourapp.com/cancel",
  metadata: { order_id: "ORD-12345", plan: "pro" },
});

// Redirect customer to hosted checkout
window.location.href = payment.checkout_url;
```

---

## `client.payments.get(id)`

Accepts UUID or short ID.

```typescript
const payment = await client.payments.get("pXk9mQ");
console.log(payment.status); // "PENDING" | "COMPLETED" | "EXPIRED" | "CANCELED" | "PARTIALLY_PAID"
```

---

## `client.payments.list(params?)`

```typescript
const { data, meta } = await client.payments.list({
  status: "COMPLETED",
  search: "john@example.com",
  page: 1,
  pageSize: 20,
});

console.log(`${meta.total} total payments across ${meta.pages} pages`);
```

---

## `client.payments.cancel(id)`

```typescript
const canceled = await client.payments.cancel("a1b2c3d4-...");
console.log(canceled.status); // "CANCELED"
```
