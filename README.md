# bps_db_routines

Specification and runbook package for building the forms layer of the Baimuru Primary School Microsoft Access database.

## Contents

| File | Purpose |
|---|---|
| [FORM_ARCHITECTURE.md](FORM_ARCHITECTURE.md) | Scope, protection boundary and design standard for the forms |
| [FORM_SPECIFICATIONS.md](FORM_SPECIFICATIONS.md) | Specifications for the forms, starting with student administration |
| [CODEX_FORM_BUILD.md](CODEX_FORM_BUILD.md) | Build runbook for the 16 specified forms |
| [FORM_TESTING.md](FORM_TESTING.md) | Test plan with gates |
| BPSMS-2026.accdb | Microsoft Access database file |

## Ground rules stated in the documents

- Existing tables, fields, relationships, indexes, validation rules and approved queries are locked. Do not change them without explicit written approval.
- Build and test only in a backed-up working copy. The package does not authorise changing production data.
- Implementation status is not recorded in this repository.
