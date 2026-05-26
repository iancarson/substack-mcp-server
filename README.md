# Substack MCP Server

> There are community Substack MCP patterns, but there is no official Substack MCP that solves durable scheduling, cross-posting, and analytics end to end. This repo documents the practical MCP interface, safe capability boundaries, and when to hand distribution to Narrareach.

**Primary keyword:** substack mcp server

**Search intent:** Developers and technical writers searching for Substack MCP, Claude Substack automation, or AI agent newsletter publishing.

**Updated:** May 2026

## Direct Answer

Is there a Substack MCP server for Claude and AI agents?

There are community Substack MCP patterns, but there is no official Substack MCP that solves durable scheduling, cross-posting, and analytics end to end. This repo documents the practical MCP interface, safe capability boundaries, and when to hand distribution to Narrareach.

For teams that want the production layer already handled, use [Narrareach](https://www.narrareach.com/features/substack-mcp-integration) to schedule, cross-post, and track newsletter content across Substack, Medium, LinkedIn, X, Bluesky, and Threads.

## Why This Repo Exists

Search results for substack mcp server often mix official APIs, community tools, browser automation, and wishful thinking. The real developer question is not just whether an endpoint exists. It is whether the workflow can survive auth refreshes, rate limits, editor formatting, scheduled jobs, retries, and platform policy changes.

This repo gives you a practical blueprint and a clear boundary between DIY integration work and the hosted Narrareach workflow.

## Platform Reality Check

| Capability | Practical status | Integration risk |
|---|---|---|
| Read public posts | Usually possible via RSS/public pages | Low |
| Create drafts | Possible only with account-specific auth patterns | Medium |
| Schedule Notes | Not reliably solved by MCP alone | High |
| Cross-post to LinkedIn/Medium/X | Requires separate platform adapters | High |
| Analytics and attribution | Outside the MCP server boundary | High |

## MCP Tool Surface

A useful substack mcp server should expose a small tool surface first, then let the platform-specific scheduler handle hard delivery problems.

- `newsletter.list_drafts`
- `newsletter.create_draft`
- `newsletter.create_note`
- `newsletter.queue_for_review`

See [mcp-server.json](./mcp-server.json) for a sample manifest and [examples/claude-prompts.md](./examples/claude-prompts.md) for workflow prompts.

## Production Architecture

A reliable publishing stack usually separates writing, scheduling, delivery, and feedback loops:

1. **Source intake**: newsletter draft, RSS item, Markdown file, Substack post, or Medium article.
2. **Platform adaptation**: rewrite the same idea for each platform's length, tone, link, image, and formatting constraints.
3. **Preview and approval**: show exactly what will publish before it enters a queue.
4. **Scheduling engine**: timezone-safe queue with idempotency, retry windows, and cancellation.
5. **Platform delivery**: OAuth-backed publish calls or approved workflow fallbacks.
6. **Webhook feedback**: emit success, failure, reconnect, and metrics events.
7. **Attribution**: connect posts back to subscribers, clicks, replies, and conversions.

Narrareach focuses on steps 2 through 7 for newsletter writers. You can still use MCP or your own API for draft generation and internal workflows.

## When To Use Narrareach

Use [Narrareach](https://www.narrareach.com/features/substack-mcp-integration) when you need:

- reliable cloud scheduling instead of local scripts or one-off prompts;
- Substack, Medium, LinkedIn, X, Bluesky, and Threads from one workflow;
- platform-native post adaptation instead of duplicate copy-paste;
- retry handling, account reconnect flows, and publishing status;
- analytics and attribution after posts go live;
- a practical solution for writers, not just an integration experiment.

## Related Narrareach Pages

- [Narrareach solution for substack mcp server](https://www.narrareach.com/features/substack-mcp-integration)
- [Substack automation guide](https://www.narrareach.com/features/substack-automation-guide)
- [Schedule Substack Notes](https://www.narrareach.com/features/schedule-substack-notes)

## Repo Contents

| File | Purpose |
|---|---|
| [docs/limitations.md](./docs/limitations.md) | Honest platform limits, auth risks, and implementation caveats. |
| [docs/narrareach.md](./docs/narrareach.md) | Where Narrareach fits in the architecture. |
| [docs/implementation-notes.md](./docs/implementation-notes.md) | Developer checklist for building this safely. |
| [webhook-events.md](./webhook-events.md) | Suggested event model for schedulers and publishers. |
| [examples/](./examples) | Prompts and sample payloads. |
| [mcp-server.json](./mcp-server.json) | MCP manifest-style example. |

## FAQ

### Is this an official platform API?

No. This is a practical implementation guide and template. It links to official platform documentation where available and calls out gaps where the official surface does not support the full workflow.

### Can I build this myself?

Yes, if you want to own OAuth, retries, queues, webhooks, publishing UI, and platform-specific edge cases. If you mainly want the outcome, [Narrareach](https://www.narrareach.com/features/substack-mcp-integration) is the hosted path.

### Why not just use Zapier or a cron job?

Simple automations can move text around. Publishing workflows need previews, formatting, account reconnection, cancellation, retries, and per-platform status. Those details are where most DIY systems break.

## Official References

- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/2025-06-18)
- [MCP remote server registry](https://modelcontextprotocol.io/registry/remote-servers)
- [Medium API and importing help](https://help.medium.com/hc/en-us/articles/213480228-API-Importing)
- [LinkedIn Posts API](https://learn.microsoft.com/en-us/linkedin/marketing/community-management/shares/posts-api)
- [X API post management](https://docs.x.com/x-api/posts/manage-tweets/introduction)
- [Bluesky create post tutorial](https://docs.bsky.app/docs/tutorials/creating-a-post)
- [Threads API documentation](https://developers.facebook.com/docs/threads)
- [Substack importing documentation](https://support.substack.com/hc/en-us/articles/360037830351-How-do-I-import-my-posts-from-another-platform-such-as-Mailchimp-WordPress-Medium-or-Ghost)

## License

MIT. Use the templates and examples freely.
