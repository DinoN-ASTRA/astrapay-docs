# Rate Limits

| Limit | Window | Scope |
|-------|--------|-------|
| 100 requests | 60 seconds | Per API key |

When exceeded, the API returns `429 RATE_LIMIT_EXCEEDED`:

```json
{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests",
    "status": 429
  }
}
```

Implement exponential backoff when you receive a `429`. Start with a 1s delay and double on each retry, up to a maximum of 60s.
