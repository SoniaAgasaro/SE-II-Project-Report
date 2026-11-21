
# Feature: Customer Maintenance

## 1. Header
- **Feature Name:** Customer Maintenance
- **System:** Invoicing System
- **Description:** Allows authorized administrators to create, view, and update customer information used for managing consulting projects and preparing customer invoices.
- **Primary Actors:** Administrator, Owner

## 2. User Stories
- As an administrator, I want to add a customer so that the company can maintain records of businesses it provides consulting services to.
- As an administrator, I want to update customer information so that the system always has accurate customer details.
- As an administrator, I want to view customer information so that I can identify customers and their contacts.
- As an administrator, I want each customer to have a unique customer number so that customers can be easily identified.
- As an administrator, I want to maintain customer billing terms so that invoices have the correct payment deadlines.
- As an administrator, I want to maintain the customer's main contact information so that the company knows who to contact regarding business and billing matters.

## 3. Functional Requirements
- FR-1: The system shall allow an authorized administrator to create a customer record.
- FR-2: The system shall assign a unique customer ID to each customer.
- FR-3: The system shall assign a customer number to each customer for identification purposes.
- FR-4: The system shall store the customer's name and address.
- FR-5: The system shall store the customer's main contact name, phone number, and email address.
- FR-6: The system shall allow administrators to view customer information.
- FR-7: The system shall allow administrators to update existing customer information.
- FR-8: The system shall allow administrators to maintain customer billing terms.
- FR-9: The system shall make customer billing terms available to invoice-related features.
- FR-10: The system shall make customer information available when creating and maintaining projects.
- FR-11: The system shall validate required customer information before saving a record.
- FR-12: The system shall prevent duplicate customer numbers.
- FR-13: The system shall restrict customer maintenance to authorized users.

## 4. Assumptions
- Customers represent businesses that receive consulting services from the company.
- Each customer has a unique customer ID and customer number.
- Customer numbers may be used to identify customers when receiving electronic payment or customer information.
- The customer's main contact is the default contact for general communication.
- Different projects belonging to the same customer may have different contacts.
- Billing terms are agreed upon between the consulting company and the customer.
- Billing terms specify when an invoice is due after it is issued.
- Customer billing terms may be used as the default payment terms when creating invoices.
- Customer records with existing project or invoice history should be retained.

## 5. Edge Cases
- An administrator attempts to create a customer without a name.
- An administrator attempts to create a customer without a required address.
- An administrator enters an invalid contact email address.
- An administrator enters an incorrectly formatted phone number.
- An administrator attempts to create a duplicate customer number.
- A customer has no main contact person available.
- An administrator attempts to update billing terms while invoices already exist.
- An administrator attempts to delete a customer who has existing projects or invoices.
- An unauthorized user attempts to modify customer information.
- A customer has different invoice contacts for different projects.

## 6. Success Criteria
- Administrators can successfully create, view, and update customer records.
- Each customer has a unique customer ID and customer number.
- Customer contact information is stored correctly.
- Customer billing terms can be maintained.
- Customer information is available when creating projects and invoices.
- Invalid or incomplete information is rejected with appropriate validation messages.
- Existing project and invoice records remain associated with their customers.
- Unauthorized users cannot modify customer information.

## 7. Key Entities
- **Customer:** Represents a business that receives consulting services and pays invoices.
- **Project:** Represents work performed for a customer.
- **Invoice:** Represents a bill sent to a customer for services and expenses.
- **Company:** Represents the consulting company that provides services and sends invoices.

## 8. Initial Data Model

### Customer
- CustomerID (Primary Key)
- CustomerNumber (Unique)
- Name
- Address
- MainContactName
- Phone
- Email
- BillingTerms

### Relationships
- One customer may have multiple projects.
- Each project belongs to one customer.
- One customer may receive multiple invoices.
- Each invoice is associated with one customer.
- Customer billing terms may be used as default invoice terms.
- A project may have its own invoice contact information.

## 9. Gherkin AC

### **Scenario 1: Successfully create a customer**
**Given** an administrator is logged into the system
**When** the administrator enters valid customer information
**And** selects Save
**Then** the system shall create the customer record
**And** assign a unique customer ID and customer number
**And** display a confirmation message.

### **Scenario 2: View customer information**
**Given** customer records exist in the system
**When** an administrator opens the customer list
**Then** the system shall display the available customers
**And** show their customer numbers, names, and main contact information.

### **Scenario 3: Update customer information**
**Given** a customer record already exists
**When** an administrator changes the customer's contact information
**And** selects Save
**Then** the system shall update the customer record
**And** display the updated information.

### **Scenario 4: Maintain customer billing terms**
**Given** a customer record already exists
**When** an administrator enters or updates the customer's billing terms
**And** selects Save
**Then** the system shall save the billing terms
**And** make the updated terms available for future invoices.

### **Scenario 5: Prevent duplicate customer numbers**
**Given** a customer already exists with a particular customer number
**When** an administrator attempts to assign the same customer number to another customer
**Then** the system shall reject the duplicate number
**And** display an appropriate validation message.

### **Scenario 6: Prevent incomplete customer records**
**Given** an administrator is creating a customer record
**When** the administrator leaves a required field empty
**And** selects Save
**Then** the system shall display a validation message
**And** shall not save the incomplete record.

### **Scenario 7: Retain customer history**
**Given** a customer has existing projects or invoices
**When** an administrator attempts to delete the customer
**Then** the system shall prevent deletion of the customer record
**And** preserve its associated project and invoice history.

## 10. Data Ownership
- The Customer Maintenance feature owns the Customer entity.
- Administrators and owners are responsible for maintaining customer information.
- Project Maintenance may read customer information when creating projects.
- Invoice Maintenance may read customer information when preparing invoices.
- Invoice-related features may use the customer's billing terms as default invoice terms.
- Project Maintenance is responsible for maintaining project-specific invoice contact information.
- Other features shall not directly modify customer records.

## 11. API Requirements
- POST /api/customers - Create a customer record.
- GET /api/customers - Retrieve the customer list.
- GET /api/customers/{id} - Retrieve an individual customer record.
- PUT /api/customers/{id} - Update customer information.
- GET /api/customers/{id}/billing-terms - Retrieve customer billing terms.
- The API shall assign unique customer IDs and customer numbers.
- The API shall validate required fields and contact information.
- The API shall prevent duplicate customer numbers.
- The API shall enforce authorization for customer maintenance.

## 12. Screen Requirements

### Customer List Screen
- Display customer ID.
- Display customer number.
- Display customer name.
- Display customer address.
- Display main contact name.
- Display phone number.
- Display email address.
- Display billing terms.
- Provide an Add Customer button.
- Provide an Edit option for each customer.
- Allow administrators to search for customers by name or customer number.

### Customer Information Screen
- Provide fields for customer name and address.
- Provide a customer number field or automatically assigned customer number.
- Provide fields for main contact name, phone, and email.
- Provide a billing terms field.
- Provide a Save button.
- Provide a Cancel button.
- Display validation messages for missing or invalid information.

## 13. Definition of Done
- Administrators can create, view, and update customer records.
- Each customer receives a unique ID and customer number.
- Customer contact information is stored correctly.
- Billing terms can be created and updated.
- Required fields and contact information are validated.
- Duplicate customer numbers are rejected.
- Existing project and invoice relationships are preserved.
- Customer information is available to project and invoice features.
- All Gherkin acceptance criteria pass testing.
- Unauthorized users cannot modify customer information.

## 14. Out of Scope
- Processing customer payments.
- Managing customer bank accounts.
- Managing customer contracts.
- Managing customer-specific project contacts.
- Generating invoices.
- Sending automatic payment reminders.
- Managing customer credit scores.
