# Codex Form Build Runbook

## Scope

Use this runbook to build the 16 specified forms in a **working copy** of the Baimuru Primary School `.accdb`. It does not authorise changing production data or any database structure.

## Before any edit

1. Identify the exact source `.accdb`; do not assume its name or location.
2. Create a timestamped backup beside or in an approved backup location. Open it and verify it is restorable.
3. Create a separate working copy. All editing and testing occurs there.
4. Inventory the working copy: tables and fields/data types; primary keys; indexes (including unique composite indexes); relationships and referential integrity; validation rules/defaults; lookup sources; approved queries; existing forms/reports/macros/VBA; startup settings; and security/permissions.
5. Produce an inspection note mapping every form in this package to the actual record source and dependencies. If a named table, query, field, index, or business rule differs, stop and request a decision. Never manufacture a substitute structure.

## Implementation stages

### Stage 1 — foundation

Build and test `frmStudents`, `frmParentsGuardians`, `frmStudentGuardians`, and `frmStudentEnrolments`. Confirm combo-bound foreign keys, relationship-safe deletion, existing validations, and navigation before continuing.

### Stage 2 — academic masters and assessment header

Build and test `frmStaff`, `frmClasses`, `frmSubjects`, and `frmAssessments`. Confirm any staff/class/subject relationships and assessment header/detail separation.

### Stage 3 — high-risk bulk academic entry

Build `frmAssessmentResults` only after confirming actual result uniqueness, scoring constraints, assessment context, and current-enrolment data source. Load a small test class; ensure percentage derivation, duplicate prevention, and edit-not-duplicate behaviour work.

### Stage 4 — monitoring

Build `frmAttendance`, `frmConductCategories`, and `frmStudentConduct`. Test class-based loading and existing-attendance retrieval before providing a mark-all action. Test the conduct composite index via the form and direct-save error handling.

### Stage 5 — resources

Build `frmPropertyEquipment`, `frmFacilities`, `frmInventoryItems`, and `frmInventoryTransactions`. Inventory transaction work must wait until actual balance calculation and transaction types are understood.

After each stage, create a new dated working-copy checkpoint and complete the relevant test cases in `FORM_TESTING.md`.

## Form construction rules

- Bind a form to the confirmed table/query record source. Do not edit query SQL or table design to make a form easier.
- Show auto-number/primary keys locked, or hide them when they do not help users. Do not prompt users to enter IDs.
- For foreign keys, use a combo with the ID as bound value and human-readable display. Its row source must be a confirmed existing table/query or a safe nonpersistent SQL row source based on approved objects.
- Retain the standard control prefixes. Actual control names may vary to avoid conflicts, but label deviations in the implementation log.
- Use code only for user-facing validation/navigation/error handling. Database constraints remain the final data protection.
- Use transactions/record rollback only where the verified Access/VBA environment supports it safely. Do not leave half-created bulk records.
- Do not suppress errors generically. Handle expected duplicate, validation, and referential-integrity scenarios with precise messages; surface unknown errors with enough detail for the builder while preserving the record.
- Delete only after confirmation. Never cascade-delete through code unless the approved relationship already authorises it and the school specifically approves the operation.

## Required implementation log entry per form

Record: form name; date; working-copy identifier; actual record source; inspected tables/queries/relationships/indexes; bound controls; combo row sources and bound columns; validation/error behaviour; code modules/procedures changed; tests and outcomes; known limitations; approver for deviations.

## Acceptance and handoff

Do not replace the source database. Deliver the tested working copy separately, the implementation log, a list of forms built, tests passed/failed, backup locations, and unresolved decisions. The school decides whether and when to promote the working copy.

## Stop conditions requiring user approval

Stop rather than improvise if: required fields are missing; a named query/table is absent or different; a form conflicts with a validation/index/relationship; an invented lookup list seems necessary; score/balance/attendance logic is unclear; a persistent VBA/security setting must change; creating a form requires changing a locked object; or a bulk operation could alter existing historical records.

