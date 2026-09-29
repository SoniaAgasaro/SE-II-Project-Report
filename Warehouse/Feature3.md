# Feature3: Customer Maintenance
**Feature ID:** 3
**Branch pattern:** `feature/3-customer-maintenance`
**Created:** 2026-09-28
**Input:** Maintaining customer information that purchase products from the warehouse

## User Stories

### US-3.1: Add a customer
**As an** office employee
**I want to** add a customer
**So that** I can make the customer available for customer orders

### US-3.2: Edit a customer
**As an** office employee
**I want to** edit customer information
**So that** I keep the customer information updated


## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add a customer.
- **FR-002**: The system MUST allow an authorized office employee to edit customer information.
- **FR-003**: The system MUST allow an authorized office employee to delete a customer.
- **FR-004**: The system MUST maintain the customer's name, and number
- **FR-005**: The system MUST maintain customers with their orders and delivery


## Acceptance Criteria

### US-3.1 — Add a customer

#### Scenario: A customer can be added
* **Given** the employee enters customer's information
* **When** the employee saves the customer's information
* **Then** the customer is available to purchase and order products from the warehouse

### US-3.2 — Edit a customer

#### Scenario: A customer's information can be edited
* **Given** the employee edites customer's information such as new email
* **When** the employee saves the customer's information
* **Then** the customer's new information is saved as current

