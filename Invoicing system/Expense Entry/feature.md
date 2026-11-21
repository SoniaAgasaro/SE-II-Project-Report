
# Feature 8 — Expense Entry

## 1. Header

**Feature Name:** Expense Entry

**Feature ID:** FEAT-008

**Description:** This feature allows employees or other authorized users to record expenses related to a project. Users can enter the expense date, amount, category, description, and attach a receipt. The recorded expenses can later be used to create expense line items when generating a customer invoice.

**Primary Users:** Employees

**Supporting Users:** Project Managers and Admin/Owner

## 2. User Stories

- As an employee, I want to record expenses I paid for while working on a project so that the company has an accurate record of project costs.
- As an employee, I want to select the project connected to an expense so that the expense is recorded under the correct customer project.
- As an employee, I want to enter the expense date, amount, and description so that the expense details are clear.
- As an employee, I want to attach a receipt so that there is proof of the expense.
- As an employee, I want to view the expenses I have submitted so that I can check the records I entered.
- As a project manager, I want to view expenses recorded for my projects so that I can understand the costs connected to each project.
- As an admin/owner, I want to view and manage project expenses so that expense information is available when preparing invoices.
- As an admin/owner, I want expenses connected to the correct projects so that they can be included in the correct customer invoices.

## 3. Functional Requirements

1. The system shall allow authorized users to create a project expense record.
2. The system shall allow the user to select an existing project for the expense.
3. The system shall only allow expenses to be recorded for valid projects.
4. The system shall allow the user to enter the date the expense occurred.
5. The system shall allow the user to enter the amount of the expense.
6. The system shall allow the user to select an expense category.
7. The system shall allow the user to enter a description explaining what the expense was for.
8. The system shall allow the user to attach a receipt or supporting document to an expense record.
9. The system shall support common receipt file formats such as PDF, JPG, and PNG.
10. The system shall validate that the expense amount is greater than zero.
11. The system shall require the project, expense date, amount, and description before saving an expense.
12. The system shall record the employee or user who entered the expense.
13. The system shall save the expense with a connection to its project.
14. The system shall allow authorized users to view expense records for a selected project.
15. The system shall allow employees to view their own submitted expense records.
16. The system shall display the expense date, project, category, description, amount, and receipt attachment when available.
17. The system shall calculate the total recorded expenses for a selected project or period.
18. The system shall allow authorized users to update an expense record when corrections are needed and the record has not been included in an issued invoice.
19. The system shall prevent unauthorized users from viewing or changing expense records.
20. The system shall make recorded expenses available to the Invoice Generation feature.
21. The system shall prevent the same expense from being added to an invoice more than once.
22. The system shall preserve expense records connected to issued invoices so that accounting history is not changed.

## 4. Assumptions

- Employees or other authorized users are responsible for entering project expenses.
- Each expense must belong to an existing project.
- Expenses are entered using information from receipts or other supporting documents.
- A receipt should be attached whenever one is available.
- The expense amount represents the total amount paid for that expense.
- Expense categories help organize and identify different types of project costs.
- The user who enters an expense is recorded by the system.
- Expenses are recorded separately from employee project time.
- Not every recorded expense is automatically billable to the customer. The company must identify which expenses can be included on the customer invoice.
- Expenses connected to an issued invoice must not be changed directly. Corrections must follow an authorized accounting process.
- Invoice Generation uses the recorded expense information to create expense line items.
- This feature does not process employee reimbursements or customer payments.

## 5. Edge Cases

- A user tries to record an expense without selecting a project.
- A user selects a project that does not exist.
- A user enters an amount of zero or a negative amount.
- A user leaves a required field empty.
- A user enters an expense date in the future.
- A user tries to attach an unsupported file format.
- A receipt file is too large or cannot be uploaded.
- A user submits an expense without attaching a receipt.
- A user accidentally enters the same expense more than once.
- A user tries to record an expense for a project that has already been closed.
- An employee tries to view or edit another employee's expense without permission.
- An expense is connected to the wrong project.
- An expense has already been included in an issued invoice.
- A user tries to change an expense that is already part of an issued invoice.
- A project has expenses but no invoice has been generated yet.
- An expense has been recorded but is not billable to the customer.

## 6. Success Criteria

- Authorized users can successfully create project expense records.
- Each expense is connected to the correct project.
- The system correctly saves the expense date, amount, category, and description.
- Users can attach and view receipt documents.
- The system prevents invalid or incomplete expense records.
- Employees can view their own expense records.
- Project managers and authorized users can view expenses for their projects.
- The system correctly calculates total recorded expenses.
- Expenses are available to the Invoice Generation feature.
- The same expense cannot be included in an invoice more than once.
- Expenses connected to issued invoices are protected from unauthorized changes.

## 7. Key Entities

- **Expense:** Stores the details of money spent on a project.
- **Project:** The project connected to the expense.
- **Employee:** The person who entered the expense.
- **Receipt:** The supporting document that provides proof of the expense.
- **Invoice Line Item:** The invoice record that may be created from a billable expense.

## 8. Initial Data Model

### Expense

- ExpenseID (Primary Key)
- ProjectID (Foreign Key)
- EmployeeID (Foreign Key)
- ExpenseDate
- Category
- Description
- Amount
- ReceiptFileReference
- IsBillable
- DateCreated
- DateUpdated

### Relationships

- One Project can have many Expenses.
- Each Expense belongs to one Project.
- One Employee can enter many Expenses.
- Each Expense is entered by one Employee.
- An Expense may have one receipt attachment.
- An Expense may be used to create an Invoice Line Item if it is billable.
- An Expense must not be included in more than one invoice.

### Example Expense Categories

- Travel
- Transportation
- Accommodation
- Supplies and Materials
- Printing
- Other Project Expenses

### Important Data Notes

- `Amount` stores the total amount paid for the expense.
- `ReceiptFileReference` stores the location or reference to the uploaded receipt file, not the entire file content.
- `IsBillable` identifies whether the expense can be charged to the customer.
- `EmployeeID` identifies the user who entered the expense.
- `ProjectID` connects the expense to the project and therefore to its customer.

## 9. Gherkin AC

### Scenario 1: Successfully create an expense

**Given** an authorized employee is logged in

**And** the employee has selected an existing project

**When** the employee enters a valid expense date, amount, category, and description

**And** submits the expense

**Then** the system shall save the expense

**And** connect it to the selected project

**And** display a confirmation message.

### Scenario 2: Attach a receipt

**Given** an employee is creating a project expense

**When** the employee uploads a supported receipt file

**And** submits the expense

**Then** the system shall save the receipt attachment

**And** connect it to the correct expense record.

### Scenario 3: Prevent an invalid expense amount

**Given** an employee is entering a project expense

**When** the employee enters an amount of zero or a negative amount

**Then** the system shall reject the expense

**And** display a message asking the employee to enter a valid amount.

### Scenario 4: Require important expense information

**Given** an employee is creating a project expense

**When** the employee leaves a required field empty

**Then** the system shall prevent the expense from being saved

**And** identify the missing information.

### Scenario 5: Prevent an invalid receipt file

**Given** an employee is attaching a receipt to an expense

**When** the employee uploads an unsupported file format

**Then** the system shall reject the file

**And** display a message explaining which file formats are accepted.

### Scenario 6: View project expenses

**Given** an authorized user is logged in

**And** a project has recorded expenses

**When** the user opens the project's expense list

**Then** the system shall display the expenses connected to that project

**And** show the date, category, description, and amount for each expense.

### Scenario 7: Calculate total project expenses

**Given** a project has multiple expense records

**When** an authorized user views the project expense summary

**Then** the system shall calculate and display the total recorded expenses for that project.

### Scenario 8: Prevent unauthorized access

**Given** an employee is logged in

**And** the employee does not have permission to view another employee's expense records

**When** the employee tries to access those records

**Then** the system shall reject the request

**And** display an authorization message.

### Scenario 9: Prevent changes to an expense on an issued invoice

**Given** an expense has already been included in an issued invoice

**When** a user tries to change or delete that expense

**Then** the system shall prevent the direct change

**And** explain that an authorized correction process is required.

### Scenario 10: Make billable expenses available for invoicing

**Given** a project has recorded expenses marked as billable

**When** the Invoice Generation feature retrieves project expenses

**Then** the system shall make the billable expenses available for invoice line items

**And** prevent an expense that has already been invoiced from being included again.

## 10. Data Ownership

- **Expense Entry** owns the creation and storage of project expense records.
- **Expense Entry** owns the expense date, category, description, amount, receipt reference, and billable information.
- **Project Maintenance** owns project information.
- **Employee Maintenance** owns employee information and account details.
- **Invoice Generation** reads billable expenses and uses them to create expense invoice line items.
- **Invoice Management** owns the issued invoice records and protects their accounting history.
- Expense Entry shall not create invoices or process customer payments.
- Expense Entry shall not manage employee payroll or reimbursements.

## 11. API Requirements

- `POST /api/expenses` — Create a new project expense.
- `GET /api/expenses/{id}` — Retrieve the details of a specific expense.
- `GET /api/projects/{projectId}/expenses` — Retrieve expenses connected to a selected project.
- `GET /api/expenses/my-expenses` — Retrieve expenses entered by the logged-in employee.
- `PUT /api/expenses/{id}` — Update an expense when changes are allowed.
- `POST /api/expenses/{id}/receipt` — Upload and attach a receipt to an expense.
- `GET /api/expenses/{id}/receipt` — Retrieve or download the receipt attached to an expense.
- `GET /api/projects/{projectId}/expenses/summary` — Retrieve the total recorded expenses for a project.

The API shall validate required information, expense amounts, project access, receipt file formats, and permissions before saving or changing an expense.

## 12. Screen Requirements

### A. New Expense Entry Screen

- Allow the user to select an existing project.
- Provide a field for the expense date.
- Provide a field for the expense amount.
- Provide a category selection.
- Provide a description field.
- Allow the user to upload a receipt.
- Provide a billable-to-customer selection for authorized users.
- Include a Submit button.
- Display validation messages when required information is missing or invalid.

### B. Project Expense List Screen

- Display expenses connected to a selected project.
- Show the expense date, employee, category, description, and amount.
- Allow users to filter expenses by date or category.
- Display the total recorded expenses for the project.
- Identify which expenses are marked as billable.

### C. Expense Details Screen

- Display all information about a selected expense.
- Show the employee who entered the expense.
- Display the project, date, category, description, and amount.
- Allow authorized users to view or download the receipt.
- Allow authorized users to update the expense when changes are permitted.
- Prevent direct changes to expenses already included in issued invoices.

### D. My Expenses Screen

- Allow employees to view their own expense records.
- Display the project, expense date, category, amount, and receipt information.
- Allow employees to filter their records by project or date.

## 13. Definition of Done

- Authorized users can create project expense records.
- Each expense is connected to a valid project.
- The system saves the employee, date, category, description, and amount.
- The system validates required fields and expense amounts.
- Users can upload and view supported receipt files.
- Employees can view their own expenses.
- Project managers and authorized users can view expenses for their projects.
- The system calculates total recorded expenses correctly.
- Authorized users can identify expenses that are billable to customers.
- Billable expenses are available to the Invoice Generation feature.
- The system prevents duplicate invoicing of the same expense.
- Expenses connected to issued invoices cannot be changed directly.
- All required validation and Gherkin acceptance scenarios pass.

## 14. Out of Scope

- Creating and maintaining projects.
- Creating and maintaining employees.
- Entering project work hours.
- Reviewing, approving, or denying project time.
- Generating invoices.
- Creating final invoice line items.
- Approving or sending invoices.
- Processing customer payments.
- Processing employee reimbursements or payroll.
- Managing company bank accounts.
- Managing supplier orders or inventory.
- Maintaining customer billing and payment terms.
