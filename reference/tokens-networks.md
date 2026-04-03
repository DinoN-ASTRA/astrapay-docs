# Supported Tokens & Networks

Use the `token` and `network` fields in payment and product creation requests. Not all token/network combinations are supported — refer to the table below.

---

## Compatibility matrix

| Token | ERC20 (Ethereum) | BASE (Base) | BEP20 (BNB Chain) | ARB (Arbitrum) | POL (Polygon) |
|-------|:----------------:|:-----------:|:-----------------:|:--------------:|:-------------:|
| **USDT** | Yes | — | Yes | Yes | Yes |
| **USDC** | Yes | Yes | Yes | Yes | Yes |
| **DAI** | Yes | — | Yes | — | Yes |
| **ETH** | Yes | Yes | — | Yes | — |
| **BNB** | — | — | Yes | — | — |
| **POL** | — | — | — | — | Yes |
| **ASTRAAI** | Yes | — | — | — | — |

---

## Networks

| Network | Chain | Notes |
|---------|-------|-------|
| `ERC20` | Ethereum mainnet | Highest fees |
| `BASE` | Base (Coinbase L2) | Lowest fees — recommended for most use cases |
| `BEP20` | BNB Chain | Low fees |
| `ARB` | Arbitrum One | Low fees |
| `POL` | Polygon PoS | Low fees |

{% hint style="info" %}
**Recommended default:** USDC on BASE. Lowest transaction fees, fast confirmation, and wide wallet support.
{% endhint %}

---

## Example — specifying token and network

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

An unsupported combination (e.g. `ETH` on `BEP20`) returns `422 UNPROCESSABLE_ENTITY`.
