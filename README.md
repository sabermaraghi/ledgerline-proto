# ledgerline-proto

Protobuf contracts shared by Ledgerline services (gRPC APIs and Kafka event schemas).

**Status:** skeleton. Populated in Phase 3 (Days 49+), when the monolith is split into services.

## Plan
- `proto/ledgerline/<context>/v1/*.proto` — one package per bounded context, versioned (`v1`, `v2`).
- `buf` for lint, formatting and **breaking-change detection** (CI blocks incompatible changes).
- Generated Go code strategy (committed `gen/go` module vs. generated per consumer) is decided in an ADR
  in `ledgerline-backend` at the start of Phase 3.

## Rules
1. Never reuse or renumber a field. Deprecate, then remove in a new major version.
2. Event messages carry `tenant_id`, `event_id` (idempotency) and `occurred_at`.
3. Every change goes through a PR with `buf breaking` green.
