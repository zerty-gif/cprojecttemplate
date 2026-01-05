# Gates and Entry/Exit Criteria

## Overview
Gates are formal checkpoints to verify readiness, manage risk, and confirm evidence before moving to the next phase.

## Gate Definitions

### G0: Discovery Gate
**Entry Criteria**
- Identified stakeholders and problem statement.
- Initial high-level solution hypothesis.

**Exit Criteria**
- Validated business objectives and success metrics.
- Feasibility assessment complete (technical + operational).
- Initial risk register created.

**Required Evidence**
- Problem statement.
- Stakeholder map.
- Feasibility notes.

### G1: Definition Gate
**Entry Criteria**
- Approved problem statement and initial feasibility.
- High-level backlog created.

**Exit Criteria**
- Defined scope, MVP definition, and roadmap.
- Resourcing and budget confirmed.
- Architecture direction and key decisions documented.

**Required Evidence**
- Scope statement.
- High-level architecture diagram.
- Roadmap and release plan.

### G2: Build Gate
**Entry Criteria**
- Approved scope and architecture direction.
- Engineering plan and sprint cadence established.

**Exit Criteria**
- Build environment ready.
- CI/CD pipeline established.
- Test plan and quality gates defined.

**Required Evidence**
- CI/CD pipeline configuration.
- Test strategy and quality gates.
- Updated risk register.

### G3: Validate Gate
**Entry Criteria**
- Feature-complete build for the release scope.
- Test execution underway.

**Exit Criteria**
- Quality targets met (pass rate, coverage where applicable).
- Security validations complete (SAST/DAST/dependency scan).
- Operational readiness checklist complete.

**Required Evidence**
- Test summary report.
- Security scan results and remediations.
- Operational readiness checklist.

### G4: Release Gate
**Entry Criteria**
- G3 passed.
- Release candidate approved.

**Exit Criteria**
- Go/No-Go approved.
- Release notes and rollback plan complete.

**Required Evidence**
- Go/No-Go decision record.
- Release notes.
- Rollback and monitoring plan.

## Gate Review Logistics
- **Participants:** PO, DL, EL, QL, SecL, SC representative.
- **Outcome:** Go, Conditional Go (with timeboxed actions), or No-Go.
- **Record:** Decision log updated within 24 hours.
