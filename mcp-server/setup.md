# MCP Server — Setup

## Prerequisites

- Node.js >= 18
- An AstraPay API key from **Settings → API Keys**

---

## Claude Desktop

Edit `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "astrapay": {
      "command": "npx",
      "args": ["-y", "astrapay-mcp"],
      "env": {
        "ASTRAPAY_API_KEY": "ap_live_your_api_key"
      }
    }
  }
}
```

Restart Claude Desktop. AstraPay tools will appear automatically.

---

## Cursor

Create or edit `.cursor/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "astrapay": {
      "command": "npx",
      "args": ["-y", "astrapay-mcp"],
      "env": {
        "ASTRAPAY_API_KEY": "ap_live_your_api_key"
      }
    }
  }
}
```

---

## VS Code

Edit `.vscode/mcp.json`:

```json
{
  "servers": {
    "astrapay": {
      "command": "npx",
      "args": ["-y", "astrapay-mcp"],
      "env": {
        "ASTRAPAY_API_KEY": "ap_live_your_api_key"
      }
    }
  }
}
```

---

## Environment variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `ASTRAPAY_API_KEY` | Yes | — | Your API key (`ap_live_...` or `ap_test_...`) |
| `ASTRAPAY_API_URL` | No | `https://apipay.byastra.ai` | Override API base URL |
| `ASTRAPAY_API_PREFIX` | No | `/v1` | API route prefix |

{% hint style="warning" %}
Never commit your API key to version control. Use environment variables or a secrets manager.
{% endhint %}
