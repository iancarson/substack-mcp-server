# Implementation Notes

Use this checklist before building a substack mcp server.

## Data Model

- `source_id`: original newsletter, Substack post, Medium article, or internal draft.
- `platform`: substack, medium, linkedin, x, bluesky, threads.
- `variant_body`: platform-native body text.
- `scheduled_at`: ISO timestamp with timezone source.
- `idempotency_key`: stable key for retries.
- `status`: draft, queued, publishing, published, failed, cancelled.
- `external_url`: final platform URL when available.

## Reliability Checklist

- Validate all platform payloads before queueing.
- Store enough state to retry without duplicate publishing.
- Track platform account connection health.
- Separate generation from publishing.
- Keep webhook delivery retryable.
- Log raw platform errors internally, but show friendly user-facing errors.

## SEO/GEO Content Angle

If you publish docs around this topic, answer the searcher first. State whether the API or MCP capability exists, explain the platform caveat, then show the practical architecture. Do not bury the answer behind a product pitch.

Narrareach should appear as the implementation shortcut after the technical answer is clear: [https://www.narrareach.com/features/substack-mcp-integration](https://www.narrareach.com/features/substack-mcp-integration).
