---
title: "Hybrid Lifecycle (Phases + Gates)"
owner: "PMO"
last_updated: "2025-01-15"
version: "1.0"
tags: ["governance", "lifecycle", "gates"]
---

# Hybrid lifecycle (phases + gates)

The delivery lifecycle blends iterative execution with formal gate reviews. Each phase can host multiple sprints, but a gate review determines readiness to proceed.

```mermaid
flowchart LR
    A[Discover Phase] -->|Gate 0: Vision| B[Define Phase]
    B -->|Gate 1: Scope| C[Build Phase]
    C -->|Gate 2: Release Readiness| D[Validate Phase]
    D -->|Gate 3: Operations Readiness| E[Operate Phase]

    subgraph Governance Gates
        G0[Gate 0: Vision]
        G1[Gate 1: Scope]
        G2[Gate 2: Release Readiness]
        G3[Gate 3: Operations Readiness]
    end

    A -.-> G0
    B -.-> G1
    C -.-> G2
    D -.-> G3
```

## Gate criteria checklist

- **Gate 0: Vision**: problem statement, stakeholder alignment, and funding authorization.
- **Gate 1: Scope**: roadmap, risk register, and dependency validation.
- **Gate 2: Release Readiness**: feature completion, security validation, and compliance sign-off.
- **Gate 3: Operations Readiness**: runbooks, monitoring, and support readiness.

## Related flow

The Scrum cadence inside each phase is documented in [Sprint-in-phase delivery flow](../agile/sprint-flow.md).
