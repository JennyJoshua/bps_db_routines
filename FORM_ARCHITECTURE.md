# Baimuru Primary School Access Forms — Architecture

## Scope and protection boundary

This package specifies the forms/UI layer for the existing Baimuru Primary School Microsoft Access database. The existing tables, fields, relationships, referential-integrity settings, indexes, validation rules, and approved queries are locked. Do not add, alter, delete, rename, bypass, recreate, or weaken them without explicit written approval.

Inspect the actual `.accdb` before any form work. Every suggested field, value, query, rule, or control must be confirmed against the approved database; never guess or invent a replacement.

## Design standard

Forms should be consistent and easy for school staff. Display meaningful names rather than IDs; combo boxes store existing foreign-key values. Primary keys are automatic and locked. No form duplicates data owned by another table.

Use: `frm` forms, `subfrm` subforms, `txt` text boxes, `cbo` combos, `chk` check boxes, `cmd` command buttons, and `lbl` labels. Standard actions where useful: `cmdNew`, `cmdSave`, `cmdSearch`, `cmdDelete`, `cmdClose`.

Saving must validate obvious errors, use the existing record source, give plain-language errors, and retain the database constraint as final authority. Deleting requires confirmation, clear referential-integrity handling, and preference for active/inactive status where supported.

## Modules and build order

| Module | Forms |
|---|---|
| Student administration | `frmStudents`, `frmParentsGuardians`, `frmStudentGuardians`, `frmStudentEnrolments` |
| Staff and academic | `frmStaff`, `frmClasses`, `frmSubjects`, `frmAssessments`, `frmAssessmentResults` |
| Student monitoring | `frmAttendance`, `frmConductCategories`, `frmStudentConduct` |
| School resources | `frmPropertyEquipment`, `frmFacilities`, `frmInventoryItems`, `frmInventoryTransactions` |

## Safety workflow

1. Make, open, and verify a timestamped backup.
2. Work only in a separate copy; never edit the user’s production file.
3. Inspect objects: fields/types, keys/indexes, relationships, validation/defaults, lookup sources, queries, existing forms, and VBA.
4. Stop and report conflicts or missing prerequisites. Do not reshape the database.
5. Build and test one module at a time; checkpoint the working copy after each accepted stage.
6. Keep an implementation log showing dependencies, controls, code, tests, issues, and approved deviations.

## Non-negotiable rules

- Use existing lookup/master data; never build parallel lists for terms, statuses, conduct categories, or transaction types.
- Never hard-code score maxima, attendance values, grading, stock rules, or term values unless they exist in the approved design.
- Do not manually maintain a derived percentage or inventory balance.
- Treat assessment results, attendance, conduct, and inventory movements as historical records and protect them from accidental deletion.
