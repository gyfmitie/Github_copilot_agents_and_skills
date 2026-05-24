---
name: testing-strategy
description: Define balanced, high-value testing coverage for Python tools and services.
argument-hint: [component] [risk profile] [critical paths]
---

# Testing Strategy

## Recommended default baseline

- Unit tests for domain logic and utilities.
- Integration tests for core external boundaries.
- One smoke end-to-end test per primary entrypoint.

## When to add property tests

Add property-based tests for:

- Parsers and serializers
- Data transformation pipelines
- Validation and rule engines

## Output format

- Coverage priorities
- Unit/integration/smoke test matrix
- Property-test candidates
- Test data strategy
- Gate recommendations
