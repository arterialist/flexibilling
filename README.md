# FlexiBilling Reference Contract

This repository is the language-neutral reference for FlexiBilling. It describes
the billing domain as a declarative contract so an implementation can be written
for any runtime without copying a language-specific design.

The contract is expressed in YAML and constrained by JSON Schema. It defines:

- domain records, enum values, and canonical numeric representation;
- persistence and cache ports;
- rating, priority-waterfall, funding, charging, refund, and snapshot behavior;
- queue lifecycle states and idempotency requirements; and
- executable conformance vectors for compatible implementations.

There is intentionally no implementation source in this repository. The
contract is the shared semantic boundary; each language package owns its
idiomatic API, concurrency model, and storage adapters.

## Files

- [`spec/flexibilling.yaml`](spec/flexibilling.yaml) — normative contract.
- [`schema/flexibilling.schema.json`](schema/flexibilling.schema.json) — structural schema.
- [`spec/conformance.yaml`](spec/conformance.yaml) — behavior vectors.
- [`docs/contract.md`](docs/contract.md) — reading guide and extension rules.
- [`docs/conformance.md`](docs/conformance.md) — implementation checklist.

## Validation

The repository needs only a YAML parser and a JSON Schema validator. The CI
workflow parses every contract file, validates the normative document, and
rejects language-specific implementation files.

## Compatibility

An implementation is compatible when it preserves the observable behavior in
the contract, including decimal arithmetic, rule ordering, zero-usage versus
insufficient-funds errors, immutable ledger entries, payment-event idempotency,
and pending-record lifecycle transitions.

The contract is versioned independently from package releases. Additive fields
are backward compatible; changing an existing field's meaning requires a new
contract version.
