**SEO & SERP MCP by GeoRanker: first workflow**

Show up to 20 Google organic results for car insurance in Bucharest, Romania, with positions, source URLs and freshness.

Call search_serps with this input to request live fetching:

```json
{
  "query": "car insurance",
  "region": "Bucharest,Romania",
  "searchEngine": "google",
  "pages": 2,
  "forceLive": true
}
```

Omit forceLive or set it to false to allow seven-day completed-cache reuse. Live fetching bypasses the MCP cache, not the provider's own processing rules. If pending, call get_serp_result with the same jobId. Lookups never start another data job.

Requested depth is at most 100 organic results; returned coverage may be lower. An absent domain is not found within the returned results, not a measured position beyond them. Use create_rank_tracking_report for multi-keyword/multi-location domain tracking and optional explicit recurring schedules. Lighthouse audits, internal-link crawls, backlink reports and keyword-volume reports have separate create/get tools. Recurring runs require operator enablement and can consume future credits. For an existing recurring rank report, forceLive or expired ready cache retrieves the same report and returns refreshNotice; it does not request a manual capture or create another schedule. Lighthouse output is a labeled summary without screenshots or detailed resource/audit tables. Report completion and provider coverage are returned as supplied; unknown completion is not a successful result claim.

Display cached, cachedAt and generatedAt when available. A missing provider generation timestamp must not be invented. The default does not mean background refresh every seven days.

Request independent tasks in parallel. The hosted service applies shared and per-installation limits and may briefly queue a call. Clients sharing an installation share its limits; the operator controls slots centrally. Keep pending job or report IDs and retrieve existing results. Cancelling a call does not guarantee that submitted work stopped. Completed-result reuse remains seven days by default.
