# Development Tasks \| Requirements \| Status

ERP development tasks in the original source sequence. Each task retains its context, requirements and status; later updates remain after earlier tasks.

## 1. Role permission framework

### Requirement

- Super Admin has access to all modules and features.

- Admin has access except Wage Access, User Access, Report Copy, Merge and Repo Access.

- Admin Fee follows Admin access and additionally has the Admin Fee Report section.

- Regional Manager initially followed Manager access, with multi-center assignment controlled by Super Admin.

- Manager access was initially limited to assigned centers.

- Maintain module-wise and user-specific permissions; confirm any changes against the current Admin Assistant implementation.

**Status: Done**

## 2. Center Management

### Requirement

- Create, view, update and delete center records and manage the document gallery.

- Original permission: Admin/Super Admin full access, Manager view only; current Admin Assistant may supersede this in ERP.

- Add delete option to the edit-document section.

- Rename CRC PAYROLL to CRC ID and CRC BUSINESS NO to Business No.

- Review duplicate Vancouver and Chef’s Corner center entries.

- Add center filtering by region (requires discussion).

**Status: Done**

## 3. Class / Classroom Management

### Requirement

- Create, view, update and delete classes and class documents.

- Original Manager access was view-only; Admin Assistant should permit editing for assigned centers.

- Allow classroom name and detail changes.

- Separate document gallery into Minor incidence and Major incidence sections.

**Status: Done**

## 4. Fee Master

### Requirement

- Create, view, update and delete fee schedules.

- ERP Fee Master access has been enabled for all user types only in the ERP setup.

- Documentation and video tutorial, pagination, sorting, search and UI improvements were added.

- Investigate and correct the reported fee name issue.

**Status: Done**

## 5. Child Master core records

### Requirement

- Create, view, update and delete child profiles per center.

- Show Created Date and Created By on child details.

- Add DOB as a separate child-list column while keeping Age in Months.

- Add search by child name, parent name and status, age ascending/descending sorting.

- Investigate the Create Child dropdown, fee schedule, attendance-day selection and banking required-field indicators.

- Correct the duplicate letter in the Enter Home Address label.

**Status: Done**

## 6. Child lifecycle and notification rules

### Requirement

- Original lifecycle: Review → Active → Withdrawal → Archive, with Manager actions requiring Admin approval.

- Record withdrawal date and notes. Historical specifications describe automatic archiving after withdrawal date, with an inconsistent note about monthly cron timing; confirm exact schedule.

- Notify relevant Admin, Super Admin and Manager users about create, approve, withdrawal and delete events.

- ERP Admin Assistant permission removes secondary approval for authorized managers.

**Status: Done**

## 7. Child Waiting List

### Requirement

- Create, view, update and delete child waiting-list entries per center.

- Original baseline grants Admin and Super Admin full access.

**Status: Done**

## 8. Fee Reports core features

### Requirement

- Create fresh reports by date range and center/class.

- Copy reports and modify parameters; merge multiple reports.

- List reports with date and center filters.

- Admin Fee Report provides financial overview for authorized users.

- Retain historical roles: Super Admin full access; Admin/Manager list/create fields as specified in source.

**Status: Done**

## 9. Employee Master and waiting list

### Requirement

- Create, view, update and delete employee profiles; baseline Admin/Super Admin full access and Manager view-only.

- Employee status: Active by default, Resigned when resignation date is added, Archive on last working date.

- Support employee waiting list and Super Admin transfer to Employee list via Edit page.

- Improve Employee Master UI/UX and ensure dashboard employee counts link to employee pages.

**Status: Done**

## 10. Wage Reports

### Requirement

- Provide monthly employee wage report and report listing; historical Super Admin full access.

- Validate employee status before generation.

- Retest after Employee Master changes and confirm updates are reflected.

- In monthly Admin wage report, center changes must not affect other modules.

- Employee and center dropdowns should show all employees, All Centers and each center including Cocomelon and Wonderful.

- Improve report UI.

**Status: Done**

## 11. System audit, login logs and deletion

### Requirement

- Use soft delete for all delete operations.

- Record created by, updated by, created/updated timestamps and status history.

- Maintain login/logout and module access logs with user/date filtering.

- System Login Logs were previously implemented for Super Admin; expanded Admin log visibility was also requested.

**Status: Done**

## 12. Dashboard summary and activity

### Requirement

- Show pending tasks/reports, attendance summary, fee-pending child alerts and activity timeline.

- Show employee monthly summaries and quick links for joiners, probation, last working day and document expiry.

**Status: Done**

## 13. Task Management and timeline

### Requirement

- Super Admin can create, assign, edit and delete tasks with due date/time, assignee, updates and notes.

- Users can update task status and add threaded notes; Managers see overdue/pending/completed tasks.

- Support recurring tasks, activity timeline and email reminder one day before due date.

- Support center-specific Manager email addresses.

- Investigate missing Pooja assignment and mandatory center selection.

**Status: Done**

## 14. Regional Manager and user assignment

### Requirement

- Allow Regional Manager to manage multiple centers under one login.

- Start configuration with Melissa’s setup.

- In Task Management, investigate why Pooja is absent from the assignment dropdown.

- Consider allowing assignment directly to users without requiring a center selection.

**Status: Done**

## 15. Report status, merge and organization

### Requirement

- Use the same Excel layout in merged reports as Fee Reports.

- Match New, Existing and Withdrawal categories in report creation and listing.

- Group reports by folders/tags, including nested year/month folders.

- Add Finalize action for report rows to organize them.

- Include Created By and allow report archiving into a separate archive area.

**Status: Done**

## 16. Accounting (ACCB)

### Requirement

- Export PDF data to CSV.

- Allow direct upload into each report.

- Add automatic counting functionality.

**Status: Done**

## 17. Employee onboarding, login and approval

### Requirement

- Document account creation, existing/new employee login, activation, forgot-password, password reset and re-login.

- Proposed employee profile approval: employee creates, Manager reviews and Manager approves; confirm before implementation.

- Employee account documentation, login guidance and secure internal document storage were previously added.

**Status: Done**

## 18. Portal interface and responsive design

### Requirement

- Remove unnecessary top bar, particularly on child file screens.

- Make Center, Child, Employee and Timeline modules responsive, and extend mobile-friendly design across the system.

- Improve Employee Master and Wage Report layouts.

- Use DataTables features on listing pages: search, sort, pagination, applicable export and up to 100 rows per page.

**Status: Done**

## 19. Expiry and missing-document reminders

### Requirement

- Notify about upcoming expiry with document name, expiry date and days remaining.

- Email reminders for upcoming expiry and missing/pending documents.

- Stop upcoming-expiry reminders after the document expiry date has passed.

- Provide monthly employee summaries on the first day: joiners, probation completions, last working days, expired documents and upcoming events.

**Status: Done**

## 20. New / Existing status and banking verification

### Requirement

- Classify a child as New for 15 days after Admission Date, then Existing; withdrawn children show Withdrawal.

- Use report month-end date when calculating fee report status.

- This logic does not check whether a child was added to the banking system.

- Arthur (Sep 21 admission) and Kinsley (Sep 15 admission) both showed New in the Sep 29 report, consistent with the documented logic.

- Monitor the next 2–3 fee reports and discuss changes only if the issue recurs.

**Status: Done**

## 21. Dashboard child review

### Requirement

- Provide dashboard Review Children action with Approve, Reject, Edit and Send Back.

- Follow the applicable child approval workflow for the user’s role.

- Make Active Child and Review Child counts and child names clickable, linking to the appropriate child page.

- Ensure Status buttons work correctly.

**Status: Done**

## 22. Employee wage increase and expiry fields

### Requirement

- Capture wage increase amount and effective date where required.

- Another later note proposes removing Wage Increase Amount if no longer required; resolve this conflict.

- Correct document expiry date calculations to match ECE behavior.

**Status: Done**

## 23. Admin Assistant access for ERP

Context: Chelsea requested broader operational permissions than the earlier Manager role permitted.

### Requirement

- Create and assign Admin Assistant role to Managers and Regional Managers.

- Managers receive Super Admin-level functional access only for their assigned center; Regional Managers only for their assigned centers.

- Permit document, licensing officer, facility, classroom and child management without secondary approval within authorized centers.

- Prevent access to unassigned centers.

**Status: Done**

## 24. Child approval workflow changes

### Requirement

- Historical workflow: Manager-created children enter Review; Admin/Super Admin approval activates them; withdrawal requests require approval.

- ERP change: authorized Admin Assistants can create, edit, withdraw, remove and delete children without secondary approval.

- Retain and clarify audit history and notifications as appropriate for the revised workflow.

**Status: Done**

## 25. Day-wise child totals

### Requirement

- Show totals for each day in the Child Master listing based on applicable scheduled attendance days.

- Implement the same day-wise counting behavior already present in Magenta.

**Status: Done**

## 26. Exclude archived children from day-wise totals

### Requirement

- Exclude archived children from daily counts.

- Recalculate day-wise totals when a child is archived.

- Match Magenta behavior.

**Status: Done**

## 27. Outstanding ERP tasks and communication

### Requirement

- Review Chelsea’s reported issues and confirm permissions and remaining fixes.

- Provide one support email address for system testers to submit issues and receive replies.

- Review Melissa’s additional software requests before implementation.

- Prepare response to Chelsea summarizing fixes, outstanding items and next actions.

**Status: Done**

## 28. Add Incident Reports Section to Next Level Portal

### Requirement

- Add a dedicated Incident Reports section to the Next Level portal.

- Confirm the section location, required report fields, report structure, user permissions, and workflow for creating, viewing, and managing incident reports.

**Status: Needs Discussion**

## 29. Employee document uploads and labels

### Requirement

- Allow multiple files in the same document category without replacing prior files.

- Support at least three reference letters.

- Permit authorized staff to manage multiple Criminal Record Check files and other repeated categories.

- Investigate single-file upload restrictions and missing document labels.

**Status: Pending – Development / Fix**

## 30. Soojin Song employee upload issue

### Requirement

- Soojin Song could not upload files through employee portal and sent them to Jasmeet.

- Documents were manually uploaded to her Wonderful Beginnings Employee Master profile.

- Four unmatched-label documents were placed under Other Documents.

- Investigate portal upload failures and missing labels to prevent recurrence.

**Status: Manual upload done; root-cause review pending**

## 31. Employee PDF merge and document notifications

### Requirement

- Merge all current employee PDFs into one printable/downloadable PDF.

- Notify assigned Manager when employees upload or update documents.

- Allow replacement of outdated files and include latest versions in merged PDF.

- Managers can print revised documents for physical staff files.

**Status: Pending – Development Required**

## 32. OCR child admission form

### Requirement

- Allow Manager to upload registration/admission PDF or image in Add Child flow.

- Extract child, parent, admission and relevant form details and populate matching fields.

- Require Manager review and correction before saving.

**Status: Pending – Development Required**

## 33. Children’s Enrollment Summary Report

### Requirement

- Create report by Center → Program → Age, showing child counts.

- Include Before & After School and KG / Grade 1–12 category selection.

- Highlight weekends and holidays in Excel and exclude holidays from counted days.

- Provide report listing with view/download.

- Use client-provided report template and obtain holiday list before finalizing calculations.

**Status: Pending – Development; template and holiday list needed**

## 34. Yearly Child Income Tax Report

### Requirement

- Create Yearly Child Income Tax Report page.

- Allow Managers to upload 12 monthly Child Fee Reports and consolidate child-wise annual totals.

- Export annual report to Excel.

- List previously generated annual reports for download.

**Status: Pending – Development Required**

## 35. New payroll and invoice management module

### Requirement

- Build a Payroll Management module integrated with Employee Master.

- Manage payroll, salaries, wage calculations, payroll reports and related invoices.

- Use relevant employee, attendance and wage information and enforce role-based access.

- Discuss payroll rules, invoice formats, approvals and permissions with the concerned person before development.

**Status: Pending – Discussion Required Before Development**

# Discussion Points – Clarifications Required

The following questions and technical points need to be discussed or confirmed. These are not marked as completed.

- **Manager Email Address:** Request and confirm the manager’s email address for portal notifications and relevant communication.

> **Status: Pending – Discussion / Confirmation Required**

- **Holiday List for Children’s Enrollment Summary:** Obtain the holiday list in Excel format for the Children’s Enrollment Summary Report. Confirm the applicable centers and dates so holidays can be highlighted and excluded from report calculations.

> **Status: Pending – Discussion / Confirmation Required**

- **Soojin Song – Manually Uploaded Documents:** Soojin Song’s employee documents were manually uploaded under Wonderful Beginnings after portal upload issues. Confirm whether all documents are correctly uploaded and categorized, including documents placed under Other Documents, and check whether the upload issue still needs to be fixed.

> **Status: Pending – Discussion / Confirmation Required**

- **Multiple Staff Document Uploads – Wonderful Beginnings and Cocomelon:** Confirm whether the same multiple-document upload functionality is required in both Wonderful Beginnings and Cocomelon, allowing multiple staff documents in the same document category without replacing existing files.

> **Status: Pending – Discussion / Confirmation Required**

- **Email Summary Recipients – Confirmation:** Please confirm whether the Next Level setup email summary should go to Melissa@educatorsoncall.ca and whether the other summary should go to Accounting@cocomelonlearning.com. Clarify which summary belongs to each recipient before configuring email delivery.

> **Status: Pending – Discussion / Confirmation Required**

- **Children’s Enrollment Summary – Manual Editing:** Add or confirm an option to manually edit generated Children’s Enrollment Summary Reports, similar to the editing option available in Fee Reports. Confirm which fields may be edited and whether edited values should be saved.

> **Status: Pending – Discussion / Confirmation Required**

- **Children’s Enrollment Summary – Merge Reports:** Add or confirm a report merge option to combine selected Children’s Enrollment Summary Reports. Discuss report selection, merge logic, and expected export format.

> **Status: Pending – Discussion / Confirmation Required**

- **Children’s Enrollment Summary – Technical Clarifications:** Technical questions about the Children’s Enrollment Summary Report remain unresolved, including report calculations, holiday exclusions, manual editing, and merging. Discuss these with Sir before finalizing the implementation.

> **Status: Pending – Discussion / Confirmation Required**

- **Current Testing – Melissa’s System:** Melissa’s system testing is currently in progress. Review testing findings and outstanding questions before confirming the final requirements or development status.

> **Status: Pending – Discussion / Confirmation Required**
