# Signature Verification

Every webhook request is signed using your webhook secret. Always verify the signature before processing the payload — this confirms the request came from AstraPay and has not been tampered with.

---

## Signature format

The `X-AstraPay-Signature` header contains a timestamp and HMAC-SHA256 signature:

```
X-AstraPay-Signature: t=1711900000,v1=5257a869e7ecebeda32affa62cdca3fa51cad7e77a0e56ff536d0ce8e108d8bd
```

---

## Verification steps

1. Extract the timestamp (`t`) and signature (`v1`) from the header
2. Construct the signed string: `{timestamp}.{raw JSON body}`
3. Compute HMAC-SHA256 of that string using your webhook secret
4. Compare your computed value to `v1` using a constant-time comparison

---

## Code examples

{% tabs %}
{% tab title="Node.js" %}
```javascript
const crypto = require("crypto");

function verifyWebhookSignature(rawBody, signatureHeader, secret) {
  const parts = Object.fromEntries(
    signatureHeader.split(",").map((p) => p.split("="))
  );

  const timestamp = parts["t"];
  const signature = parts["v1"];

  const expected = crypto
    .createHmac("sha256", secret)
    .update(`${timestamp}.${rawBody}`)
    .digest("hex");

  return crypto.timingSafeEqual(
    Buffer.from(signature, "hex"),
    Buffer.from(expected, "hex")
  );
}

// Express route example
app.post("/webhooks/astrapay", express.raw({ type: "application/json" }), (req, res) => {
  const sig = req.headers["x-astrapay-signature"];

  if (!verifyWebhookSignature(req.body.toString(), sig, process.env.WEBHOOK_SECRET)) {
    return res.status(401).send("Invalid signature");
  }

  const event = JSON.parse(req.body.toString());

  if (event.event === "payment.completed") {
    // Fulfill order using event.data
  }

  res.sendStatus(200);
});
```
{% endtab %}

{% tab title="Python" %}
```python
import hmac
import hashlib
import json

def verify_webhook_signature(raw_body: str, signature_header: str, secret: str) -> bool:
    parts = dict(p.split("=", 1) for p in signature_header.split(","))
    timestamp = parts["t"]
    signature = parts["v1"]

    payload = f"{timestamp}.{raw_body}"
    expected = hmac.new(
        secret.encode(), payload.encode(), hashlib.sha256
    ).hexdigest()

    return hmac.compare_digest(signature, expected)

# FastAPI / Flask example
@app.post("/webhooks/astrapay")
async def handle_webhook(request: Request):
    raw_body = await request.body()
    sig = request.headers.get("x-astrapay-signature", "")

    if not verify_webhook_signature(raw_body.decode(), sig, WEBHOOK_SECRET):
        raise HTTPException(status_code=401, detail="Invalid signature")

    event = json.loads(raw_body)

    if event["event"] == "payment.completed":
        # Fulfill order
        pass

    return {"ok": True}
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
Use `express.raw()` (Node.js) or the equivalent raw body parser in your framework — not `express.json()`. Signature verification requires the **raw bytes** of the request body. Parsing to JSON first and re-serializing will produce a different string and cause verification to fail.
{% endhint %}
