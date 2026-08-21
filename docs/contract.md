# Contract guide

The normative YAML is organized from stable domain vocabulary to observable
behavior:

1. `contract` fixes the version and exact-decimal numeric model.
2. `identity` defines the values that host systems may represent with their own
   identifier types.
3. `enums` and `records` define the data exchanged across the billing boundary.
4. `ports` define the persistence and materialized-view capabilities required by
   the engine.
5. `algorithms` define the decisions an implementation must reproduce.
6. `lifecycle` and `invariants` define failure, retry, and consistency behavior.

## Extensibility

Applications may use any string for a service or asset name. The listed values
are convenience examples, not a closed registry. Additional metadata keys are
allowed, and implementations must preserve unknown metadata when it is stored
or forwarded.

The contract intentionally leaves transactions, concurrency primitives, storage
schemas, clocks, and framework middleware to the host runtime. Those concerns
must preserve the transaction and idempotency invariants but do not belong in a
language-neutral data description.

## Decimal values

Amounts and billable quantities are serialized as decimal strings. Implementations
must not use binary floating-point as the source of truth for balance changes or
ledger amounts. Display-only counters may use a native number after exact values
have been calculated.

## Error categories

- `rule-not-found` means no active rule exists for the service.
- `no-billable-usage` means rules existed but filters or zero cost prevented a
  charge.
- `insufficient-funds` means at least one positive cost was calculated and no
  eligible balance could fund it.
- `configuration-error` means the host failed to provide a required identifier,
  transaction, or adapter capability.

These categories are deliberately distinct so callers can choose retry, skip,
or user-facing behavior without parsing implementation-specific messages.
