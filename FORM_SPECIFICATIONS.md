# Baimuru Primary School Access Forms — Specifications

Use controls only for fields confirmed in the existing database. All foreign keys use user-friendly combos that store the existing key.

## Student administration

1. **`frmStudents` — `tblStudents`:** Student master form. Locked `txtStudentID`; actual number/code, names, `cboSex`, `txtDateOfBirth`, `chkActive`, and confirmed personal fields. Search by number/name. Related enrolment, attendance, results, and conduct should be related views, not duplicated master data.

2. **`frmParentsGuardians` — `tblParentsGuardians`:** Locked `txtParentGuardianID`; actual name/contact fields; retain confirmed `cboSex`, `cboRelationship`, `chkActive`, `cmdNewParent`, `cmdSave`, `cmdSearch`, `cmdDelete`, `cmdClose`. Search by name/phone. Student connections belong in `tblStudentGuardians`.

3. **`frmStudentGuardians` — `tblStudentGuardians`:** Relationship form with `cboStudent` and `cboParentGuardian`, relationship/status only if fields exist. Detect duplicates under actual indexes. Do not copy master data; support related use from either parent or student form.

4. **`frmStudentEnrolments` — `tblStudentEnrolments`:** Enrolment-history form: existing student, year, class, dates/status only if real fields. New class/year creates history, not overwrites student master data. Use confirmed current-enrolment logic and existing uniqueness rules.

## Staff and academic

5. **`frmStaff` — `tblStaff`:** Locked ID; actual code, name, personal/contact/employment, and active fields. Search by staff number/name. Explain blocked deletes and prefer inactivation where supported.

6. **`frmClasses` — `tblClasses`:** Locked `txtClassID`, name, and actual grade/stream/year/status. `cboTeacher` only for an existing staff FK. Search meaningfully; respect existing uniqueness. Related students come from enrolments/query data.

7. **`frmSubjects` — `tblSubjects`:** Locked ID, existing code/name/description/status. Search by code/name; respect uniqueness; do not delete referenced subjects—use active status if present.

8. **`frmAssessments` — `tblAssessments`:** Assessment header/event, not marks. Actual school year, `cboTerm`, `cboAssessmentPeriod`, `cboClass`, date, remarks. Use approved values. Results are child records in `subfrmAssessmentResults`; detect duplicate headers only if existing design requires it.

9. **`frmAssessmentResults` — `tblAssessmentResults`:** Bulk-entry form: select `cboAssessment` and `cboSubject`; derive header context; load only eligible current-enrolment students using confirmed architecture (potentially `qryStudentsCurrentEnrolment`). Continuous `subfrmAssessmentResults`: student display, `txtRawScore`, `txtPercentage`. Validate approved scores; derive percentage only from approved structure; prevent AssessmentID + StudentID + SubjectID duplicates when actual design requires it; edit existing results rather than duplicate.

## Student monitoring

10. **`frmAttendance` — `tblAttendance`:** Class-based daily entry. Select actual date/class context, then `cmdLoadClass` loads existing enrolments into `subfrmAttendance`. Status list must be existing values; remarks only if real. Load existing class/date records for edit. A mark-all-present action is allowed only if it cannot overwrite saved data. Enforce actual attendance uniqueness.

11. **`frmConductCategories` — `tblConductCategories`:** Small reference form for actual ID, category name, display order, active status. Preserve established categories and display order, including Attendance, Cooperation, Presentation and Grooming, Punctuality, Hygiene, Reliability, Responsibility, Participation, Interactions, and Voluntary School Service. No second category system.

12. **`frmStudentConduct` — `tblStudentConduct`:** Friendly student/category combos and actual year, term, period, result, remarks. Respect the established unique composite index: StudentID + ConductCategoryID + SchoolYear + Term + AssessmentPeriod. Tell users to edit existing records; do not copy category names into results.

## School resources

13. **`frmPropertyEquipment` — `tblPropertyEquipment`:** Durable asset master form. Actual identification, acquisition, condition/status, facility/location FK, and confirmed fields. No parallel facility/inventory system; protect historical assets from casual deletion.

14. **`frmFacilities` — `tblFacilities`:** Actual ID/name/type/description/location/condition/status. Use controlled combos only where approved. Search by real meaningful fields; block deletion of referenced facilities and retain history through status where available.

15. **`frmInventoryItems` — `tblInventoryItems`:** Actual ID/code/name/description/category/unit/status/stock-control fields. Approved combos only. Do not allow uncontrolled editing of transaction-derived stock balance. Block deleting items with transactions; offer read-only history where helpful.

16. **`frmInventoryTransactions` — `tblInventoryTransactions`:** Historical movement form: `cboInventoryItem`, `txtTransactionDate`, `cboTransactionType`, `txtQuantity`, plus real reference/supplier/recipient/purpose/remarks. Use approved types/quantity rules. Display an existing derived balance read-only. Prevent issues beyond available stock only if it is already an approved rule. Search by item/date/type/reference. Confirm deletion and prefer approved adjustments/reversals.
