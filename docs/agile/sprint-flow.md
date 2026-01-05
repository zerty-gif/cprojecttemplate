---
title: "Sprint-in-Phase Delivery Flow"
owner: "Agile Enablement"
last_updated: "2025-01-15"
version: "1.0"
tags: ["agile", "scrum", "gates"]
---

# Sprint-in-phase delivery flow (Scrum cadence + gate review)

Sprint execution happens inside governance phases, with gate reviews validating readiness to advance.

```mermaid
sequenceDiagram
    participant PO as Product Owner
    participant Team as Delivery Team
    participant Gate as Governance Gate

    PO->>Team: Prioritize sprint backlog
    Team->>Team: Sprint planning
    Team->>Team: Daily execution & integration
    Team->>PO: Sprint review + demo
    Team->>Team: Retrospective + improvements
    Team->>Gate: Gate review evidence
    Gate-->>PO: Gate decision + next-phase guidance
```

## Cadence alignment

- **Sprint planning** aligns with phase objectives set during governance gates.
- **Sprint review** provides the evidence required for gate readiness checks.
- **Retrospectives** feed continuous improvements into the next sprint.

## Related documentation

- Governance lifecycle and gates: [Hybrid lifecycle](../governance/lifecycle.md)
