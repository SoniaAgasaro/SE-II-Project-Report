# Feature: Customer Maintenance

**Feature ID:** 6
**Branch pattern:** `feature/6-customer-maintenance`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Maintain customer information needed to receive, fulfill, route, and deliver customer orders.

## User Stories

### US-6.1: Add a customer
**As an** office employee
**I want to** add a customer and customer number
**So that** I accept orders from that customer

**Independent test:** Verify that the system supports the ability to add a customer and customer number.

### US-6.2: Update customer information
**As an** office employee
**I want to** update customer contact and delivery information
**So that** I use accurate order and delivery details

**Independent test:** Verify that the system supports the ability to update customer contact and delivery information.

### US-6.3: Deactivate customer
**As an** office employee
**I want to** deactivate a customer no longer ordering
**So that** I preserve historical customer orders

**Independent test:** Verify that the system supports the ability to deactivate a customer no longer ordering.

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add and update customer records.
- **FR-002**: The system MUST maintain a customer number and the customer information needed for orders and delivery.
- **FR-003**: The system MUST allow a customer to be deactivated.
- **FR-004**: The system MUST NOT permanently delete a customer referenced by customer orders, routes, shipments, or deliveries.
- **FR-005**: The system MUST retain historical customer orders when a customer is deactivated.

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
