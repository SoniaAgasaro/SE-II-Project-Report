
# Feature 9 — Invoice Generation

## 1. Header

**Feature Name:** Invoice Generation

**Feature ID:** FEAT-009

**Description:** This feature allows the Admin/Owner to generate customer invoices for completed project work. The system uses approved project time and billable project expenses within a selected billing period to create invoice line items. The generated invoice includes company, customer, project, billing, and payment information.

**Primary Users:** Admin/Owner

**Supporting Users:** Project Managers

**Recipient:** Customer

## 2. User Stories

- As an admin/owner, I want to generate an invoice for a selected project so that the customer can be charged for completed work.
- As an admin/owner, I want to select a billing period so that the invoice includes work and expenses from the correct dates.
- As an admin/owner, I want the system to include only approved project time so that customers are not charged for unapproved hours.
- As an admin/owner, I want billable expenses included in the invoice so that customers can be charged for project-related costs.
- As an admin/owner, I want service time grouped by project role and agreed rate so that the invoice is clear and easy to understand.
- As an admin/owner, I want the invoice to use the correct customer and project information so that it is sent to the right customer.
- As an admin/owner, I want the invoice to include the correct project contact so that it reaches the person responsible for reviewing or paying it.
- As an admin/owner, I want the system to calculate line item totals and the invoice total automatically so that billing calculations are accurate.
- As an admin/owner, I want to preview the invoice before it is submitted for approval so that I can check its information.
- As a project manager, I want to review project billing information so that I can help verify that the invoice reflects the work completed.
- As a customer, I want to receive an invoice that clearly explains the services and expenses being charged so that I understand what I am paying for.

## 3. Functional Requirements

1. The system shall allow an authorized Admin/Owner to generate an invoice for an existing project.
2. The system shall require the user to select a project before generating an invoice.
3. The system shall retrieve the customer connected to the selected project.
4. The system shall allow the user to select a billing period using a start date and end date.
5. The system shall retrieve project time entries that belong to the selected project and fall within the billing period.
6. The system shall include only project time entries with an Approved status.
7. The system shall exclude Pending Approval and Denied time entries.
8. The system shall group approved service time by project role and agreed project rate when creating service line items.
9. The system shall calculate service line item totals by multiplying the approved hours by the agreed project rate.
10. The system shall retrieve expenses connected to the selected project and billing period.
11. The system shall include only expenses marked as billable and not previously included in another invoice.
12. The system shall create separate expense line items from billable project expenses.
13. The system shall calculate each expense line item using the recorded expense amount.
14. The system shall prevent the same approved time entry or expense from being included in more than one invoice.
15. The system shall generate a unique invoice number for each invoice.
16. The system shall automatically assign an invoice date.
17. The system shall retrieve company name, mailing address, phone number, and email from the Company record for the invoice header.
18. The system shall retrieve customer name and billing address from the Customer record.
19. The system shall retrieve the appropriate project-specific invoice contact information.
20. The system shall retrieve the applicable payment terms for the invoice.
21. The system shall display the project name and billing period on the invoice.
22. The system shall calculate the total amount of all invoice line items.
23. The system shall save the invoice with a Pending Approval status after generation.
24. The system shall allow the authorized user to preview the generated invoice before submitting it for approval.
25. The system shall allow the user to view previously generated invoices.
26. The system shall allow users to search for invoices by invoice number, customer, project, date, or status.
27. The system shall prevent an invoice from being issued before it has been approved.
28. The system shall preserve invoice details and accounting history after an invoice has been issued.
29. The system shall allow corrections to issued invoices only through an authorized correction process, such as a credit or adjustment, rather than directly changing the issued invoice.
30. The system shall make generated invoices available to the separate Invoice Approval and Invoice Management features.

## 4. Assumptions

- Projects, customers, company information, employees, roles, and project assignments have already been maintained in the system.
- Each project belongs to one customer.
- Each project has an appropriate invoice contact or billing contact.
- Project-specific agreed rates are maintained through Project Maintenance.
- Employees submit project time through Project Time Entry.
- Project managers review time through Time Approval.
- Only Approved project time can be included in an invoice.
- Expenses are entered through Expense Entry.
- Only expenses marked as billable can be charged to customers.
- Expenses already included in an invoice cannot be included again.
- Invoices are generated for one project and one selected billing period.
- An invoice is initially saved with a Pending Approval status.
- Invoice approval and issuing are handled through separate features.
- The invoice number is generated automatically and must be unique.
- The invoice uses the company's saved contact information and the project's appropriate customer contact.
- The system does not automatically assume that every project expense is billable to the customer.

## 5. Edge Cases

- A user tries to generate an invoice without selecting a project.
- A user selects a project that does not exist.
- A project does not have a connected customer.
- A project does not have the required customer billing contact information.
- A user selects an invalid billing period where the start date is after the end date.
- A project has no approved time entries for the selected billing period.
- A project has time entries, but all of them are still Pending Approval.
- A project has only Denied time entries.
- A project has expenses, but none are marked as billable.
- An expense has already been included in a previous invoice.
- An employee has submitted time for the project, but the time has not been approved.
- The project has different employees working under the same role with the same agreed rate.
- The same role has different agreed rates on different projects.
- The system retrieves a time entry that falls outside the selected billing period.
- The invoice contains no approved time or billable expenses.
- Company information is missing or incomplete.
- Customer billing information is missing or incomplete.
- An invoice number is accidentally generated more than once.
- A user tries to issue an invoice that has not been approved.
- A user tries to change an invoice after it has already been issued.
- Two users attempt to generate invoices for the same project and billing period at the same time.

## 6. Success Criteria

- Authorized users can generate invoices for existing projects.
- Users can select a valid billing period.
- The system retrieves the correct customer and project information.
- Only approved project time is included.
- Only billable expenses that have not already been invoiced are included.
- Service time is grouped correctly using project roles and agreed rates.
- Expense line items show the correct descriptions and amounts.
- The system calculates line item totals and invoice totals accurately.
- Each invoice receives a unique invoice number.
- Company, customer, and project-specific contact information appears correctly.
- The generated invoice is saved with a Pending Approval status.
- Users can preview and review generated invoices.
- The system prevents duplicate billing of time entries and expenses.
- Issued invoices preserve their original accounting information.

## 7. Key Entities

- **Invoice:** Stores the main information about a customer invoice, including its number, date, project, customer, billing period, payment terms, and status.
- **Invoice Line Item:** Stores each service or expense charge included in an invoice.
- **Project:** Identifies the project for which the work and expenses are being billed.
- **Customer:** Identifies the customer receiving the invoice.
- **Company:** Provides the company's contact and mailing information for the invoice header.
- **Project Time:** Provides the approved hours used to calculate service charges.
- **Project Role:** Provides the agreed billing rate for the work performed.
- **Project Role Assignment:** Connects the employee, project, and project role associated with the time entry.
- **Expense:** Provides billable project expenses that can be included in the invoice.
- **Employee:** Identifies the person who performed the project work or entered an expense.

## 8. Initial Data Model

### Invoice

- InvoiceID (Primary Key)
- InvoiceNumber
- CustomerID (Foreign Key)
- ProjectID (Foreign Key)
- InvoiceDate
- BillingPeriodStart
- BillingPeriodEnd
- PaymentTerms
- InvoiceContactName
- InvoiceContactEmail
- InvoiceContactPhone
- Status
- Subtotal
- TotalAmount
- DateCreated
- CreatedByEmployeeID (Foreign Key)

### Invoice Line Item

- InvoiceLineItemID (Primary Key)
- InvoiceID (Foreign Key)
- Type
- Date
- Description
- Quantity
- Rate
- Total
- ProjectTimeID (Foreign Key, optional)
- ExpenseID (Foreign Key, optional)

### Relationships

- One Customer can have many Invoices.
- One Project can have many Invoices over time.
- Each Invoice belongs to one Customer and one Project.
- One Invoice can have many Invoice Line Items.
- Each Invoice Line Item belongs to one Invoice.
- An Invoice Line Item can represent either a service charge or an expense charge.
- A service line item is created from approved Project Time.
- An expense line item is created from a billable Expense.
- Each service line item can reference its source Project Time records or the source records used to calculate its grouped quantity.
- Each expense line item references the Expense record it represents.
- The Company record provides the company information displayed on the invoice.

### Invoice Line Item Types

**Service**
- Represents work completed by employees.
- Quantity represents approved hours.
- Rate represents the agreed project role rate.
- Total is calculated as hours multiplied by the agreed rate.

**Expense**
- Represents a billable project expense.
- Quantity can be recorded as 1 for a single expense.
- Rate represents the recorded expense amount.
- Total represents the expense amount.

### Invoice Status Values

- Pending Approval
- Approved
- Issued/Published

### Calculation Rules

- Service Total = Approved Hours × Agreed Project Rate.
- Expense Total = Recorded Billable Expense Amount.
- Invoice Subtotal = Sum of Invoice Line Item Totals.
- Invoice Total = Sum of applicable invoice charges.

## 9. Gherkin AC

### Scenario 1: Generate an invoice with approved project time

**Given** an authorized Admin/Owner is logged in

**And** a project has approved time entries within the selected billing period

**When** the user selects the project and billing period and generates an invoice

**Then** the system shall retrieve the approved time entries

**And** create service invoice line items using the correct project roles and agreed rates

**And** calculate the service totals correctly.

### Scenario 2: Exclude unapproved time

**Given** a project has Pending Approval, Approved, and Denied time entries

**When** the system generates an invoice for the project

**Then** the system shall include only Approved time entries

**And** exclude Pending Approval and Denied entries.

### Scenario 3: Include billable expenses

**Given** a project has expenses marked as billable

**And** the expenses have not been included in previous invoices

**When** the user generates an invoice for the applicable billing period

**Then** the system shall create expense line items for those expenses

**And** calculate their totals using the recorded expense amounts.

### Scenario 4: Exclude expenses that are not billable

**Given** a project has both billable and non-billable expenses

**When** the system generates an invoice

**Then** the system shall include only expenses marked as billable

**And** exclude non-billable expenses.

### Scenario 5: Prevent duplicate billing

**Given** a time entry or expense has already been included in an issued invoice

**When** the system generates another invoice

**Then** the system shall prevent that same source record from being included again.

### Scenario 6: Calculate service charges using the agreed project rate

**Given** an employee has an approved time entry for a project

**And** the employee's assigned project role has an agreed rate of $100 per hour

**When** the system generates the service line item for 5 approved hours

**Then** the system shall use the agreed rate of $100 per hour

**And** calculate the service total as $500.

### Scenario 7: Retrieve customer and company information

**Given** a project is connected to an existing customer

**And** the company information has been saved in the system

**When** the system generates an invoice

**Then** the system shall retrieve the correct customer information

**And** display the company's contact and mailing information in the invoice header.

### Scenario 8: Use the project-specific invoice contact

**Given** a customer has multiple projects with different invoice contacts

**When** the system generates an invoice for one of those projects

**Then** the system shall use the invoice contact connected to the selected project

**And** display that contact's information on the invoice.

### Scenario 9: Prevent an invalid billing period

**Given** an Admin/Owner is generating an invoice

**When** the user selects a start date that is later than the end date

**Then** the system shall reject the billing period

**And** display a message asking the user to enter a valid date range.

### Scenario 10: Save the generated invoice for approval

**Given** the system has successfully generated an invoice

**When** the invoice is saved

**Then** the system shall assign it a unique invoice number

**And** save the invoice with a Pending Approval status

**And** make it available for review through the Invoice Approval feature.

### Scenario 11: Prevent issuing an unapproved invoice

**Given** an invoice has a Pending Approval status

**When** a user tries to issue or publish the invoice

**Then** the system shall prevent the action

**And** explain that the invoice must be approved first.

### Scenario 12: Prevent direct changes to an issued invoice

**Given** an invoice has an Issued/Published status

**When** a user tries to directly change its invoice details or line items

**Then** the system shall prevent the direct change

**And** require an authorized correction process.

## 10. Data Ownership

- **Invoice Generation** owns the process of creating invoices from approved project time and billable expenses.
- **Invoice Generation** owns the creation of invoice records and invoice line items.
- **Company Maintenance** owns company information used in the invoice header.
- **Customer Maintenance** owns customer names, addresses, and general customer contact information.
- **Project Maintenance** owns project information, project-specific roles, agreed rates, and project invoice contact information.
- **Project Time Entry** owns the creation and storage of project time records.
- **Time Approval** owns the approval status and approval history of project time entries.
- **Expense Entry** owns expense records, receipt references, and billable information.
- **Invoice Approval** owns the process of reviewing and approving generated invoices.
- **Invoice Management** owns the process of issuing invoices and preserving issued invoice records.
- Invoice Generation shall read approved time and billable expenses without changing their original records.
- Invoice Generation shall not process customer payments or calculate employee payroll.

## 11. API Requirements

- `POST /api/invoices/generate` — Generate an invoice for a selected project and billing period.
- `GET /api/invoices` — Retrieve invoices with optional search and filtering.
- `GET /api/invoices/{id}` — Retrieve the details of a specific invoice.
- `GET /api/invoices/{id}/line-items` — Retrieve the line items belonging to an invoice.
- `GET /api/projects/{projectId}/billing-data` — Retrieve available approved time and billable expenses for a project.
- `GET /api/projects/{projectId}/billing-summary` — Retrieve a summary of project charges for a selected billing period.
- `GET /api/invoices/{id}/preview` — Retrieve the invoice preview before approval.
- `GET /api/invoices/next-number` — Retrieve or reserve the next available invoice number, if supported by the numbering process.

The API shall validate the selected project, billing period, approved time entries, billable expenses, customer information, and invoice permissions before generating an invoice.

The API shall also prevent source time entries and expenses from being included in more than one invoice.

## 12. Screen Requirements

### A. Generate Invoice Screen

- Allow an authorized user to select a project.
- Display the customer connected to the selected project.
- Allow the user to select a billing period using a start date and end date.
- Display the available approved time entries for that period.
- Display the available billable expenses for that period.
- Display the applicable project roles and agreed rates.
- Display the project-specific invoice contact.
- Provide a Generate Invoice button.
- Display validation messages if required information is missing.

### B. Invoice Preview Screen

- Display the company name, address, phone number, and email.
- Display the customer name and billing address.
- Display the appropriate project invoice contact.
- Display the invoice number and invoice date.
- Display the project name and billing period.
- Display the payment terms.
- Display service line items with descriptions, quantities, rates, and totals.
- Display expense line items with descriptions, quantities, rates, and totals.
- Display the invoice subtotal and total.
- Allow the user to review the invoice before submitting it for approval.

### C. Invoice List Screen

- Display previously generated invoices.
- Show invoice number, customer, project, invoice date, amount, and status.
- Allow users to search by invoice number, customer, or project.
- Allow users to filter invoices by date and status.
- Allow authorized users to open an invoice and view its details.

### D. Invoice Details Screen

- Display all invoice information.
- Display the invoice line items.
- Show the billing period and payment terms.
- Show the current invoice status.
- Provide access to the invoice approval process.
- Prevent direct changes to issued invoices.

## 13. Definition of Done

- Authorized Admin/Owner users can generate invoices for existing projects.
- Users can select a valid billing period.
- The system retrieves the correct customer and project information.
- Only approved project time entries are included.
- Only billable expenses that have not already been invoiced are included.
- Service line items use the correct agreed project rates.
- Expense line items use the correct recorded expense amounts.
- The system calculates line item totals and invoice totals correctly.
- Each invoice receives a unique invoice number.
- Company and customer information appears correctly.
- The correct project-specific invoice contact is displayed.
- Payment terms and billing period are included.
- The generated invoice receives a Pending Approval status.
- Users can preview generated invoices.
- The system prevents duplicate billing of source records.
- Pending invoices cannot be issued before approval.
- Issued invoices preserve their original accounting history.
- All required validation and Gherkin acceptance scenarios pass.

## 14. Out of Scope

- Creating and maintaining company information.
- Creating and maintaining customers.
- Creating and maintaining projects.
- Creating and maintaining employees and project roles.
- Entering project time.
- Reviewing, approving, or denying project time.
- Entering project expenses and uploading receipts.
- Reviewing and approving generated invoices.
- Sending or publishing approved invoices to customers.
- Processing customer payments.
- Tracking overdue invoices or collections.
- Calculating employee payroll.
- Processing employee reimbursements.
- Changing issued invoices directly.
- Creating credit notes or adjustment documents.
