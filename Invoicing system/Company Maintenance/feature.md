
# Feature: Company Maintenance

## 1. Header
- **Feature Name:** Company Maintenance
- **System:** Invoicing System
- **Description:** Allows an administrator or owner to maintain the consulting company's information used for business operations and customer invoices.
- **Primary Actors:** Administrator, Owner

## 2. User Stories
- As an administrator, I want to add company information so that the system knows which company is providing consulting services.
- As an administrator, I want to update company information so that invoices display accurate business details.
- As an owner, I want to view company information so that I can verify the information used on invoices.
- As an administrator, I want to maintain banking information so that customers have the information needed to make payments.

## 3. Functional Requirements
- FR-1: The system shall allow an administrator to create a company record.
- FR-2: The system shall store the company ID, name, address, website URL, phone number, email address, and banking information.
- FR-3: The system shall allow an administrator to view company information.
- FR-4: The system shall allow an administrator to update company information.
- FR-5: The system shall use company information when preparing customer invoices.
- FR-6: The system shall restrict company information maintenance to authorized users.
- FR-7: The system shall validate required information before saving a company record.

## 4. Assumptions
- The system is initially designed for one consulting company.
- Company information is maintained by an administrator or owner.
- Company address, phone number, and email may appear on invoices.
- Banking information is maintained to support customer payments.
- Company information is not entered by regular employees.

## 5. Edge Cases
- An administrator attempts to save a company record without a required name.
- An administrator enters an invalid email address.
- An administrator enters an incorrectly formatted phone number.
- An administrator attempts to create a duplicate company record.
- An administrator attempts to update company information without permission.
- Banking information is missing when an invoice requires payment instructions.

## 6. Success Criteria
- An authorized administrator can successfully create a company record.
- Company information can be viewed and updated.
- Required fields are validated before saving.
- Updated company information is available when generating invoices.
- Unauthorized users cannot change company information.

## 7. Key Entities
- **Company:** Represents the consulting company that provides services and sends invoices.

## 8. Initial Data Model
### Company
- CompanyID (Primary Key)
- Name
- Address
- WebsiteURL
- Phone
- Email
- BankInformation

## 9. Gherkin AC
### Scenario 1: Successfully create company information
Given an administrator is logged into the system
When the administrator enters valid company information
And selects Save
Then the system shall create the company record
And display a confirmation message.

### Scenario 2: Update company information
Given a company record already exists
When an administrator changes the company information
And selects Save
Then the system shall update the record
And display the updated information.

### Scenario 3: Missing required information
Given an administrator is creating a company record
When the administrator leaves the company name empty
And selects Save
Then the system shall display a validation message
And shall not save the incomplete record.

### Scenario 4: Unauthorized access
Given a user does not have company maintenance permission
When the user attempts to update company information
Then the system shall deny the update.

## 10. Data Ownership
- The Company Maintenance feature owns the Company entity.
- Only authorized administrators or owners may create and update company information.
- Invoice-related features may read company information but shall not directly modify it.

## 11. API Requirements
- POST /api/company - Create a company record.
- GET /api/company - Retrieve company information.
- PUT /api/company/{id} - Update company information.
- The API shall validate required fields.
- The API shall enforce authorization for company updates.

## 12. Screen Requirements
### Company Information Screen
- Display company name.
- Display company address.
- Display website URL.
- Display phone number.
- Display email address.
- Display banking information.
- Provide an Edit button.
- Provide a Save button.
- Provide a Cancel button.
- Display validation messages when information is missing or invalid.

## 13. Definition of Done
- Company information can be created, viewed, and updated.
- Required fields are validated.
- Unauthorized users cannot modify company information.
- Company information is available to the invoice generation feature.
- All acceptance criteria pass testing.

## 14. Out of Scope
- Managing multiple consulting companies.
- Processing customer payments.
- Managing employee payroll.
- Managing customer billing terms.
- Automatically sending invoices to customers.
