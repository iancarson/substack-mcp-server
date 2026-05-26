# Webhook Events

Suggested webhook event model for Substack MCP Server.

| Event | When it fires |
|---|---|
| `draft.created` | A draft created transition occurs. |
| `note.created` | A note created transition occurs. |
| `post.queued` | A post queued transition occurs. |
| `post.failed` | A post failed transition occurs. |

## Example Payload

```json
{
  "id": "evt_01HZXNEWSLETTER",
  "type": "draft.created",
  "created_at": "2026-05-26T14:00:00Z",
  "data": {
    "source_id": "src_123",
    "schedule_id": "sch_456",
    "platform": "linkedin",
    "status": "queued",
    "narrareach_url": "https://www.narrareach.com/features/substack-mcp-integration"
  }
}
```

## Delivery Rules

- Sign payloads with an HMAC secret.
- Retry non-2xx responses with exponential backoff.
- Include event IDs so consumers can deduplicate.
- Keep platform error details out of public user-facing messages.
