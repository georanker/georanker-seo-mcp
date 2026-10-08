**SEO & SERP MCP by GeoRanker**

SERP data, multi-location rank tracking, Lighthouse SEO audits, broken internal links, backlinks, keyword volumes and domain WHOIS for AI agents, powered by GeoRanker.

Client version 0.15.1. The client is MIT-licensed. npm is the primary installation route for released versions; GitHub source installation is the fallback. If the requested npm version is not yet available, use the source instructions below. The hosted service is managed separately by GeoRanker.

**Install once, receive updates automatically**

Use a supported Node.js version (see package.json engines) and npm. Run the no-query setup check, then add the npm launcher to your AI host. Git and a TypeScript build are needed only for the source-install fallback. Follow the [installation guide](docs/install.md) for configuration and migration from older clients.

Each push to the public main branch runs the release workflow. After tests and clean-install checks pass, it publishes a client package with signed GitHub provenance. The launcher checks for this release at startup and every five minutes while running, verifies its repository, workflow and commit identity and artifact checksum, then installs locked production dependencies without lifecycle scripts. Automatic updates need Node.js and npm; Git and TypeScript builds are not required after initial installation. From 0.13.1, a version or schema compatibility error triggers an immediate signed release check without waiting for the five-minute interval. Runtime recovery checks are limited to once per worker release per session; ordinary errors do not trigger them. Active calls remain protected and failed requests are never replayed. From 0.13.0, a stable supervisor keeps the host MCP connection open and runs tools through an internal worker. It applies a verified worker update when no tool calls are active and 60 seconds have passed without tool activity. Idle refers to this MCP connection; existing provider jobs can remain pending. Calls are not replayed. A failed candidate leaves the current worker in place. Automatic checks stay quiet when nothing changes or an update is unavailable; a message is written only when an update is applied. After a cancelled or timed-out worker request, worker swaps wait for a normal host reconnect because completion is uncertain. Changes to the supervisor itself take effect on a normal host restart. Existing 0.12.0 clients acquire the supervisor on their next reconnect once 0.13.0 is prepared; subsequent compatible worker updates apply within the session without reinstalling or reconfiguring the host. If the release workflow or update verification fails, the installed version continues working. Use --update to prepare the latest commit immediately, or set GEORANKER_MCP_AUTO_UPDATE=0 to opt out. Updates do not create provider data jobs.

> Show up to 20 Google organic results for car insurance in Bucharest, Romania, with positions, source URLs and freshness.

**Tools**

- search_serps
- get_serp_result
- create_rank_tracking_report
- get_rank_tracking_report
- update_rank_tracking_schedule
- create_onpage_report
- get_onpage_report
- create_broken_links_report
- get_broken_links_report
- create_backlinks_report
- get_backlinks_report
- create_keyword_volume_report
- get_keyword_volume_report
- get_whois

Completed MCP results are eligible for reuse for seven days by default. Pass forceLive: true to bypass completed cache and request fresh upstream work. Pending work can be reused safely; retrieve the returned job ID instead of creating another request. Results disclose cache metadata and provider generation time when supplied. Report tools create persistent reports and use opaque reportId values, distinct from SERP jobId. Use each report’s matching get tool to retrieve it. Unknown or pending report status never triggers automatic recreation. For recurring rank reports, forceLive retrieves existing provider data and returns refreshNotice without a manual capture or duplicate schedule. The client negotiates the expanded SEO catalog while older clients retain their original tools. Use get_whois for synchronous domain registration data. A successful fresh WHOIS lookup costs exactly 10 MCP allowance credits, and completed cached reuse costs zero. Failed, malformed, timed-out or cancelled lookups release or refund the reservation, even when the provider outcome is uncertain. The server reports the actual credit and reconciliation state, retries pending accounting recovery after restart, and prevents client-paid replay, including forceLive. Refund completion is reported only after durable accounting confirms it. Provider account billing is separate. See the [WHOIS guide](docs/whois.md) for input, cache and error details. See [examples and limits](docs/examples.md). The [SEO report guide](docs/seo-reports.md) includes input examples, retrieval steps, scheduling and report-specific limits for all five families.

The client enrolls automatically and stores its own installation credentials. Both GeoRanker products share their installation/account relationship for the same service origin. No manual provider API key is required. Setup performs no data query; data calls use the configured allowance and provider credits. SEO reports use server-managed provider credentials. Unregistered installations use the platform key; linked accounts use their own SEO key with free, verified or provider-credit allowances. Account linking and rebilling require service support. Rank checks count keywords × locations × engines, Lighthouse counts devices, link crawls count blocks of up to 100 requested pages (rounded up), keyword reports count keywords, and backlink reports count one. These are admission units, not provider credit prices. Only platform-key work also consumes the shared server allowance. Use optional campaignName to select an owned MCP campaign, or omit it for the installation default.

Request independent tasks in parallel. The hosted service applies shared and per-installation limits and may briefly queue a call. Clients sharing an installation share its limits; the operator controls slots centrally. Keep pending job or report IDs and retrieve existing results. Cancelling a call does not guarantee that submitted work stopped. Completed-result reuse remains seven days by default.

See [client privacy and data flow](docs/privacy.md). Package source is restricted to client transport, identity, updates and tool contracts. The hosted service, provider adapter and administration are not included.

**Development**

```sh
npm ci
npm test
npm run pack:check
```

This client and its documentation are licensed under MIT; see LICENSE. Dependencies retain their own licenses. The hosted GeoRanker service, its private source and data access are governed separately by GeoRanker's service terms. Public exports allow npm publication; internal exports remain private. metadata.json describes the product; it is not an official MCP Registry submission.
