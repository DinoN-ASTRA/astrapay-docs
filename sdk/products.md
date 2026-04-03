# SDK — Products

## `client.products.create(params)`

```typescript
// FIAT product (USD pricing, converted at checkout)
const product = await client.products.create({
  name: "Pro Plan",
  description: "Monthly subscription",
  price: 49.00,
  currency_type: "FIAT",
});

// CRYPTO product (fixed token amount)
const nftPass = await client.products.create({
  name: "NFT Pass",
  price: 1.00,
  currency_type: "CRYPTO",
  token: "USDC",
  network: "BASE",
});

console.log(product.share_link);
// => "https://pay.byastra.ai/products/b2c3d4e5"
```

---

## `client.products.list()`

```typescript
const products = await client.products.list();
```

---

## `client.products.get(id)`

```typescript
const product = await client.products.get("b2c3d4e5-f6a7-8901-bcde-f23456789012");
```

---

## `client.products.update(id, params)`

```typescript
const updated = await client.products.update("b2c3d4e5-...", {
  price: 59.00,
  active: true,
});
```

---

## `client.products.delete(id)`

```typescript
const result = await client.products.delete("b2c3d4e5-...");
// => { deleted: true }
```
