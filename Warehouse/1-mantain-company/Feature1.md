# Feature: Company Maintenance

**Feature ID:** 1
**Branch pattern:** `feature/1-company-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Maintain the company information used by the warehouse system.

## User Stories

### US-1.1: Add company information
**As a** office employee
**I want to** add the company's business information
**So that** keep the system's company record current

**Priority:** P1
**Independent test:** Verify that the system supports the ability to add the company's business information.
**Acceptance scenarios:** see US-1.1 under Gherkin AC

### US-1.2: Update company information
**As a** office employee
**I want to** update company information
**So that** use current business information

**Priority:** P1
**Independent test:** Verify that the system supports the ability to update company information.
**Acceptance scenarios:** see US-1.2 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add company information.
- **FR-002**: The system MUST allow an authorized office employee to update existing company information.
- **FR-003**: The system MUST identify each company record with a stable system-generated identifier.
- **FR-004**: The system MUST validate required company fields before saving a record.
- **FR-005**: The system MUST retain a single authoritative company record for the operating business.
- **FR-006**: The system MUST make the current company information available to other features that print or reference company details (e.g., Bills of Lading).
- **FR-007**: The system MUST preserve the company record when dependent records exist; deactivation MAY be used instead of deletion.

## Assumptions

- Only authorized office employees can modify company records.
- The system maintains one company record for the operating business.
- The company record is referenced by shipment documents and is therefore long-lived.
- Company details are entered once and updated infrequently.

## Edge Cases

- An employee attempts to save a company record with a blank required field.
- An employee enters an invalid email or phone format.
- Two employees edit the same company record at the same time (last-write-wins is acceptable, but the conflict SHOULD be surfaced).
- An employee attempts to create a second company record when one already exists.
- The company record is referenced by an existing Bill of Lading and an employee attempts to delete it.

## Success Criteria

- A valid company record can be created and retrieved after saving.
- An incomplete company record is rejected with a clear, field-level message.
- Updates persist and are visible to subsequent users and dependent documents.
- Invalid email/phone values are rejected before save.
- The company record cannot be permanently deleted while referenced.

## Key Entities

- **Company**: the business operating the warehouse system.

## Initial Data Model

- Company: company_id, company name, business address, phone, email.
  - `company_id` — system-generated, immutable primary key.
  - `company name` — required, non-empty.
  - `business address` — required.
  - `phone` — required, validated format.
  - `email` — required, validated format.

## Gherkin AC

### US-1.1 — Add company information

#### Scenario: Company information is added
* **Given** an authorized office employee is maintaining company records
* **When** the employee enters valid company information and saves it
* **Then** the system stores the company record and makes it available for later use

#### Scenario: Required company information is missing
* **Given** the employee is entering a company record
* **When** the employee attempts to save without a required field
* **Then** the system identifies the missing information and does not save an incomplete record

#### Scenario: Invalid contact format is rejected
* **Given** the employee is entering a company record
* **When** the employee enters an invalid email or phone format and saves
* **Then** the system rejects the value and explains the expected format

### US-1.2 — Update company information

#### Scenario: Company information is updated
* **Given** a company record already exists
* **When** the employee changes a company field and saves
* **Then** the system stores the updated value

#### Scenario: Concurrent update is detected
* **Given** two employees open the same company record
* **When** both save changes
* **Then** the system preserves the last saved values and informs the second employee that the record changed

## Data Ownership

- **Company** is owned by the office/administrative function.
- Only authorized office employees may create or update it.
- Dependent features (shipment/Bill of Lading) MAY read but MUST NOT modify company data.

## API Requirements

- `GET /companies/{id}` — retrieve the company record.
- `POST /companies` — create a company record.
- `PUT /companies/{id}` — update a company record.
- JSON request/response bodies; server-side validation of required fields and formats.
- Errors returned as `400` (validation), `404` (not found), `409` (concurrent modification), `403` (unauthorized).

## Screen Requirements

- **Company Maintenance screen**: form with company name, address, phone, email; Save and Cancel actions; inline validation messages; read-only display of `company_id`.
- Field-level error messages aligned to the offending field.
- Success confirmation after save.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Validation and error cases pass their Gherkin scenarios.
- No hard-delete of referenced company data.
- API endpoints documented and exercised via at least one integration test.
- Screen reviewed against the UI mockups in `Warehouse/docs/`.

## Out of Scope

- Multi-company support.
- Company logo/branding management.
- Company-level user/permission administration (handled by the auth feature).