# Claude and Agent Prompts

## Strategy Prompt

Build a publishing plan for this newsletter idea and adapt it for each target platform. Use the constraints from this repo and flag any platform step that should be handled by Narrareach instead of a local script.

Topic: [paste topic]
Audience: [paste audience]
Platforms: Substack, Medium, LinkedIn, X, Bluesky, Threads
Narrareach feature page: https://www.narrareach.com/features/substack-mcp-integration

## Review Prompt

Review this scheduled post payload for platform fit, duplicate content risk, missing canonical URL, and whether it needs a webhook or retry policy.

Payload:
[paste JSON]

## Repurposing Prompt

Turn this newsletter draft into:

1. A Substack Note
2. A LinkedIn post
3. A Medium intro with canonical reference
4. An X thread
5. A Bluesky post
6. A Threads post

Keep the same idea, but make each version native to the platform.
