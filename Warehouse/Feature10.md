# Feature: Create and Send Supplier Orders

**Feature ID:** 10
**Branch pattern:** `feature/10-create-send-supplier-orders`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Determine replenishment needs using minimum and maximum stock levels and send supplier orders electronically when supported.

## User Stories

### US-10.1: Identify items needing replenishment
**As an** inventory clerk
**I want to** identify items whose quantity is below the minimum level
**So that** I replenish stock before it runs out

**Independent test:** Verify that the system supports the ability to identify items whose quantity is below the minimum level.

### US-10.2: Calculate order quantity
**As an** inventory clerk
**I want to** calculate the quantity needed to bring stock up to its maximum level
**So that** I order the intended replenishment amount

**Independent test:** Verify that the system supports the ability to calculate the quantity needed to bring stock up to its maximum level.

### US-10.3: Send supplier order
**As an** inventory clerk
**I want to** send the supplier order electronically
**So that** I reduce manual order handling

**Independent test:** Verify that the system supports the ability to send the supplier order electronically.

## Functional Requirements

- **FR-001**: The system MUST compare the current inventory quantity with the item's minimum stock level.
- **FR-002**: The system MUST identify an item for replenishment when its inventory quantity is below the minimum.
- **FR-003**: When inventory quantity is below the minimum, the system MUST calculate the order quantity as maximum stock level minus the current inventory quantity, subject to clarification of the stock scope.
- **FR-004**: The system MUST support a minimum and maximum stock level for an item; the values are intended to reflect how quickly the item sells.
- **FR-005**: The system MUST associate the replenishment order with a supplier and the relevant item quantities.
- **FR-006**: The system SHOULD support sending supplier orders electronically.

## Key Entities

- **Item**: product subject to replenishment.
- **Inventory Balance**: current on-hand quantity for an item and stock scope.
- **Supplier Order**: replenishment order sent to a supplier.

## Initial Data Model

- Item or Item-Warehouse Stock Policy: item_id, warehouse_id if applicable, minimum_quantity, maximum_quantity, sales-rate basis if tracked.
- Inventory Balance: item_id, warehouse_id, location_id, quantity_on_hand.
- Supplier Order Line: item_id, quantity_ordered, supplier_id or parent supplier order.

## Gherkin AC

### US-10.1 — Identify items needing replenishment

#### Scenario: Item below minimum is flagged
* **Given** an item's current quantity and minimum level are recorded
* **When** the replenishment process checks the item
* **Then** the system identifies the item as needing an order

### US-10.2 — Calculate order quantity

#### Scenario: Order quantity brings stock to maximum
* **Given** an item's current quantity is below minimum and a maximum level exists
* **When** the system calculates replenishment quantity
* **Then** the calculated quantity equals maximum quantity minus current inventory quantity

### US-10.3 — Send supplier order

#### Scenario: Supplier order is sent
* **Given** a valid supplier order is ready to send
* **When** the clerk chooses the send action
* **Then** the system sends or records the electronic transmission result according to the configured method
