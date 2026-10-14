# Feature: Receive Customer Orders

**Feature ID:** 13
**Branch pattern:** `feature/13-receive-customer-orders`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Record customer orders, customer purchase-order details, items, and requested quantities for fulfillment.

## User Stories

### US-13.1: Enter a customer order
**As an** office employee
**I want to** record a customer's order and PO information
**So that** I start order fulfillment

**Independent test:** Verify that the system supports the ability to record a customer's order and PO information.

### US-13.2: Update an unfulfilled customer order
**As an** office employee
**I want to** correct an order before picking or shipping
**So that** I keep the order accurate

**Independent test:** Verify that the system supports the ability to correct an order before picking or shipping.

### US-13.3: Make an order available for picking
**As a** warehouse employee
**I want to** view customer orders ready to be picked
**So that** I know which orders need fulfillment

**Independent test:** Verify that the system supports the ability to view customer orders ready to be picked.

## Functional Requirements

- **FR-001**: The system MUST allow an authorized employee to create and update customer orders.
- **FR-002**: The system MUST associate each customer order with a customer.
- **FR-003**: The system MUST record the order date, customer PO number when provided, and order lines.
- **FR-004**: The system MUST record the item, quantity ordered, and applicable price for each order line.
- **FR-005**: The system MUST make a valid customer order available to the picking process.
- **FR-006**: The system MUST preserve history once fulfillment activity has been recorded.

## Key Entities

- **Customer Order**: an order received from a customer.
- **Customer Order Line**: item and quantity requested by the customer.
- **Customer**: business placing the order.

## Initial Data Model

- Customer Order: customer_order_id, customer_id, customer_PO_number, order_date, status.
- Customer Order Line: customer_order_line_id, customer_order_id, item_id, quantity_ordered, unit_price.

## Gherkin AC

### US-13.1 — Enter a customer order

#### Scenario: Customer order is entered
* **Given** a customer exists and the order details are available
* **When** an employee enters the customer, PO number, items, and quantities and saves
* **Then** the system stores the order and its lines

### US-13.2 — Update an unfulfilled customer order

#### Scenario: Order is ready for picking
* **Given** a valid customer order has been saved
* **When** a warehouse employee opens the picking work list
* **Then** the order appears as available for picking

### US-13.3 — Make an order available for picking

#### Scenario: Order with fulfillment history is changed
* **Given** a customer order has picking or shipping activity
* **When** an employee attempts to change an ordered quantity
* **Then** the system preserves recorded fulfillment history and applies the configured restriction or adjustment process
