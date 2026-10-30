# Feature: Supplier Order Maintenance

**Feature ID:** 9
**Branch pattern:** `feature/9-supplier-order-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Maintain supplier orders and their ordered items, quantities, purchase-order numbers, and dates.

## User Stories

### US-9.1: Add a supplier order
**As a** inventory clerk
**I want to** create a supplier order with its supplier and items
**So that** record what the warehouse is requesting

**Priority:** P1
**Independent test:** Verify that the system supports the ability to create a supplier order with its supplier and items.
**Acceptance scenarios:** see US-9.1 under Gherkin AC

### US-9.2: Update a supplier order
**As a** inventory clerk
**I want to** update an eligible supplier order
**So that** correct order details before receiving

**Priority:** P1
**Independent test:** Verify that the system supports the ability to update an eligible supplier order.
**Acceptance scenarios:** see US-9.2 under Gherkin AC

### US-9.3: Cancel or remove an unused supplier order
**As a** inventory clerk
**I want to** cancel an order that has not been received
**So that** avoid processing an order that is no longer needed

**Priority:** P1
**Independent test:** Verify that the system supports the ability to cancel an order that has not been received.
**Acceptance scenarios:** see US-9.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to create and update supplier orders.
- **FR-002**: The system MUST associate each supplier order with one supplier.
- **FR-003**: The system MUST record a purchase-order number, order date, and one or more ordered item lines.
- **FR-004**: The system MUST record the item and quantity ordered for each order line.
- **FR-005**: The system MUST prevent edits that would silently overwrite received quantities or other completed receiving history.
- **FR-006**: The system MUST preserve completed supplier orders and receiving history; orders with history MUST be cancelled or deactivated rather than permanently deleted.

## Assumptions

- Purchase Order (PO) numbers are unique per supplier.
- An order can only be edited if it has not yet entered the receiving process.
- The `unit_cost` at the time of order creation is pulled from the Supplier Item Price record.

## Edge Cases

- Attempting to edit an order that already has received items.
- Entering a negative or zero quantity for an order line.
- Adding an inactive item to a new supplier order.
- Canceling an order that is currently out for delivery.

## Success Criteria

- Orders are accurately saved with their line items.
- Invalid quantities are rejected.
- Orders with receiving history are protected from deletion.
- Canceled orders are visibly marked but remain in the system.

## Key Entities

- **Supplier Order**: an order the warehouse sends to a supplier.
- **Supplier Order Line**: an item and quantity requested on a supplier order.
- **Supplier**: the party receiving the order.

## Initial Data Model

- Supplier Order: supplier_order_id, supplier_id, PO_number, order_date, status.
- Supplier Order Line: supplier_order_line_id, supplier_order_id, item_id, quantity_ordered, unit_cost.

## Gherkin AC

### US-9.1 — Add a supplier order

#### Scenario: Supplier order is created
* **Given** a supplier exists and the clerk has selected items and quantities
* **When** the clerk saves the order with a PO number
* **Then** the system stores the supplier order and its order lines

### US-9.2 — Update a supplier order

#### Scenario: Order line quantity is invalid
* **Given** a supplier order is being entered
* **When** the clerk enters a zero or negative quantity
* **Then** the system rejects the invalid quantity and explains what must be corrected

### US-9.3 — Cancel or remove an unused supplier order

#### Scenario: Order with history is cancelled
* **Given** a supplier order has receiving history
* **When** the clerk attempts to remove the order
* **Then** the system preserves the order history and uses a cancellation or inactive status instead of deleting the record

## Data Ownership

- **Supplier Order** and **Supplier Order Line** are owned by the purchasing function.
- Only authorized inventory clerks may create, update, or cancel orders.
- The receiving feature (Feature 11) MAY read and update order line quantities as items are received.

## API Requirements

- `GET /supplier-orders` — list orders (filter: `status`, `supplier_id`).
- `GET /supplier-orders/{id}` — retrieve an order with lines.
- `POST /supplier-orders` — create an order.
- `PUT /supplier-orders/{id}` — update an unreceived order.
- `PATCH /supplier-orders/{id}/cancel` — cancel an order.

## Screen Requirements

- **Supplier Order screen**: Header (Supplier, PO Number, Date), Line Item grid (Item, Quantity, Unit Cost).
- "Add Line" and "Remove Line" actions (only available if not received).
- Status indicator (Draft, Ordered, Partially Received, Received, Canceled).

## Definition of Done

- All functional requirements implemented and demonstrated.
- Validation and cancellation scenarios pass their Gherkin AC.
- Order history is immutable once receiving begins.
- Screen reviewed against UI mockups.

## Out of Scope

- Automated emailing or faxing of POs to suppliers (handled in Feature 10).
- Multi-currency conversions.