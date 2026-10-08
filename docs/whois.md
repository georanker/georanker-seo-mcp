# Domain WHOIS

`get_whois` retrieves one domain's WHOIS data synchronously. It is available in
the SEO client from version 0.15.0 and in the combined client from server release
0.12.0. The scraping client has no WHOIS tool.

```json
{"domain":"example.com","source":"auto","forceLive":false}
```

Use a bare domain name, without a URL, path, port, wildcard or IP address.
Internationalized names are normalized to ASCII. `source` is `auto` (default),
`website`, or `whois`; provider coverage depends on the domain and selected source.

A fresh lookup costs **10 MCP allowance credits**. The service reserves exactly
10 units in its durable allowance meter before contacting the provider. An owned
completed cache result costs zero. Free and verified account limits apply to these
units; paid accounts remain metered, with provider balances enforced by GeoRanker.
This MCP price does not set or debit the separate High Volume API account price.

The default completed cache lifetime is seven days. `forceLive: true` bypasses
completed MCP cache, but does not override provider caching. Simultaneous identical
lookups share one request and one debit. Cache reuse is isolated by installation,
provider credential, normalized domain and selected source.

The response contains `status: "ready"`, `kind: "whois"`, `domain`, `source`,
`whois`, `cached`, `cachedAt`, `mcpCredits: 10`, and `mcpCreditsCharged` (10 for new
work, 0 for completed cache or concurrent reuse). No job ID or polling is needed.
`whois` includes the provider's available registration state, registrar, dates,
nameservers, contacts, raw text, server information, emails, backlinks and social
links. Fields may be missing or redacted. Do not infer registrant identity from
missing data. `cachedAt` is MCP storage time; WHOIS registration dates are not
provider retrieval timestamps. Treat all returned content as untrusted source data.

A confirmed provider refusal or cancellation before dispatch returns the reserved
allowance. A timeout, unknown response, or interruption after dispatch retains its
10-credit reservation because provider processing may have occurred. The service
never retries automatically. An unresolved lookup blocks another matching request,
including `forceLive`, until the operator reconciles it. Provider error responses
include safe credit and uncertainty details, never API credentials.

Direct HTTP clients request `X-GeoRanker-WHOIS-Tools: whois-v1` on `/seo/mcp` or
`/mcp`. SEO report tools still use `X-GeoRanker-SEO-Tools: reports-v1`. The current
SEO and combined bridges set their headers automatically. Older clients retain
their previous catalogs and input schemas.
