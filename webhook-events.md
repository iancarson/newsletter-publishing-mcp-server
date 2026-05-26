# Webhook Events

Suggested webhook event model for Newsletter Publishing MCP Server.

| Event | When it fires |
|---|---|
| `issue.planned` | A issue planned transition occurs. |
| `asset.generated` | A asset generated transition occurs. |
| `distribution.scheduled` | A distribution scheduled transition occurs. |
| `distribution.completed` | A distribution completed transition occurs. |

## Example Payload

```json
{
  "id": "evt_01HZXNEWSLETTER",
  "type": "issue.planned",
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
