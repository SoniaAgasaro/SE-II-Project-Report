
# Feature 12: Payment Recording

## 1. Header

**Feature Name:** Payment Recording

**Feature Number:** 12

**System:** Invoicing System

**Description:** This feature allows authorized employees to record payments received from customers for issued invoices. It keeps track of payment amounts, payment dates, payment methods, and remaining balances. The system updates the payment status of an invoice based on the amount received.

**Primary Users:** Administrators and Authorized Employees

**Related Features:**
- Invoice Generation
- Invoice Approval
- Invoice Management
- Customer Maintenance

---

## 2. User Stories

- As an administrator, I want to record a payment from a customer so that the system can keep track of money received.
- As an administrator, I want to connect each payment to an invoice so that I know which invoice the customer is paying.
- As an authorized employee, I want to record partial payments so that the system can show how much the customer still owes.
- As an administrator, I want to see the remaining balance on an invoice so that I can identify unpaid amounts.
- As an authorized employee, I want to view payment history so that I can see all payments made toward an invoice.
- As an administrator, I want the invoice payment status to update automatically so that I can easily identify unpaid, partially paid, and fully paid invoices.
- As an administrator, I want to record the payment method and reference number so that payment information can be checked later.
- As an administrator, I want to correct a payment record when an error is discovered so that the system maintains accurate payment information.

---

## 3. Functional Requirements

1. The system shall allow authorized employees to record payments received from customers.
2. The system shall allow a payment to be connected to an issued invoice.
3. The system shall display the invoice number, customer name, invoice total, amount already paid, and remaining balance before recording a payment.
4. The system shall allow the user to enter:
   - Payment amount
   - Payment date
   - Payment method
   - Payment reference number, when available
   - Additional notes, when needed
5. The system shall support payment methods such as:
   - Bank transfer
   - Check
   - Cash
   - Credit or debit card
   - Other
6. The system shall require the payment amount to be greater than zero.
7. The system shall prevent a payment from being recorded if it is greater than the remaining invoice balance, unless an authorized user follows a separate overpayment process.
8. The system shall calculate the remaining invoice balance after each successful payment.
9. The system shall update the invoice payment status based on the total amount received.
10. The system shall use the following payment statuses:
    - Unpaid: No payment has been recorded.
    - Partially Paid: Some payment has been recorded, but a balance remains.
    - Paid: The full invoice amount has been received.
11. The system shall allow multiple payments to be recorded for the same invoice.
12. The system shall keep a payment history for each invoice.
13. The system shall record the employee who entered each payment.
14. The system shall record the date and time when each payment record was created.
15. The system shall allow authorized users to view payment records for invoices they are permitted to access.
16. The system shall prevent payments from being recorded against invoices that have not been issued.
17. The system shall allow authorized administrators to correct payment information when a mistake is discovered, while keeping a record of the correction.
18. The system shall not automatically process bank transfers, charge credit cards, or withdraw money from customer accounts.
19. The system shall display the total amount paid and the remaining balance on the invoice.
20. The system shall prevent unauthorized users from creating, changing, or viewing payment records.

---

## 4. Assumptions

- Payments are recorded after a customer has received an issued invoice.
- Only authorized employees can record payments.
- A customer may pay an invoice in one payment or through multiple partial payments.
- Each payment must be connected to an existing issued invoice.
- Payment amounts are entered using the invoice's currency.
- The payment date represents the date the company received the payment.
- Payment methods are selected from a list of available options.
- Payment reference numbers may be used to identify bank transfers, checks, or other transactions.
- The system calculates the remaining balance automatically.
- The system does not directly connect to a bank or payment processor.
- Payment corrections should preserve a history of the original record and the correction.
- An invoice is considered fully paid when the total valid payments equal the invoice amount.

---

## 5. Edge Cases

- **Payment amount is zero or negative:** The system shall reject the payment and ask the user to enter a valid amount.
- **Payment is greater than the remaining balance:** The system shall prevent the payment from being recorded and display the remaining balance.
- **Invoice has not been issued:** The system shall prevent payment recording for that invoice.
- **Invoice is already fully paid:** The system shall prevent another payment from being added unless an authorized overpayment process is available.
- **Payment date is in the future:** The system shall prevent the user from recording a future payment date.
- **Payment method is missing:** The system shall ask the user to select a payment method.
- **Payment reference number is missing:** The system shall allow the payment to be recorded if the selected payment method does not require a reference number.
- **Two employees record payments at the same time:** The system shall check the remaining balance before saving each payment to prevent the invoice from being overpaid accidentally.
- **Duplicate payment is entered:** The system should warn the user if the same invoice, amount, payment date, and reference number appear to have already been recorded.
- **Payment is recorded against the wrong invoice:** An authorized administrator shall be able to correct the record while preserving its history.
- **Payment information is incomplete:** The system shall prevent saving when required information is missing.
- **Payment is corrected after recording:** The system shall preserve the original payment information and record who made the correction and when.

---

## 6. Success Criteria

- Authorized employees can record payments for issued invoices.
- Each payment is connected to the correct invoice.
- The system records the payment amount, date, and method.
- Partial payments can be recorded successfully.
- The remaining balance is calculated automatically.
- Invoice payment status updates to Unpaid, Partially Paid, or Paid.
- Multiple payments can be recorded for one invoice.
- The system keeps a complete payment history.
- Payments cannot be recorded against invoices that have not been issued.
- Invalid payment amounts are rejected.
- Unauthorized users cannot access payment records.
- Payment corrections are recorded without losing the original history.
- The system does not process actual financial transactions.

---

## 7. Key Entities

**Payment**
- Represents money received from a customer for an invoice.
- Stores the amount, date, payment method, reference number, and notes.
- Connects each payment to an invoice.

**Invoice**
- Represents the issued invoice being paid.
- Provides the original invoice total.
- Stores or displays the current payment status and remaining balance.

**Employee**
- Identifies the employee who recorded or corrected a payment.
- Helps maintain a record of who performed each action.

**Payment History**
- Stores information about payment changes and corrections.
- Helps administrators review previous payment records.

**Customer**
- Identifies the customer who made the payment.
- Customer information is retrieved through the invoice.

---

## 8. Initial Data Model

### Payment

| Field | Description |
|---|---|
| PaymentID (PK) | Unique identifier for the payment |
| InvoiceID (FK) | Invoice receiving the payment |
| PaymentAmount | Amount received from the customer |
| PaymentDate | Date the payment was received |
| PaymentMethod | Bank Transfer, Check, Cash, Card, or Other |
| ReferenceNumber | Transaction or check reference, when available |
| Notes | Additional payment information |
| RecordedByEmployeeID (FK) | Employee who recorded the payment |
| DateCreated | Date and time the payment was recorded |
| Status | Active or Reversed |

### Payment History

| Field | Description |
|---|---|
| PaymentHistoryID (PK) | Unique identifier for the history record |
| PaymentID (FK) | Payment being changed or reviewed |
| ChangedByEmployeeID (FK) | Employee who made the change |
| PreviousAmount | Payment amount before the change |
| NewAmount | Payment amount after the change |
| ChangeReason | Explanation for the correction |
| ChangeDate | Date and time of the change |

### Invoice Payment Information

The invoice should also provide the following payment information:

| Field | Description |
|---|---|
| TotalAmount | Original invoice total |
| AmountPaid | Total of all valid payments |
| BalanceDue | Amount still owed |
| PaymentStatus | Unpaid, Partially Paid, or Paid |

### Relationships

- One Invoice can have many Payments.
- Each Payment belongs to one Invoice.
- One Employee can record many Payments.
- One Payment can have multiple Payment History records.
- Each Payment History record belongs to one Payment.
- Customer information is obtained through the Invoice connected to the Payment.

### Payment Calculation

The system shall calculate:

**Amount Paid = Sum of all active payments for the invoice**

**Balance Due = Invoice Total - Amount Paid**

Example:

- Invoice Total: $585.50
- First Payment: $300.00
- Second Payment: $100.00
- Amount Paid: $400.00
- Remaining Balance: $185.50
- Payment Status: Partially Paid

When the remaining balance reaches $0.00, the invoice payment status changes to Paid.

---

## 9. Gherkin AC

### Scenario 1: Record a payment

**Given** an invoice has been issued  
**And** the employee has permission to record payments  
**When** the employee enters a valid payment amount, date, and method  
**Then** the system shall save the payment  
**And** the system shall connect the payment to the selected invoice  
**And** the system shall record the employee who entered the payment.

### Scenario 2: Record a partial payment

**Given** an issued invoice has a total amount of $585.50  
**And** no payment has been recorded  
**When** the employee records a payment of $300.00  
**Then** the system shall save the payment  
**And** the system shall calculate the remaining balance as $285.50  
**And** the invoice payment status shall change to Partially Paid.

### Scenario 3: Record the final payment

**Given** an invoice has a remaining balance of $185.50  
**And** the invoice has a Partially Paid status  
**When** the employee records a valid payment of $185.50  
**Then** the system shall save the payment  
**And** the remaining balance shall become $0.00  
**And** the invoice payment status shall change to Paid.

### Scenario 4: Reject an invalid payment amount

**Given** an employee is recording a payment  
**When** the employee enters an amount of zero or less  
**Then** the system shall reject the payment  
**And** the system shall display a message asking for a valid amount.

### Scenario 5: Prevent a payment greater than the remaining balance

**Given** an invoice has a remaining balance of $200.00  
**When** the employee attempts to record a payment of $250.00  
**Then** the system shall prevent the payment from being saved  
**And** the system shall display the remaining balance.

### Scenario 6: Prevent payment recording for an unissued invoice

**Given** an invoice has not been issued  
**When** an employee attempts to record a payment  
**Then** the system shall prevent the payment from being recorded  
**And** the system shall display a message explaining that only issued invoices can receive payments.

### Scenario 7: View payment history

**Given** an invoice has one or more recorded payments  
**When** an authorized employee opens the payment history  
**Then** the system shall display all valid payments for that invoice  
**And** the system shall show the payment amount, date, method, and reference number when available.

### Scenario 8: Prevent unauthorized payment recording

**Given** an employee does not have permission to record payments  
**When** the employee attempts to add a payment  
**Then** the system shall deny the action  
**And** the system shall display an access-denied message.

### Scenario 9: Warn about a possible duplicate payment

**Given** a payment with the same invoice, amount, date, and reference number has already been recorded  
**When** an employee attempts to record the same payment again  
**Then** the system shall display a warning about a possible duplicate  
**And** the system shall ask the employee to review the payment before continuing.

### Scenario 10: Correct a payment record

**Given** a payment has already been recorded  
**And** an authorized administrator discovers an error  
**When** the administrator corrects the payment and provides a reason  
**Then** the system shall save the correction  
**And** the system shall preserve the previous payment information in the history  
**And** the system shall recalculate the invoice balance.

### Scenario 11: Prevent recording a future payment date

**Given** an employee is recording a payment  
**When** the employee enters a payment date later than the current date  
**Then** the system shall reject the date  
**And** the system shall ask the employee to enter a valid payment date.

---

## 10. Data Ownership

- **Payment Recording:** Owns payment records, payment details, payment corrections, and payment history.
- **Invoice Management:** Owns issued invoice information and the official invoice total.
- **Customer Maintenance:** Owns customer information.
- **Employee Maintenance:** Owns employee information used to identify employees who record payments.

Payment Recording can update the payment status and calculated balance associated with an invoice, but it does not change the original issued invoice amount or line items.

---

## 11. API Requirements

The system should provide the following API endpoints:

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/api/invoices/{invoiceId}/payments` | Retrieve payments for an invoice |
| POST | `/api/invoices/{invoiceId}/payments` | Record a new payment |
| GET | `/api/payments/{paymentId}` | Retrieve payment details |
| PUT | `/api/payments/{paymentId}` | Correct an existing payment record |
| GET | `/api/invoices/{invoiceId}/payment-summary` | Retrieve total paid and remaining balance |
| GET | `/api/invoices/{invoiceId}/payment-history` | Retrieve payment history |
| GET | `/api/payments` | Retrieve payment records the user is allowed to access |

### API Rules

- Only authorized users can record or correct payments.
- The system shall confirm that an invoice has been issued before accepting a payment.
- The system shall reject payment amounts that are zero or negative.
- The system shall check the remaining balance before saving a payment.
- The system shall recalculate the invoice balance after every successful payment or correction.
- The system shall update the invoice payment status automatically.
- The system shall preserve the history of payment corrections.
- The system shall not directly change the original issued invoice total.

---

## 12. Screen Requirements

### Screen 1: Payment List

This screen displays recorded payments.

**Information displayed:**
- Payment ID
- Invoice Number
- Customer Name
- Payment Date
- Payment Amount
- Payment Method
- Recorded By

**Actions:**
- View Payment
- Search Payment
- Filter by Date
- Filter by Payment Method

### Screen 2: Record Payment

This screen allows an authorized employee to enter a new payment.

**Information displayed:**
- Invoice Number
- Customer Name
- Invoice Total
- Amount Already Paid
- Remaining Balance

**Input fields:**
- Payment Amount
- Payment Date
- Payment Method
- Reference Number
- Notes

**Actions:**
- Save Payment
- Cancel

### Screen 3: Invoice Payment Summary

This screen shows the payment information for one invoice.

**Information displayed:**
- Invoice Number
- Customer Name
- Original Invoice Total
- Amount Paid
- Remaining Balance
- Payment Status

**Actions:**
- Record Another Payment
- View Payment History

### Screen 4: Payment History

This screen displays all payments connected to an invoice.

**Information displayed:**
- Payment Date
- Payment Amount
- Payment Method
- Reference Number
- Recorded By
- Current Payment Record Status

**Actions:**
- View Payment Details
- View Correction History

### Screen 5: Payment Details and Correction

This screen allows authorized administrators to review or correct a payment record.

**Information displayed:**
- Payment ID
- Invoice Number
- Original Payment Amount
- Payment Date
- Payment Method
- Recorded By

**Input fields for corrections:**
- Corrected Payment Amount
- Reason for Correction

**Actions:**
- Save Correction
- Cancel

---

## 13. Definition of Done

- Authorized employees can record payments for issued invoices.
- Payments are connected to the correct invoice.
- The system saves the payment amount, date, method, and reference number when available.
- The system supports multiple payments for one invoice.
- Partial payments are calculated correctly.
- The system calculates the remaining invoice balance automatically.
- The invoice payment status changes to Unpaid, Partially Paid, or Paid as appropriate.
- Invalid payment amounts are rejected.
- Payments cannot be recorded for invoices that have not been issued.
- The system warns users about possible duplicate payments.
- Authorized administrators can correct payment records.
- Payment corrections are saved in the payment history.
- Unauthorized users cannot access or change payment information.
- The original issued invoice amount remains unchanged.
- All Gherkin acceptance criteria pass testing.
- The feature is reviewed, documented, and committed to the correct Git branch.

---

## 14. Out of Scope

- Generating invoices.
- Approving or issuing invoices.
- Sending invoices to customers.
- Processing actual bank transfers.
- Charging customer credit or debit cards.
- Connecting directly to customer bank accounts.
- Managing employee payroll.
- Processing employee reimbursements.
- Managing refunds or credit notes.
- Creating financial or tax reports.
- Managing company bank accounts.
