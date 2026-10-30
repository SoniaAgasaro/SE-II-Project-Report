# Feature: Create and Send Supplier Orders

**Feature ID:** 10
**Branch pattern:** `feature/10-create-send-supplier-orders`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Determine replenishment needs using minimum and maximum stock levels and send supplier orders electronically when supported.

## User Stories

### US-10.1: Identify items needing replenishment
**As a** inventory clerk
**I want to** identify items whose quantity is below the minimum level
**So that** replenish stock before it runs out

**Priority:** P1
**Independent test:** Verify that the system supports the ability to identify items whose quantity is below the minimum level.
**Acceptance scenarios:** see US-10.1 under Gherkin AC

### US-10.2: Calculate order quantity
**As a** inventory clerk
**I want to** calculate the quantity needed to bring stock up to its maximum level
**So that** order the intended replenishment amount

**Priority:** P1
**Independent test:** Verify that the system supports the ability to calculate the quantity needed to bring stock up to its maximum level.
**Acceptance scenarios:** see US-10.2 under Gherkin AC

### US-10.3: Send supplier order
**As a** inventory clerk
**I want to** send the supplier order electronically
**So that** reduce manual order handling

**Priority:** P1
**Independent test:** Verify that the system supports the ability to send the supplier order electronically.
**Acceptance scenarios:** see US-10.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST compare the current inventory quantity with the item's minimum stock level.
- **FR-002**: The system MUST identify an item for replenishment when its inventory quantity is below the minimum.
- **FR-003**: When inventory quantity is below the minimum, the system MUST calculate the order quantity as maximum stock level minus the current inventory quantity, subject to clarification of the stock scope.
- **FR-004**: The system MUST support a minimum and maximum stock level for an item; the values are intended to reflect how quickly the item sells.
- **FR-005**: The system MUST associate the replenishment order with a supplier and the relevant item quantities.
- **FR-006**: The system SHOULD support sending supplier orders electronically.
- **FR-007**: [NEEDS CLARIFICATION: Define whether the minimum and maximum are set per item, per warehouse, or per location, and specify how sales rate determines the values.]
- **FR-008**: [NEEDS CLARIFICATION: Confirm which electronic order transmission method is required.]

## Assumptions

- Replenishment is calculated based on the total on-hand inventory across all locations in a warehouse, or globally (pending clarification in FR-007).
- Electronic transmission could be via email (PDF/CSV) or API integration.
- An item must have a primary supplier assigned to generate an automated replenishment order.

## Edge Cases

- An item falls below minimum but has no supplier assigned.
- Multiple items from the same supplier need replenishment (should be grouped into one order).
- Minimum stock level is set higher than maximum stock level.
- Inventory drops below minimum while a previous supplier order is still in transit.

## Success Criteria

- Items below the minimum threshold are accurately identified.
- The suggested order quantity brings inventory exactly to the maximum level.
- Orders are successfully marked as "Sent" after transmission.

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

## Data Ownership

- Replenishment calculation logic is owned by the purchasing/inventory function.
- Supplier Orders created here transition to the ownership of Feature 9 once saved.

## API Requirements

- `GET /replenishment/suggestions` — get a list of items below minimum and suggested quantities.
- `POST /supplier-orders/send` — trigger the electronic transmission of an order.
- JSON responses.

## Screen Requirements

- **Replenishment Dashboard**: List of items below minimum, showing Current Qty, Min, Max, and Suggested Order Qty.
- "Create Order" action grouping selected items by supplier.
- Send confirmation modal showing transmission status.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Calculation logic verified against edge cases.
- Transmission method successfully records a "sent" status.
- Screen reviewed against UI mockups.

## Out of Scope

- Predictive AI forecasting for stock levels.
- Automatic ordering without clerk review and approval.