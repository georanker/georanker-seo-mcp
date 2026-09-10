**SEO & SERP MCP by GeoRanker**

SERP data, multi-location rank tracking, Lighthouse SEO audits, broken internal links, backlinks and keyword volumes for AI agents, powered by GeoRanker.

Public client source, version 0.10.2. Install from this repository; the npm package is not published. The hosted service is managed separately by GeoRanker. Setup checks the connection without submitting a data query. Availability and completion of individual reports depend on the hosted service.

**Start with one useful result**

Build this client with Node.js 22+, run the no-query setup check, and add it to your AI host. Follow the [installation guide](docs/install.md) for Codex, Claude Code, Claude Desktop, Cursor, VS Code, Windsurf, Cline, Continue, Gemini CLI, OpenCode and OMP.

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

Completed MCP results are eligible for reuse for seven days by default. Pass forceLive: true to bypass completed cache and request fresh upstream work. Pending work can be reused safely; retrieve the returned job ID instead of creating another request. Results disclose cache metadata and provider generation time when supplied. Report tools create persistent reports and use opaque reportId values, distinct from SERP jobId. Use each report’s matching get tool to retrieve it. Unknown or pending report status never triggers automatic recreation. For recurring rank reports, forceLive retrieves existing provider data and returns refreshNotice without a manual capture or duplicate schedule. The client negotiates the expanded SEO catalog while older clients retain their original tools. See [examples and limits](docs/examples.md). The [SEO report guide](docs/seo-reports.md) includes input examples, retrieval steps, scheduling and report-specific limits for all five families.

The client enrolls automatically and stores its own installation credentials. Both GeoRanker products share their installation/account relationship for the same service origin. No manual provider API key is required. Setup performs no data query; data calls use the configured allowance and provider credits. SEO reports share an admission allowance. Rank checks count keywords × locations × engines, Lighthouse counts devices, link crawls count blocks of up to 100 requested pages (rounded up), keyword reports count keywords, and backlink reports count one. These are admission units, not provider credit prices.

Request independent tasks in parallel. The hosted service applies shared and per-installation limits and may briefly queue a call. Clients sharing an installation share its limits; the operator controls slots centrally. Keep pending job or report IDs and retrieve existing results. Cancelling a call does not guarantee that submitted work stopped. Completed-result reuse remains seven days by default.

See [client privacy and data flow](docs/privacy.md). Host instructions are based on official configuration documentation; fixture tests are not live-provider or all-host certification. Package source is restricted to public-safe client transport, identity and tool contracts. The hosted service, provider adapter and administration are not included.

**Development**

```sh
npm ci
npm test
npm run pack:check
```

The existing UNLICENSED designation is retained; this publication does not add an open-source license. The private flag in package.json prevents accidental npm publication and does not control GitHub visibility. metadata.json describes the client and is not a submitted official-registry manifest.
