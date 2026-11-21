
# Feature 7 — Project Time Approval

## 1. Header

**Feature Name:** Project Time Approval

**Feature ID:** FEAT-007

**Description:** This feature allows project managers to review project time entries submitted by employees and either approve or deny them. Approved time entries become available for invoice generation, while denied entries are excluded.

**Primary Users:** Project Managers

**Supporting Users:** Employees and Admin/Owner

## 2. User Stories

- As a project manager, I want to view submitted time entries for my projects so that I can review the hours employees have worked.
- As a project manager, I want to see the employee, project, role, date, and hours for each entry so that I can understand what work was recorded.
- As a project manager, I want to approve valid time entries so that approved hours can be used for invoicing.
- As a project manager, I want to deny incorrect time entries so that inaccurate hours are not included in invoices.
- As a project manager, I want to provide a reason when denying time so that employees understand what needs to be corrected.
- As an employee, I want to see whether my time entries were approved or denied so that I know their current status.
- As an employee, I want to see the reason for a denied entry so that I can correct and resubmit it when appropriate.
- As an admin/owner, I want to view time approval records so that I can monitor the approval process and maintain accurate company records.

## 3. Functional Requirements

1. The system shall allow project managers to view submitted time entries for projects they manage.
2. The system shall display only time entries with a Pending Approval status in the pending approval list.
3. The system shall display the employee name, project name, project role, work date, hours, and work description for each time entry.
4. The system shall allow a project manager to open an individual time entry and review its details.
5. The system shall allow a project manager to approve a pending time entry.
6. The system shall allow a project manager to deny a pending time entry.
7. The system shall require a denial reason before a time entry can be denied.
8. The system shall change the status to Approved when a manager approves an entry.
9. The system shall change the status to Denied when a manager denies an entry.
10. The system shall record the date and time of each approval decision.
11. The system shall record the employee or manager account responsible for the decision.
12. The system shall prevent users without the required permissions from approving or denying time entries.
13. The system shall prevent a project manager from approving or denying time entries for projects they do not manage, unless they have additional authorized permissions.
14. The system shall prevent an already approved or denied entry from being approved or denied again through the normal approval process.
15. The system shall allow employees to view the approval status of their own time entries.
16. The system shall display the denial reason to the employee when an entry is denied.
17. The system shall allow a denied entry to be corrected and resubmitted according to the time-entry correction process.
18. The system shall preserve the original decision history when a denied entry is corrected and resubmitted.
19. The system shall make approved time entries available to the Invoice Generation feature.
20. The system shall prevent Pending Approval and Denied time entries from being included in invoice service line items.
21. The system shall preserve approved time records so that accounting history is not changed without an authorized correction process.

## 4. Assumptions

- Employees submit time entries through the Project Time Entry feature.
- New time entries receive a Pending Approval status.
- Each project has an assigned project manager responsible for reviewing its time entries.
- Project managers can only approve or deny entries for projects they manage unless given additional permissions.
- A project manager reviews the employee's submitted hours and work description before making a decision.
- A denial reason is required when an entry is denied.
- Employees can view the results of the approval process.
- Denied entries may be corrected and resubmitted.
- Approval decisions must be recorded for future reference.
- Only Approved time entries can be used for invoice generation.
- This feature does not calculate payroll or pay employees.

## 5. Edge Cases

- A project manager tries to approve a time entry that has already been approved.
- A project manager tries to approve or deny an entry for a project they do not manage.
- A project manager tries to deny an entry without providing a reason.
- An employee tries to approve or deny their own time entry without the required permissions.
- A time entry is submitted while the project manager is reviewing another entry.
- An employee's project assignment is no longer active when the manager reviews the entry.
- A project manager tries to review an entry that has already been denied.
- A project manager accidentally selects the wrong time entry.
- A manager loses access or their session expires while reviewing an entry.
- An employee tries to edit an approved time entry.
- A denied time entry is corrected and resubmitted.
- A project has no assigned project manager available to review time.
- An invoice is being prepared while time entries are still pending approval.

## 6. Success Criteria

- Project managers can view submitted time entries for their projects.
- Managers can open and review the details of each entry.
- Managers can approve valid time entries.
- Managers can deny incorrect time entries.
- The system requires a reason when denying an entry.
- The system correctly updates the approval status.
- The system records who made each decision and when.
- Employees can view the status and denial reason for their own entries.
- Approved time entries are available for invoice generation.
- Pending and denied entries are excluded from invoice generation.
- Approval history is preserved for accurate recordkeeping.

## 7. Key Entities

- **Project Time:** Stores the employee's submitted hours and current approval status.
- **Project Role Assignment:** Connects the time entry to the employee, project, and role.
- **Employee:** The person who submitted the time entry.
- **Project:** The project where the work was completed.
- **Project Manager:** The person responsible for reviewing project time.
- **Time Approval Record:** Stores the decision, reviewer, date, and any denial reason.

## 8. Initial Data Model

### Project Time

- ProjectTimeID (Primary Key)
- ProjectRoleAssignmentID (Foreign Key)
- WorkDate
- Hours
- Description
- Status
- SubmittedDate

### Time Approval Record

- ApprovalRecordID (Primary Key)
- ProjectTimeID (Foreign Key)
- ReviewedByEmployeeID (Foreign Key)
- Decision
- DecisionDate
- DenialReason

### Relationships

- One Project Time entry can have multiple approval records if it is denied, corrected, and resubmitted.
- Each approval record belongs to one Project Time entry.
- Each approval record is connected to the employee or manager account that made the decision.
- The Project Time entry is connected to a Project Role Assignment.
- The Project Role Assignment identifies the employee, project, and project role.
- The latest approval decision determines the current approval status of the time entry.

### Status Values

- Pending Approval
- Approved
- Denied

### Decision Values

- Approved
- Denied

## 9. Gherkin AC

### Scenario 1: Approve a valid time entry

**Given** a project manager is logged in

**And** an employee has submitted a time entry with a Pending Approval status

**And** the time entry belongs to a project managed by that manager

**When** the manager reviews the entry and selects Approve

**Then** the system shall change the status to Approved

**And** record the manager and decision date

**And** make the approved time available for invoice generation.

### Scenario 2: Deny a time entry with a reason

**Given** a project manager is reviewing a pending time entry

**When** the manager selects Deny and enters a reason

**Then** the system shall change the status to Denied

**And** save the denial reason

**And** record the manager and decision date.

### Scenario 3: Require a denial reason

**Given** a project manager is reviewing a pending time entry

**When** the manager selects Deny without entering a reason

**Then** the system shall prevent the denial

**And** display a message asking the manager to provide a reason.

### Scenario 4: Prevent unauthorized approval

**Given** a project manager is logged in

**And** a time entry belongs to a project they do not manage

**When** the manager tries to approve or deny that entry

**Then** the system shall reject the action

**And** display an authorization message.

### Scenario 5: Prevent duplicate approval decisions

**Given** a time entry already has an Approved status

**When** a manager tries to approve or deny the same entry through the normal approval process

**Then** the system shall prevent the duplicate decision

**And** display the current status of the entry.

### Scenario 6: Employee views an approved time entry

**Given** an employee has submitted a time entry

**And** the project manager has approved it

**When** the employee opens My Time Entries

**Then** the system shall display the entry with an Approved status.

### Scenario 7: Employee views a denied time entry

**Given** an employee has submitted a time entry

**And** the project manager has denied it with a reason

**When** the employee opens My Time Entries

**Then** the system shall display the entry with a Denied status

**And** show the reason provided by the manager.

### Scenario 8: Denied time is corrected and resubmitted

**Given** an employee has a denied time entry

**And** the manager has provided a reason for the denial

**When** the employee corrects the entry and resubmits it according to the correction process

**Then** the system shall create a new pending approval decision

**And** preserve the original denial reason and decision history.

### Scenario 9: Exclude pending and denied time from invoicing

**Given** a project has time entries with Pending Approval, Approved, and Denied statuses

**When** the Invoice Generation feature retrieves project time

**Then** the system shall provide only Approved time entries

**And** exclude Pending Approval and Denied entries.

## 10. Data Ownership

- **Time Approval** owns the review and approval process for project time entries.
- **Time Approval** owns approval decisions, reviewer information, decision dates, and denial reasons.
- **Project Time Entry** owns the creation and submission of project time records.
- **Project Maintenance** owns project and project manager assignment information.
- **Employee Maintenance** owns employee information and account details.
- **Invoice Generation** reads approved time entries to create invoice service line items.
- Time Approval shall not create invoices or change agreed project role rates.

## 11. API Requirements

- `GET /api/time-approval/pending` — Retrieve pending time entries for projects managed by the logged-in project manager.
- `GET /api/time-approval/{id}` — Retrieve the details of a specific time entry.
- `POST /api/time-approval/{id}/approve` — Approve a pending time entry.
- `POST /api/time-approval/{id}/deny` — Deny a pending time entry and save the denial reason.
- `GET /api/time-approval/history/{id}` — Retrieve the approval history for a time entry.
- `GET /api/time-approval/my-decisions` — Retrieve approval decisions made by the logged-in project manager.

The API shall verify the manager's permissions before allowing an approval decision. It shall also prevent duplicate decisions and require a denial reason when denying an entry.

## 12. Screen Requirements

### A. Pending Time Approval Screen

- Display all pending time entries for projects managed by the logged-in project manager.
- Show employee name, project, role, work date, hours, and submission date.
- Allow managers to filter entries by project, employee, or date.
- Allow managers to open an entry for review.
- Display the number of pending entries.

### B. Review Time Entry Screen

- Display the full details of a selected time entry.
- Show the employee, project, role, work date, hours, and work description.
- Display the agreed project role rate for reference.
- Provide Approve and Deny actions.
- Require a denial reason when the manager chooses Deny.
- Display a confirmation message after a successful decision.

### C. Approval History Screen

- Display previous approval decisions.
- Show the time entry, decision, reviewer, date, and denial reason when applicable.
- Allow authorized users to view past decisions.
- Preserve previous decisions when an entry is corrected and resubmitted.

### D. Employee Time Status Screen

- Allow employees to view the approval status of their own time entries.
- Display denial reasons when entries are denied.
- Provide access to the correction and resubmission process for denied entries.

## 13. Definition of Done

- Project managers can view pending time entries for their projects.
- Managers can review the full details of submitted time.
- Managers can approve pending time entries.
- Managers can deny pending time entries with a required reason.
- The system records the manager and decision date.
- Unauthorized users cannot approve or deny time.
- The system prevents duplicate approval decisions.
- Employees can view their time entry statuses.
- Employees can view denial reasons.
- Approval history is preserved.
- Approved time entries are available to Invoice Generation.
- Pending and denied time entries are excluded from invoice generation.
- All required validation and Gherkin acceptance scenarios pass.

## 14. Out of Scope

- Creating or editing employee accounts.
- Creating or editing projects.
- Creating or editing project roles and assignments.
- Entering new project time.
- Calculating employee payroll or salaries.
- Tracking employee attendance.
- Generating invoice line items.
- Creating, approving, or sending invoices.
- Processing customer payments.
- Changing agreed project role rates.
- Changing approved time entries without an authorized correction process.
