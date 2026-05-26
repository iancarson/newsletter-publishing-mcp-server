# Limitations and Platform Reality

This repo is intentionally honest about what a newsletter publishing mcp server can and cannot do.

## Core Constraints

- **Draft generation**: Strong fit for MCP and AI agents. Risk level: Low.
- **Editorial review**: Strong fit for MCP. Risk level: Low.
- **Multi-platform publishing**: Needs dedicated distribution layer. Risk level: Medium.
- **Cloud scheduling**: Needs background jobs and account auth refresh. Risk level: Medium.
- **Analytics loop**: Needs persistent platform metrics. Risk level: Medium.

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
