
# Feature 6 — Project Time Entry

## 1. Header

**Feature Name:** Project Time Entry

**Feature ID:** FEAT-006

**Description:** This feature allows employees to enter and submit the hours they worked on assigned projects. Each time entry is connected to a Project Role Assignment so the system can identify the employee, project, role, and agreed billing rate.

**Primary Users:** Employees

**Supporting Users:** Project Managers and Admin/Owner

## 2. User Stories

- As an employee, I want to enter the hours I worked so that my work can be recorded for the correct project.
- As an employee, I want to select from my assigned projects and roles so that I only enter time for work assigned to me.
- As an employee, I want to add a date and description to my time entry so that the work I completed is clear.
- As an employee, I want to view my submitted time entries so that I can check the hours I have recorded.
- As an employee, I want to see whether my time is pending, approved, or denied so that I know its current status.
- As a project manager, I want to view time submitted for my projects so that I can review it through the time approval process.
- As an admin/owner, I want time entries to be connected to project assignments so that the correct project and billing rate can be identified.

## 3. Functional Requirements

1. The system shall allow an employee to create a new project time entry.
2. The system shall display the projects and project roles assigned to the logged-in employee.
3. The employee shall select a valid Project Role Assignment before entering time.
4. The system shall automatically identify the employee, project, and role using the selected Project Role Assignment ID.
5. The system shall allow the employee to enter the date the work was completed.
6. The system shall allow the employee to enter the number of hours worked.
7. The system shall allow the employee to add an optional description of the work completed.
8. The system shall verify that the selected Project Role Assignment belongs to the logged-in employee.
9. The system shall only allow time to be entered for projects with an Active status.
10. The system shall verify that the number of hours entered is greater than zero.
11. The system shall verify that the work date is valid and is not a future date.
12. The system shall save each submitted time entry with a Pending Approval status.
13. The system shall display a confirmation message after a time entry is successfully submitted.
14. The system shall allow employees to view their own time entries.
15. The system shall display the date, project, role, hours, description, and approval status for each entry.
16. The system shall allow employees to view the total hours they have entered for a selected period.
17. The system shall prevent employees from changing entries that have already been approved. Corrections to approved time must follow an authorized correction process.
18. The system shall keep separate time entries when an employee works on different projects or assignments on the same date.
19. The system shall make approved time entries available to the invoice generation process.
20. The system shall not include pending or denied time entries when generating invoice service line items.

## 4. Assumptions

- Employees must have an active account to enter project time.
- Employees must already be assigned to a project role before they can enter time for that assignment.
- Projects must have an Active status before employees can submit time.
- Time is entered as a number of hours worked, not as clock-in and clock-out times.
- Employees enter time after completing the work.
- A time entry is connected to one Project Role Assignment.
- The Project Role Assignment identifies the employee, project, and role.
- The agreed rate is maintained in Project Maintenance and is not manually entered by the employee.
- The system uses Pending Approval as the initial status after submission.
- Project managers are responsible for reviewing submitted time through a separate approval feature.
- Only approved time can be used to create invoice service line items.

## 5. Edge Cases

- An employee tries to enter time without a project role assignment.
- An employee tries to enter time for a project that is Pending or Closed.
- An employee selects an assignment that belongs to another employee.
- An employee enters zero or a negative number of hours.
- An employee enters a future work date.
- An employee leaves the date or hours field empty.
- An employee submits time without selecting a project role assignment.
- An employee submits the same work information more than once by mistake.
- An employee attempts to change an entry that has already been approved.
- A project role assignment is no longer active when the employee tries to submit time.
- An employee has multiple assignments on the same project and must select the correct role.
- An employee works on different projects on the same date and needs to submit separate entries.

## 6. Success Criteria

- Employees can successfully enter and submit project time.
- Employees can only submit time for their own project role assignments.
- The system prevents time entry for Pending and Closed projects.
- Each time entry is connected to the correct employee, project, and role.
- The system correctly saves the work date and number of hours.
- Employees can view their submitted time entries and their current statuses.
- Submitted time entries receive a Pending Approval status.
- Approved time is available for invoice generation.
- Pending and denied time is excluded from invoice generation.
- The system keeps accurate records of submitted time.

## 7. Key Entities

- **Project Time:** Stores the hours an employee worked on a project.
- **Project Role Assignment:** Connects an employee to a specific project role.
- **Employee:** The person who enters the project time.
- **Project:** The project where the work was completed.
- **Project Role:** The role performed by the employee on the project and its agreed billing rate.

## 8. Initial Data Model

### Project Time

- ProjectTimeID (Primary Key)
- ProjectRoleAssignmentID (Foreign Key)
- WorkDate
- Hours
- Description
- Status
- SubmittedDate

### Project Role Assignment

- ProjectRoleAssignmentID (Primary Key)
- ProjectRoleID (Foreign Key)
- EmployeeID (Foreign Key)

### Relationships

- One Project Role Assignment can have many Project Time entries.
- Each Project Time entry belongs to one Project Role Assignment.
- One employee can have many Project Role Assignments.
- One Project Role can have many Project Role Assignments.
- The Project Role Assignment identifies the project and role associated with each time entry.
- The Project Time record does not need a separate EmployeeID or ProjectID because those details can be identified through Project Role Assignment.

### Status Values

- Pending Approval
- Approved
- Denied

## 9. Gherkin AC

### Scenario 1: Successfully submit project time

**Given** an employee is logged in and has an active project role assignment

**And** the project has an Active status

**When** the employee selects the assignment, enters a valid date and hours, and submits the time entry

**Then** the system shall save the time entry

**And** the time entry shall receive a Pending Approval status

**And** the system shall display a confirmation message.

### Scenario 2: Prevent time entry for a closed project

**Given** an employee is assigned to a project

**And** the project has a Closed status

**When** the employee tries to enter time for that project

**Then** the system shall prevent the time entry

**And** display a message explaining that time cannot be entered for a closed project.

### Scenario 3: Prevent time entry for a pending project

**Given** an employee is assigned to a project

**And** the project has a Pending status

**When** the employee tries to submit time

**Then** the system shall prevent the submission

**And** display a message explaining that the project must be Active before time can be entered.

### Scenario 4: Prevent invalid hours

**Given** an employee is entering project time

**When** the employee enters zero or a negative number of hours

**Then** the system shall reject the time entry

**And** display a message asking the employee to enter a valid number of hours.

### Scenario 5: Prevent future work dates

**Given** an employee is entering project time

**When** the employee selects a future date

**Then** the system shall reject the entry

**And** display a message explaining that future work dates are not allowed.

### Scenario 6: Prevent an employee from using another employee's assignment

**Given** an employee is logged in

**And** a Project Role Assignment belongs to another employee

**When** the employee tries to submit time using that assignment

**Then** the system shall reject the submission

**And** display an authorization error.

### Scenario 7: View submitted time entries

**Given** an employee is logged in

**And** the employee has previously submitted time entries

**When** the employee opens the My Time Entries screen

**Then** the system shall display the employee's time entries

**And** show the work date, project, role, hours, and status.

### Scenario 8: Submit time for different projects on the same date

**Given** an employee has assignments on two different active projects

**When** the employee submits time for both assignments on the same date

**Then** the system shall save each entry separately

**And** connect each entry to its correct Project Role Assignment.

### Scenario 9: Exclude unapproved time from invoice generation

**Given** a project has time entries with Pending Approval, Approved, and Denied statuses

**When** the system prepares service time for invoice generation

**Then** only the Approved time entries shall be available

**And** Pending Approval and Denied entries shall be excluded.

## 10. Data Ownership

- **Project Time Entry** owns the creation and storage of project time records.
- **Project Time Entry** is responsible for connecting each time record to a valid Project Role Assignment.
- **Project Maintenance** owns project information and project role assignments.
- **Employee Maintenance** owns employee information and employee account details.
- **Time Approval** owns the process of reviewing, approving, and denying submitted time entries.
- **Invoice Generation** reads approved time entries to create invoice service line items.
- Project Time Entry shall not independently change project information, employee information, or agreed project role rates.

## 11. API Requirements

- `POST /api/project-time` — Create and submit a new project time entry.
- `GET /api/project-time/my-entries` — Retrieve time entries for the logged-in employee.
- `GET /api/project-time/{id}` — Retrieve details of a specific time entry, subject to user permissions.
- `GET /api/project-time/my-assignments` — Retrieve the logged-in employee's available project role assignments.
- `GET /api/project-time/summary` — Retrieve the employee's total submitted hours for a selected period.

The API shall validate the employee's assignment, project status, work date, and hours before saving a time entry.

## 12. Screen Requirements

### A. New Time Entry Screen

- Display available project role assignments for the logged-in employee.
- Allow the employee to select a project and role.
- Provide a field for the work date.
- Provide a field for the number of hours worked.
- Provide an optional work description field.
- Include a Submit button.
- Display validation messages when required information is missing or invalid.

### B. My Time Entries Screen

- Display the employee's previously submitted time entries.
- Show the date, project, role, hours, description, and status.
- Allow employees to filter entries by date or period.
- Display the total number of hours entered for the selected period.
- Clearly show whether an entry is Pending Approval, Approved, or Denied.

### C. Project Manager Time Overview

- Allow project managers to view submitted time entries for projects they manage.
- Display employee names, work dates, roles, hours, and statuses.
- Provide access to the separate Time Approval feature.
- Do not allow approval actions to be performed directly through the employee time-entry screen.

## 13. Definition of Done

- Employees can create and submit project time entries.
- Employees can select only their own valid project role assignments.
- The system checks that the project is Active.
- The system validates the work date and number of hours.
- Each submitted entry is connected to the correct Project Role Assignment.
- New entries receive a Pending Approval status.
- Employees can view their submitted time entries.
- Employees can see the current status of each entry.
- Project managers can view time entries for their projects.
- Approved time can be accessed by the invoice generation feature.
- Pending and denied time entries are excluded from invoice generation.
- All required validation and Gherkin acceptance scenarios pass.

## 14. Out of Scope

- Creating and maintaining employees.
- Creating and maintaining projects.
- Creating and maintaining project roles.
- Assigning employees to project roles.
- Reviewing, approving, or denying project time.
- Editing project budgets.
- Calculating employee payroll or salaries.
- Tracking employee attendance or clock-in and clock-out times.
- Entering project expenses or receipts.
- Generating invoices.
- Approving or sending invoices.
- Processing customer payments.
