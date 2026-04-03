# MCP Server

The AstraPay MCP (Model Context Protocol) server lets AI agents — Claude, Cursor, VS Code Copilot, and any LLM-powered tool — manage payments, products, and webhooks through natural language.

**npm:** [`astrapay-mcp`](https://www.npmjs.com/package/astrapay-mcp)

---

## How it works

Instead of writing API calls, you describe what you want:

> *"Create a $49.99 USDC payment on Base for john@example.com"*

The AI agent reads the MCP tool definitions, maps your intent to the right parameters, and calls the AstraPay API automatically. You get back the `checkout_url` and can act on it immediately.

---

## What you can do

```
"Create a $25 USDC payment on Base for john@example.com"
"Show me all pending payments"
"Has payment pXk9mQ been completed?"
"Cancel payment pXk9mQ"
"Create a product called 'Pro Plan' for $49"
"Set up a webhook at https://myapp.com/hooks for payment completions"
"List all my webhooks"
```

---

## Available tools

13 tools across payments, products, and webhooks. See [Available Tools](./tools.md) for the full list.
