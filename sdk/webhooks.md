# SDK — Webhooks

## `client.webhooks.create(params)`

```typescript
const webhook = await client.webhooks.create({
  url: "https://yourapp.com/webhooks/astrapay",
  events: ["payment.completed", "payment.canceled"],
});

// Store this securely — only returned once
console.log(webhook.secret); // "whsec_..."
```

---

## `client.webhooks.list()`

```typescript
const webhooks = await client.webhooks.list();
```

---

## `client.webhooks.get(id)`

```typescript
const webhook = await client.webhooks.get("c3d4e5f6-...");
```

---

## `client.webhooks.update(id, params)`

```typescript
const updated = await client.webhooks.update("c3d4e5f6-...", {
  events: ["payment.completed", "payment.expired"],
  active: true,
});
```

---

## `client.webhooks.delete(id)`

```typescript
await client.webhooks.delete("c3d4e5f6-...");
```
