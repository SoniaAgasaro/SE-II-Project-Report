
# Feature 11: Invoice Management

## 1. Header

**Feature Name:** Invoice Management

**Feature Number:** 11

**System:** Invoicing System

**Description:** This feature allows authorized employees to manage approved invoices. It includes issuing invoices to customers, viewing issued invoices, tracking invoice status, and keeping invoice records. Once an invoice is issued, the system protects its original information from direct changes.

**Primary Users:** Administrators and Authorized Employees

**Related Features:**
- Invoice Generation
- Invoice Approval
- Customer Maintenance
- Project Maintenance
- Company Maintenance

---

## 2. User Stories

- As an administrator, I want to issue an approved invoice so that it can be sent to the customer for payment.
- As an administrator, I want to view all invoices so that I can keep track of invoices created for different customers and projects.
- As an authorized employee, I want to search for invoices by invoice number, customer, project, or date so that I can quickly find a specific invoice.
- As an administrator, I want to see whether an invoice is pending approval, approved, issued, or overdue so that I can understand its current status.
- As an administrator, I want to view and download an issued invoice so that I can keep a copy or share it with the customer.
- As an administrator, I want the system to record when an invoice was issued so that there is a clear record of when it was sent.
- As an administrator, I want issued invoices to be protected from direct changes so that the company's accounting records remain accurate.
- As an administrator, I want to see the payment status of an invoice so that I can identify invoices that have been paid or are still outstanding.

---

## 3. Functional Requirements

1. The system shall display invoices that have been generated and saved in the system.
2. The system shall allow authorized users to view invoice details.
3. The system shall allow users to search for invoices using:
   - Invoice number
   - Customer name
   - Project name
   - Invoice date
   - Invoice status
4. The system shall allow authorized users to filter invoices by status.
5. The system shall allow an authorized administrator to issue an invoice only when its status is Approved.
6. The system shall change the invoice status from Approved to Issued after a successful issue action.
7. The system shall record the date and time the invoice was issued.
8. The system shall record the employee who issued the invoice.
9. The system shall create a final invoice document that includes:
   - Company name and contact information
   - Customer name and billing information
   - Invoice number and invoice date
   - Project information
   - Billing period
   - Invoice line items
   - Subtotal and total amount
   - Payment terms
   - Payment instructions, when available
10. The system shall allow authorized users to download or print an issued invoice.
11. The system shall allow an issued invoice to be sent to the customer's invoice contact by email, if email delivery is supported and configured.
12. The system shall record the date and time an invoice email is sent and its delivery status when available.
13. The system shall prevent users from directly editing the main details of an issued invoice.
14. The system shall preserve the original invoice information after it has been issued.
15. The system shall display the invoice's payment status when payment information is available.
16. The system shall allow authorized users to view invoice history and related actions.
17. The system shall allow users to view invoices for customers and projects they are authorized to access.
18. The system shall prevent an invoice from being issued more than once.
19. The system shall display a clear message if a user attempts to issue an invoice that has not been approved.
20. The system shall keep issued invoices available for future reference.

---

## 4. Assumptions

- An invoice must be generated before it can be managed.
- An invoice must be approved before it can be issued.
- Only authorized administrators or employees can issue invoices.
- Each invoice has a unique invoice number.
- The customer has an invoice contact with an email address when email delivery is required.
- The company information displayed on the invoice comes from Company Maintenance.
- Customer and project information comes from their respective maintenance features.
- Payment terms are already defined when the invoice is generated.
- Issuing an invoice means officially finalizing it and making it available to the customer.
- Email delivery depends on the system having a working email service.
- Payment tracking may depend on a separate payment-recording feature or an external accounting system.
- Issuing an invoice does not mean that the customer has paid it.

---

## 5. Edge Cases

- **Invoice has not been approved:** The system shall prevent the user from issuing it.
- **Invoice has already been issued:** The system shall prevent the user from issuing it again.
- **Invoice has no customer email address:** The system shall allow the authorized user to download or print the invoice but shall not attempt email delivery.
- **Email delivery fails:** The system shall keep the invoice issued and record the email delivery failure so that the user can try sending it again.
- **Invoice has missing company information:** The system shall warn the user before issuing the invoice if required company details are missing.
- **Invoice has no line items:** The system shall prevent issuing an invoice that does not contain billable items.
- **Invoice has a zero or negative total:** The system shall flag the invoice and prevent issuing it until the problem is reviewed.
- **Two users attempt to issue the same invoice:** The system shall allow only one successful issue action.
- **User tries to edit an issued invoice:** The system shall prevent direct changes to the original invoice.
- **Invoice needs correction after issuing:** The system shall preserve the original invoice and require the correction to be handled through a separate adjustment or credit process.
- **Invoice email is sent more than once:** The system shall keep a record of each sending attempt.
- **Payment information is not available:** The system shall not assume that an invoice has been paid.

---

## 6. Success Criteria

- Authorized users can view and search for invoices.
- Users can filter invoices by their current status.
- Only approved invoices can be issued.
- An invoice changes to Issued after a successful issue action.
- The system records who issued the invoice and when.
- The final invoice document contains all required company, customer, project, and billing information.
- Authorized users can download and print issued invoices.
- Invoices can be emailed to customer contacts when email delivery is available.
- Email delivery attempts and results are recorded.
- Issued invoices cannot be directly edited.
- The system prevents the same invoice from being issued more than once.
- Invoice records remain available for future reference.
- Payment status is displayed only when reliable payment information is available.

---

## 7. Key Entities

**Invoice**
- Stores the main invoice information.
- Includes invoice number, customer, project, invoice date, billing period, payment terms, total amount, and current status.
- Its status changes from Approved to Issued when the invoice is issued.

**Invoice Line Item**
- Stores the service and expense charges included in an invoice.
- Provides the details displayed on the final invoice document.

**Employee**
- Identifies the employee who issued the invoice.
- Helps keep a record of who performed the action.

**Invoice Delivery Record**
- Stores information about sending an invoice to a customer by email.
- Includes the recipient, date and time sent, and delivery result.
- Allows the system to keep a history of sending attempts.

**Customer**
- Provides the customer's name, billing information, and invoice contact details.

**Company**
- Provides the company's name, mailing address, phone number, email, and payment instructions for the invoice document.

---

## 8. Initial Data Model

### Invoice

| Field | Description |
|---|---|
| InvoiceID (PK) | Unique identifier for the invoice |
| InvoiceNumber | Unique invoice number |
| CustomerID (FK) | Customer receiving the invoice |
| ProjectID (FK) | Project connected to the invoice |
| InvoiceDate | Date the invoice was generated |
| BillingPeriodStart | First day of the billing period |
| BillingPeriodEnd | Last day of the billing period |
| InvoiceContactName | Name of the invoice contact |
| InvoiceContactEmail | Email of the invoice contact |
| InvoiceContactPhone | Phone number of the invoice contact |
| PaymentTerms | Payment terms for the customer |
| Status | Pending Approval, Approved, or Issued |
| Subtotal | Total before additional charges or adjustments |
| TotalAmount | Final invoice amount |
| IssuedDate | Date and time the invoice was issued |
| IssuedByEmployeeID (FK) | Employee who issued the invoice |

### Invoice Delivery Record

| Field | Description |
|---|---|
| DeliveryRecordID (PK) | Unique identifier for the delivery record |
| InvoiceID (FK) | Invoice being sent |
| RecipientEmail | Email address used for delivery |
| SentDate | Date and time the email was sent |
| DeliveryStatus | Pending, Sent, Failed, or Delivered when confirmed |
| ErrorMessage | Error details if email delivery fails |

### Relationships

- One Customer can have many Invoices.
- One Project can have many Invoices.
- One Invoice can contain many Invoice Line Items.
- One Employee can issue many Invoices.
- One Invoice can have multiple Invoice Delivery Records if it is sent more than once.
- One Invoice Delivery Record belongs to one Invoice.
- Company information is retrieved from Company Maintenance when preparing the invoice document.

### Important Data Rule

The invoice's original information must remain unchanged after issuing. The system may store delivery records and payment updates separately, but it must not directly change the original issued invoice's charges, customer, project, or billing details.

---

## 9. Gherkin AC

### Scenario 1: View all invoices

**Given** an authorized user is logged into the system  
**When** the user opens the Invoice Management page  
**Then** the system shall display the invoices the user is allowed to access  
**And** the system shall show each invoice's number, customer, project, total amount, and status.

### Scenario 2: Search for an invoice

**Given** invoices are available in the system  
**When** the user searches using an invoice number or customer name  
**Then** the system shall display invoices that match the search  
**And** the system shall display a message if no matching invoice is found.

### Scenario 3: Successfully issue an approved invoice

**Given** an invoice has an Approved status  
**And** the user has permission to issue invoices  
**When** the user selects Issue Invoice  
**Then** the system shall change the invoice status to Issued  
**And** the system shall save the issue date and time  
**And** the system shall save the employee who issued the invoice  
**And** the system shall prepare the final invoice document.

### Scenario 4: Prevent issuing an unapproved invoice

**Given** an invoice has a Pending Approval status  
**When** a user attempts to issue the invoice  
**Then** the system shall prevent the action  
**And** the system shall display a message explaining that the invoice must be approved first.

### Scenario 5: Prevent issuing an invoice twice

**Given** an invoice has already been issued  
**When** a user attempts to issue the same invoice again  
**Then** the system shall prevent the second issue action  
**And** the system shall display the existing issued status.

### Scenario 6: Download an issued invoice

**Given** an invoice has an Issued status  
**And** the user has permission to access it  
**When** the user selects Download Invoice  
**Then** the system shall provide the final invoice document for download.

### Scenario 7: Email an invoice to a customer

**Given** an invoice has an Issued status  
**And** the customer has a valid invoice contact email address  
**And** the email service is available  
**When** the user selects Send Invoice  
**Then** the system shall send the invoice document to the customer's email address  
**And** the system shall record the recipient and sending date and time.

### Scenario 8: Handle a failed email delivery

**Given** an invoice has been issued  
**And** the email service is unavailable or the delivery attempt fails  
**When** the user attempts to send the invoice  
**Then** the system shall display a message explaining that the email could not be sent  
**And** the system shall keep the invoice status as Issued  
**And** the system shall record the failed delivery attempt.

### Scenario 9: Prevent editing an issued invoice

**Given** an invoice has already been issued  
**When** a user attempts to change its original billing details or line items  
**Then** the system shall prevent the changes  
**And** the system shall display a message explaining that issued invoices cannot be directly edited.

### Scenario 10: View invoice delivery history

**Given** an invoice has been sent to a customer one or more times  
**When** an authorized user opens its delivery history  
**Then** the system shall display the recipient, sending date, and delivery result for each attempt.

### Scenario 11: View payment status

**Given** an invoice has been issued  
**And** payment information is available in the system  
**When** an authorized user opens the invoice  
**Then** the system shall display its current payment status.

---

## 10. Data Ownership

- **Invoice Management:** Owns the process of issuing invoices, recording issue information, managing invoice delivery records, and providing access to issued invoice documents.
- **Invoice Generation:** Owns the original creation of invoices and invoice line items.
- **Invoice Approval:** Owns approval decisions and approval history. It makes approved invoices available for issuing.
- **Customer Maintenance:** Owns customer details and general customer contact information.
- **Project Maintenance:** Owns project details and project-specific invoice contact information.
- **Company Maintenance:** Owns company information displayed on invoice documents.
- **Employee Maintenance:** Owns employee information used to identify the employee who issued an invoice.

Invoice Management can update the invoice's status and issue information, but it cannot directly change the original charges or line items of an issued invoice.

---

## 11. API Requirements

The system should provide the following API endpoints:

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/api/invoices` | Retrieve invoices the user is allowed to access |
| GET | `/api/invoices/{invoiceId}` | Retrieve a specific invoice |
| GET | `/api/invoices/{invoiceId}/line-items` | Retrieve invoice line items |
| POST | `/api/invoices/{invoiceId}/issue` | Issue an approved invoice |
| GET | `/api/invoices/{invoiceId}/document` | Generate or retrieve the final invoice document |
| GET | `/api/invoices/{invoiceId}/download` | Download an issued invoice |
| POST | `/api/invoices/{invoiceId}/send` | Send an issued invoice to the customer by email |
| GET | `/api/invoices/{invoiceId}/delivery-history` | Retrieve invoice email delivery attempts |
| GET | `/api/invoices/{invoiceId}/payment-status` | Retrieve available payment information |

### API Rules

- Only authorized users can issue invoices.
- The issue endpoint shall confirm that the invoice has an Approved status.
- The system shall prevent the same invoice from being issued more than once.
- The system shall record the employee and date and time of issue.
- The email endpoint shall only send invoices that have already been issued.
- The system shall save every email delivery attempt.
- The system shall not change the invoice's status to Issued just because an email was successfully sent. Issuing and emailing are separate actions.
- The system shall prevent direct changes to the original information of an issued invoice.
- The system shall check user permissions before displaying or downloading invoice documents.

---

## 12. Screen Requirements

### Screen 1: Invoice Management List

This screen displays invoices and their current status.

**Information displayed:**
- Invoice Number
- Customer Name
- Project Name
- Invoice Date
- Total Amount
- Invoice Status
- Issue Date

**Actions:**
- View Invoice
- Issue Invoice (for approved invoices)
- Download Invoice (for issued invoices)
- Send Invoice (for issued invoices)
- View Delivery History

**Filters:**
- All Invoices
- Pending Approval
- Approved
- Issued

### Screen 2: Invoice Details

This screen displays the complete invoice.

**Information displayed:**
- Company information
- Customer information
- Invoice number and date
- Project name
- Billing period
- Invoice line items
- Subtotal and total amount
- Payment terms
- Invoice status
- Issue date, if issued

**Actions:**
- Issue Invoice, if approved
- Download, if issued
- Send to Customer, if issued
- View Delivery History

### Screen 3: Issue Invoice Confirmation

This screen asks the user to confirm before issuing an invoice.

**Information displayed:**
- Invoice Number
- Customer Name
- Project Name
- Total Amount
- Invoice Contact Email

**Actions:**
- Confirm Issue
- Cancel

The system should make it clear that issuing the invoice finalizes its original billing information.

### Screen 4: Invoice Delivery History

This screen shows the email sending attempts for an invoice.

**Information displayed:**
- Recipient Email
- Date and Time Sent
- Delivery Status
- Error Message, if available

**Actions:**
- Retry Sending (when a previous attempt failed)
- Back to Invoice Details

### Screen 5: Issued Invoice Document

This screen displays the final invoice document in a printable format.

**Information displayed:**
- Company name and contact information
- Customer billing information
- Invoice number
- Invoice date
- Project name
- Billing period
- Service charges
- Expense charges
- Subtotal and total amount
- Payment terms and instructions

**Actions:**
- Download PDF
- Print
- Send by Email

---

## 13. Definition of Done

- Authorized users can view invoices they have permission to access.
- Users can search and filter invoices.
- Only approved invoices can be issued.
- The system changes an invoice's status to Issued after successful issuing.
- The system records who issued the invoice and when.
- The final invoice document contains the required company, customer, project, and billing details.
- Authorized users can download and print issued invoices.
- The system can send issued invoices to customer contacts when email delivery is available.
- The system records email delivery attempts and their results.
- The system prevents the same invoice from being issued more than once.
- Issued invoices cannot be directly edited.
- Invoice records remain available for future reference.
- Payment status is displayed when reliable payment information is available.
- All Gherkin acceptance criteria pass testing.
- The feature is reviewed, documented, and committed to the correct Git branch.

---

## 14. Out of Scope

- Creating new invoices.
- Calculating service charges and expense charges.
- Approving or returning invoices for correction.
- Entering or approving project time.
- Entering project expenses.
- Changing customer, project, company, or employee information.
- Recording or processing customer payments.
- Managing refunds or credit notes.
- Directly editing issued invoices.
- Managing employee payroll or reimbursements.
- Generating financial reports or tax reports.
