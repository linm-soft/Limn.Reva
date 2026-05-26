# REVA — Event Architecture

## Event schema (concept)

| Field | Type | Description |
|-------|------|-------------|
| id | uuid | Event id |
| type | string | e.g. `order.created` |
| source | string | Service name |
| payload | jsonb | Domain payload |
| status | enum | pending · processing · completed · failed |
| created_at | timestamptz | UTC |

## Catalog (examples)

| Event | Producer | Consumers |
|-------|----------|-----------|
| order.created | reva-order | inventory, analytics, notification |
| order.paid | reva-order | membership, ERP sync (batch) |
| wallet.credited | reva-membership | notification, analytics |
| stock.reserved | reva-inventory | order |

## Worker logic

- Poll `event_jobs` with `FOR UPDATE SKIP LOCKED`
- Retry with exponential backoff (max 5)
- Dead-letter queue after max retries
- Idempotent handlers via `idempotency_key`

## No external broker

Event-job runs on **PostgreSQL** in Phase 1 — no RabbitMQ/Kafka required for MVP.
