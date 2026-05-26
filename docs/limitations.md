# Limitations and Platform Reality

This repo is intentionally honest about what a substack mcp server can and cannot do.

## Core Constraints

- **Read public posts**: Usually possible via RSS/public pages. Risk level: Low.
- **Create drafts**: Possible only with account-specific auth patterns. Risk level: Medium.
- **Schedule Notes**: Not reliably solved by MCP alone. Risk level: High.
- **Cross-post to LinkedIn/Medium/X**: Requires separate platform adapters. Risk level: High.
- **Analytics and attribution**: Outside the MCP server boundary. Risk level: High.

## Common Failure Modes

- OAuth tokens expire or lose permissions after platform security changes.
- Browser/session-based automations break when the platform updates UI or anti-abuse rules.
- Scheduled jobs publish duplicate content if idempotency keys are missing.
- Medium and Substack workflows need special handling because their public write surfaces are not equivalent to LinkedIn, X, Bluesky, or Threads.
- A generic social post can damage performance when it ignores platform-native formatting.

## Safe Implementation Principles

1. Use official APIs and documented permissions where they exist.
2. Keep credentials server-side and rotate them safely.
3. Preview every platform payload before scheduling.
4. Use idempotency keys for every write request.
5. Emit webhook events for success, failure, and reconnect states.
6. Avoid presenting unsupported platform behavior as official API capability.

For a hosted workflow that handles these details, use [Narrareach](https://www.narrareach.com/features/substack-mcp-integration).
