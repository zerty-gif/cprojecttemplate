# Agile Delivery

## Backlog Structure
- **Epics:** High-level outcomes aligned to business goals.
- **Features:** User-facing capabilities grouped under epics.
- **User Stories:** Thin vertical slices delivering value.
- **Tasks:** Implementation units for stories.
- **Defects/Tech Debt:** Tracked with severity and remediation plan.

## Sprint Cadence
- **Sprint length:** 2 weeks (default).
- **Planning:** Day 1 of sprint; commitments based on capacity and velocity.
- **Daily standup:** 15 minutes, focus on blockers.
- **Review/Demo:** End of sprint; showcase completed stories.
- **Retro:** End of sprint; identify improvement actions.

## Definition of Ready (DoR)
A story is ready when:
- Clear user value and acceptance criteria.
- Dependencies identified.
- Estimates agreed.
- Test considerations documented.
- Security and compliance requirements known.

## Definition of Done (DoD)
A story is done when:
- Acceptance criteria met.
- Code reviewed and merged.
- Automated tests pass.
- Security checks executed (SAST/dependency scan minimum).
- Documentation updated (as needed).
- Deployed to the agreed environment.

## Agile Metrics
- **Velocity:** Used for forecasting, not performance management.
- **Cycle time:** Monitor flow efficiency.
- **Defect leakage:** Track escaped defects after release.

## Change Management
- Changes to scope require PO approval.
- Reprioritization happens during backlog refinement or sprint planning.
- Emergency changes follow a documented expedited process.
