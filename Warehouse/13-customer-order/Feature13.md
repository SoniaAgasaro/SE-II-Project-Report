# Feature: Receive Customer Orders

**Feature ID:** 13
**Branch pattern:** `feature/13-receive-customer-orders`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Record customer orders, customer purchase-order details, items, and requested quantities for fulfillment.

## User Stories

### US-13.1: Enter a customer order
**As a** office employee
**I want to** record a customer's order and PO information
**So that** start order fulfillment

**Priority:** P1
**Independent test:** Verify that the system supports the ability to record a customer's order and PO information.
**Acceptance scenarios:** see US-13.1 under Gherkin AC

### US-13.2: Update an unfulfilled customer order
**As a** office employee
**I want to** correct an order before picking or shipping
**So that** keep the order accurate

**Priority:** P1
**Independent test:** Verify that the system supports the ability to correct an order before picking or shipping.
**Acceptance scenarios:** see US-13.2 under Gherkin AC

### US-13.3: Make an order available for picking
**As a** warehouse employee
**I want to** view customer orders ready to be picked
**So that** know which orders need fulfillment

**Priority:** P1
**Independent test:** Verify that the system supports the ability to view customer orders ready to be picked.
**Acceptance scenarios:** see US-13.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized employee to create and update customer orders.
- **FR-002**: The system MUST associate each customer order with a customer.
- **FR-003**: The system MUST record the order date, customer PO number when provided, and order lines.
- **FR-004**: The system MUST record the item, quantity ordered, and applicable price for each order line.
- **FR-005**: The system MUST make a valid customer order available to the picking process.
- **FR-006**: The system MUST preserve history once fulfillment activity has been recorded.

## Assumptions

- Orders are entered manually by office staff (not via a customer-facing web portal).
- The unit price for an order line is pulled from the Item's current selling price at the time of entry.
- Orders transition from "Entered" to "Ready for Picking" once verified.

## Edge Cases

- Attempting to add an inactive item to a new customer order.
- Modifying an order after some items have already been picked.
- Ordering a quantity that exceeds current warehouse inventory (backorder situation).
- Missing customer PO number (if the customer requires it, though the FR says "when provided").

## Success Criteria

- Customer orders are accurately saved with their line items.
- Orders appear on the picking work list promptly.
- Editing is locked once physical fulfillment (picking) begins.

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

## Data Ownership

- **Customer Order** and **Customer Order Line** are owned by the office/sales function.
- Office employees have write access. Warehouse staff have read access for picking.
- Once picking begins, the order data is effectively locked from office modifications.

## API Requirements

- `GET /customer-orders` — list orders (filter: `status`).
- `GET /customer-orders/{id}` — retrieve an order.
- `POST /customer-orders` — create an order.
- `PUT /customer-orders/{id}` — update an order (only if status is 'Entered').

## Screen Requirements

- **Customer Order Entry screen**: Header (Customer selection, PO Number, Date), Line Item grid (Item, Qty, Price).
- Status indicator (Entered, Ready for Picking, Picked, Shipped).
- Validation for inactive items or missing quantities.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Gherkin scenarios pass.
- Locking mechanism prevents edits during picking.
- Screen reviewed against UI mockups.

## Out of Scope

- Integration with customer EDI for automatic order drops.
- Credit card processing or payment gateways.