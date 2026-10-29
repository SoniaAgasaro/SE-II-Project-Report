# Feature2: Supplier Maintenance
**Feature ID:** 2
**Branch pattern:** `feature/2-supplier-maintenance`
**Created:** 2026-09-28
**Input:** Maintaining supplier information from which the warehouse buys products

## User Stories

### US-2.1: Add a supplier
**As an** office employee
**I want to** add a supplier
**So that** I can make the supplier available for supplier orders

### US-2.2: Edit a supplier
**As an** office employee
**I want to** edit supplier information
**So that** I keep the supplier information updated

### US-2.3: Delete a supplier
**As an** office employee
**I want to** delete a supplier
**So that** I remove a supplier whose services are nolonger required by the warehouse


## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add a supplier.
- **FR-002**: The system MUST allow an authorized office employee to edit supplier information.
- **FR-003**: The system MUST allow an authorized office employee to delete a supplier.
- **FR-004**: The system MUST maintain the supplier's name, address, phone, and email information
- **FR-005**: The system MUST associate supplier information to the items supplied by that supplier


## Acceptance Criteria

### US-2.1 — Add a Supplier

#### Scenario: A supplier can be added
* **Given** the employee enters supplier's information
* **When** the employee saves the supplier's information
* **Then** the supplier is available to supply orders to the warehouse

## US-2.2 — Delete a Supplier

#### Scenario: A supplier can be deleted
* **Given** the employee deletes supplier's information
* **When** the employee removes the supplier's information
* **Then** the supplier is will nolonger be available to supply orders to the warehouse

## US-2.3 — Edit a Supplier

#### Scenario: A supplier can be edited
* **Given** the employee edits the supplier's information
* **When** the employee saves the supplier's information
* **Then** the supplier's information is saved as current