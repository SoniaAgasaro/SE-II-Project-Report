# Feature: Customer Maintenance

**Feature ID:** 6
**Branch pattern:** `feature/6-customer-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Maintain customer information needed to receive, fulfill, route, and deliver customer orders.

## User Stories

### US-6.1: Add a customer
**As a** office employee
**I want to** add a customer and customer number
**So that** accept orders from that customer

**Priority:** P1
**Independent test:** Verify that the system supports the ability to add a customer and customer number.
**Acceptance scenarios:** see US-6.1 under Gherkin AC

### US-6.2: Update customer information
**As a** office employee
**I want to** update customer contact and delivery information
**So that** use accurate order and delivery details

**Priority:** P1
**Independent test:** Verify that the system supports the ability to update customer contact and delivery information.
**Acceptance scenarios:** see US-6.2 under Gherkin AC

### US-6.3: Deactivate customer
**As a** office employee
**I want to** deactivate a customer no longer ordering
**So that** preserve historical customer orders

**Priority:** P1
**Independent test:** Verify that the system supports the ability to deactivate a customer no longer ordering.
**Acceptance scenarios:** see US-6.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add and update customer records.
- **FR-002**: The system MUST maintain a customer number and the customer information needed for orders and delivery.
- **FR-003**: The system MUST allow a customer to be deactivated.
- **FR-004**: The system MUST NOT permanently delete a customer referenced by customer orders, routes, shipments, or deliveries.
- **FR-005**: The system MUST retain historical customer orders when a customer is deactivated.
- **FR-006**: The system MUST enforce unique customer numbers.

## Assumptions

- Customer numbers are manually assigned or system-generated but must be unique.
- Delivery addresses are tied to the customer record.
- Customers can be assigned to routes via the Route Maintenance feature.

## Edge Cases

- Attempting to save a customer with a duplicate customer number.
- Deactivating a customer that is currently assigned to an active route.
- Missing required delivery address.
- Invalid phone/email formats.

## Success Criteria

- Customer records are accurately stored and retrievable.
- Customer numbers are unique.
- Deactivated customers are excluded from new order creation but visible in reporting.

## Key Entities

- **Customer**: a store or business that purchases products from the warehouse.
- **Route**: a delivery route that may include the customer.

## Initial Data Model

- Customer: customer_id, customer_number, name, address, phone, email, active_status.

## Gherkin AC

### US-6.1 — Add a customer

#### Scenario: Customer is added
* **Given** an office employee has the customer's required details
* **When** the employee saves the customer
* **Then** the system stores the customer and makes the customer available for orders

### US-6.2 — Update customer information

#### Scenario: Customer with order history is deactivated
* **Given** a customer has existing orders
* **When** the employee deactivates the customer
* **Then** the system marks the customer inactive and retains the order history

### US-6.3 — Deactivate customer

#### Scenario: Required customer number is missing
* **Given** the employee is entering a customer record
* **When** the employee attempts to save without a customer number
* **Then** the system identifies the missing required information and does not save the record

## Data Ownership

- **Customer** is owned by the office/administrative function.
- Only authorized office employees may create, update, or deactivate customers.
- Routing, shipping, and delivery features MAY read customer data but MUST NOT modify it.

## API Requirements

- `GET /customers` — list customers (filter: `active`).
- `GET /customers/{id}` — retrieve a customer.
- `POST /customers` — create a customer.
- `PUT /customers/{id}` — update a customer.
- `PATCH /customers/{id}/deactivate` — deactivate.
- JSON bodies; server-side uniqueness check on customer number.

## Screen Requirements

- **Customer Maintenance screen**: list with search; Add/Edit form with customer number, name, address, phone, email.
- Inline validation for required fields and formats.
- Deactivate action with confirmation.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Validation and deactivation scenarios pass their Gherkin AC.
- Inactive customers blocked from new orders.
- Screen reviewed against UI mockups.

## Out of Scope

- Customer credit limits or billing management.
- Customer portal/login access.