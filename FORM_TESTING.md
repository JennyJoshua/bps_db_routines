# Baimuru Primary School Access Forms — Test Plan

Run all tests in a disposable working copy, never the user's actual database. Record tester, date, working-copy identifier, test data, expected outcome, actual outcome, and evidence. Restore the checkpoint before repeating destructive tests.

## Gate 0 — Backup and inspection

- [ ] Backup was created before any form edit and opens successfully.
- [ ] Source database was not modified.
- [ ] Actual tables, fields, relationships, validation rules, indexes, and queries were inspected and logged.
- [ ] Each form's record source and combo source are confirmed.
- [ ] Any discrepancy with this package was reported and approved before implementation.

## Common tests for every applicable form

- [ ] Opens without Access/VBA errors and has a clear title.
- [ ] New record works; automatic ID is not manually editable.
- [ ] Required fields give a plain-language warning and cannot be saved incomplete when the database requires them.
- [ ] Invalid date/number/controlled selection receives a useful message and the existing validation remains active.
- [ ] Save succeeds for valid data and record can be reopened.
- [ ] Existing record edits save without creating a duplicate.
- [ ] Search finds real records by meaningful criteria and does not require an ID.
- [ ] Foreign-key combos display names and save the correct underlying existing ID.
- [ ] Delete asks for confirmation; cancel leaves the record untouched.
- [ ] Attempting to delete a referenced record is blocked or handled according to the existing relationship, with a clear message.
- [ ] No table, relationship, index, validation rule, or approved query changed during testing.

## Student administration

- [ ] Students: search by student number/name; verify related information is not duplicated into student master data.
- [ ] Parents/guardians: search by name/phone; verify parent/guardian can be linked to more than one student through the link table.
- [ ] Student guardians: create a valid link; attempt duplicate link and confirm existing index/rule protects it; verify records appear through both parent and student contexts if related views are provided.
- [ ] Enrolments: create a valid enrolment; create a later enrolment for the same student without overwriting history; verify current-enrolment source returns intended data.

## Academic and results

- [ ] Classes: teacher combo stores an existing staff key and displays a name; referenced classes cannot be casually deleted.
- [ ] Assessments: create a header with valid class/year/term/period; results remain child/detail records rather than duplicated in the header.
- [ ] Assessment results: selecting assessment displays only confirmed relevant context; class load contains only eligible enrolled students.
- [ ] Assessment results: valid raw score saves; invalid low/high/non-numeric score is rejected by approved rules.
- [ ] Assessment results: percentage is derived correctly from the approved architecture, or is not exposed as editable when derivation is unsupported.
- [ ] Assessment results: duplicate AssessmentID + StudentID + SubjectID attempt is stopped with a clear message if the actual index requires uniqueness.
- [ ] Assessment results: existing results load for edit and bulk save does not overwrite a different student's result.

## Attendance and conduct

- [ ] Attendance: date + class load uses actual enrolments for the correct year/context.
- [ ] Attendance: existing class/date records load for edit, not as a second daily set.
- [ ] Attendance: status list exactly matches approved values; no alternative status system exists.
- [ ] Attendance: mark-all-present (if built) changes only newly loaded blank rows and never overwrites saved records without explicit user action.
- [ ] Attendance: duplicate student/day/event record is prevented by existing design.
- [ ] Conduct categories: existing category records and display order are retained; referenced categories cannot be improperly deleted.
- [ ] Student conduct: save a valid result; attempt the same StudentID + ConductCategoryID + SchoolYear + Term + AssessmentPeriod and confirm friendly duplicate guidance plus final index protection.

## Resources and inventory

- [ ] Facilities and property/equipment: actual condition/status/location combos save existing controlled values; historical referenced records are protected from deletion.
- [ ] Inventory items: item master does not permit uncontrolled editing of a transaction-derived balance.
- [ ] Inventory transactions: valid item, date, type, and positive approved quantity save successfully.
- [ ] Inventory transactions: invalid/future date, invalid type, or invalid quantity is rejected under existing rules.
- [ ] Inventory transactions: any displayed balance agrees with the confirmed existing calculation/query.
- [ ] Inventory transactions: issue exceeding availability is blocked only if this is an existing approved rule; message states available quantity where calculable.
- [ ] Inventory transactions: deletion requires explicit confirmation and warns about history; approved adjustment/reversal is used in preference to silent deletion where available.

## Final regression and handoff

- [ ] Reopen database and each form after compact/repair only if the school explicitly authorises it; verify all existing records still open.
- [ ] Verify counts/sample data in critical tables are unchanged except for intentional test data in the disposable working copy.
- [ ] Re-run the actual approved queries and compare expected results.
- [ ] Export/retain implementation log and test record.
- [ ] Confirm the original database file remains unchanged and deliver only the working copy for review.

