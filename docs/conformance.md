# Conformance checklist

An implementation should demonstrate the following before claiming contract
compatibility:

- exact fixed, quantity, duration, and units rating;
- metadata duration taking precedence over the record field;
- dotted-path filter matching and filter-mismatch handling;
- ascending-priority waterfall selection;
- fallback to a later asset when an earlier balance is insufficient;
- distinction between zero usage and insufficient funds;
- atomic balance plus ledger behavior for charge, refund, and usage processing;
- top-up and monthly-quota product strategies;
- payment-reference idempotency;
- pending, processed, failed, skipped, and retry behavior;
- usage-session accumulation and exception-write policy;
- cold-cache balance checks and gatekeeper denial;
- worker result counts and queue transitions;
- period snapshots using used plus remaining balance; and
- preservation of application-defined service, asset, and metadata names.

The vectors in [`../spec/conformance.yaml`](../spec/conformance.yaml) are
language-neutral fixtures. A package may expose them through its native test
framework or a separate conformance runner, but the expected decimal values and
error categories must remain unchanged.
