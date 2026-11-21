# Aakaar MCP

The Aakaar MCP lets AI assistants such as Claude and ChatGPT work with your Amazon seller and Amazon Ads data through [Aakaar AI](https://aakaarai.com). You ask questions in plain English, and the assistant pulls the numbers from your connected Amazon accounts.

This repository holds documentation only. The server is hosted by Aakaar AI, and there is nothing to install or run locally.

## Server URL

```
https://mcp.aakaarai.com/mcp
```

Transport: remote MCP over HTTP. Sign-in: OAuth (see below).

## What you can do

The server has 60+ tools, a prompt library and approval-gated actions. It covers:

- **Amazon Ads:** Sponsored Products, Sponsored Brands, Sponsored Display and DSP.
- **Seller Central:** orders, inventory, FBA fees, returns, listings and profit after fees.
- **Vendor Central:** shipped revenue, margin, purchase orders and forecasts.
- **Brand Analytics:** search query performance and search terms.
- **Amazon Marketing Cloud (AMC):** path-to-purchase and overlap analyses, and building audiences. This needs an AMC instance linked to your Amazon Ads account.
- **Market intelligence:** keyword search volume, who holds the top positions for large keywords, and category growth, next to your own data.
- **History and freshness:** hourly ad metrics, new orders within minutes, and 1 to 2 years of stored history.
- **Marketplaces:** 23 Amazon marketplaces through one connection. Agencies can switch between brands by name.

Examples of outcome-level tools: `get_account_health_report`, `get_asin_profitability_report`, `create_amc_audience`.

Example questions:

- "Give me a health check of my Amazon account for the last 30 days."
- "Why did my ACoS jump last week?"
- "Which high-volume keywords in my category am I not bidding on?"

**Changes are approval-gated.** The assistant can change bids and budgets, add negative keywords, create and update campaigns, update listings and build AMC audiences, but only after you approve each change. Aakaar logs each change with the prompt that asked for it, the time, and the before and after values, and it can be rolled back where Amazon allows.

Aakaar also publishes a free prompt library on [aakaarai.com/mcp](https://aakaarai.com/mcp).

## Sign in

The server uses OAuth 2.1 with PKCE and dynamic client registration:

1. Add the server URL in your MCP client.
2. Your client sends you to Aakaar to sign in and approve access.
3. You are redirected back and connected.

No API keys are pasted into the client. Aakaar takes your identity from the authenticated session, never from parameters the model sends.

You need an Aakaar account (there is a 14-day free trial) with your Amazon accounts connected.

## Setup

### Claude (claude.ai and Claude Desktop)

1. In Claude, click the add (+) icon, hover over **Add connector** and select **Add custom connector**.
2. Paste `https://mcp.aakaarai.com/mcp` as the Server URL, enter a name such as "Aakaar AI" and click **Continue**.
3. Review the connector settings, click **Add**, then finish signing in to Aakaar in the pop-up window.

### ChatGPT

1. Turn on Developer mode under **Settings**, then **Security**.
2. Go to **Plugins**, add a custom MCP server and click **Create MCP App**.
3. Paste `https://mcp.aakaarai.com/mcp` into the **Connection** field and sign in to Aakaar.

### Other MCP clients

Any client that supports remote MCP over HTTP with OAuth can use the server URL above. Aakaar's site also lists setup for Grok (under Plugins) and Microsoft 365 Copilot (an admin adds it once in the Admin Center).

## Privacy and security

From what Aakaar states at [aakaarai.com/mcp](https://aakaarai.com/mcp):

- Sign-in uses OAuth 2.1 with PKCE. Tokens are scoped to the MCP, not a long-lived API key handed to the model.
- Access is scoped to the Amazon accounts you connect.
- Data is isolated per tenant, with encryption in transit and at rest.
- Every tool call is logged with a timestamp, and the audit log is exportable.
- Writes run only after you approve them.

See the [privacy policy](https://www.aakaarai.com/privacy-policy) and [terms of use](https://www.aakaarai.com/terms-and-conditions).

## Links

- Product page and setup guides: https://aakaarai.com/mcp
- Docs: https://www.aakaarai.com/docs
- Support: support@aakaarai.com
- Website: https://aakaarai.com

## License

The documentation in this repository is released under the [MIT License](LICENSE).
