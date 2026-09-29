# Feature9: Supplier Order Maintenance
**Feature ID:** 9
**Branch pattern:** `feature/9-supply-order-maintenance`
**Created:** 2026-09-28
**Input:** Maintaining supplier orders used to request products from suppliers, Creating an order to supplier using inventory level and stocking calculations, receiving products, comparing the received and ordered quantities, and putting the received products into their warehouse locations and update inventory

## User Stories

### US-9.1: Create and Add a supplier order
**As a** office employee
**I want to** add and create a supplier order for needed items
**So that** record what the warehouse is ordering and replenish inventory

### US-9.2: Edit a supplier order
**As a** office employee
**I want to** edit a supplier order
**So that** correct or update an order before it is completed

### US-9.3: Delete a supplier order
**As a** office employee
**I want to** delete a supplier order
**So that** remove an order that should no longer be maintained

### US-9.4: Calculate order quantity
**As a** authorized office employee
**I want to** use minimum and maximum inventory levels
**So that** order the needed amount

### US-9.5: Receive a supplier order
**As a** warehouse employee
**I want to** check in a supplier shipment
**So that** record what was actually received

### US-9.6: Compare received quantity
**As a** warehouse employee
**I want to** compare received quantity with ordered quantity
**So that** identify quantity differences

### US-9.7: Put away received items
**As a** warehouse employee
**I want to** place received items in warehouse locations
**So that** store inventory in the appropriate location

### US-9.8: Move inventory
**As a** warehouse employee
**I want to** move inventory from one warehouse location to another
**So that** keep inventory location information accurate


## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add a supplier order.
- **FR-002**: The system MUST allow an authorized office employee to edit a supplier order.
- **FR-003**: The system MUST allow an authorized office employee to delete a supplier order.
- **FR-004**: The system MUST associate a supplier order with a supplier.
- **FR-005**: The system MUST record the item and quantity ordered for each supplier order line.
- **FR-006**: The system MUST allow an authorized user to create a supplier order.
- **FR-007**: The system MUST use an item's minimum and maximum stocking values when determining whether an order is needed.
- **FR-008**: The system MUST identify an item for ordering when inventory quantity is below its minimum.
- **FR-009**: When inventory quantity is below the minimum, the system MUST calculate an order quantity that brings inventory up to the maximum.
- **FR-010**: The minimum and maximum values MUST be based on how fast the item is selling.
- **FR-011**: The system MUST allow a warehouse employee to receive a supplier order using its PO number.
- **FR-012**: The system MUST record the quantity received for each item.
- **FR-013**: The system MUST compare quantity received with quantity ordered.
- **FR-014**: The system MUST identify when received quantity differs from ordered quantity.
- **FR-015**: The system MUST associate receiving information with the supplier order and its items.
- **FR-016**: The system MUST allow a warehouse employee to record where received items are put away.
- **FR-017**: The system MUST associate an item quantity with its warehouse location.
- **FR-018**: The system MUST allow an authorized warehouse employee to move inventory from one warehouse location to another.
- **FR-019**: The system MUST update the recorded inventory location when inventory is moved.


## Acceptance Criteria

### US-9.1 — Add a supplier order

#### Scenario: A supplier order can be added
* **Given** an authorized employee enters the supplier and ordered items
* **When** the employee saves the order
* **Then** the supplier order is available for receiving

### US-9.2 — Create a supplier order

#### Scenario: An item below minimum is included in replenishment
* **Given** inventory quantity is below the item's minimum
* **When** the stocking rule is applied
* **Then** the calculated quantity orders inventory up to the item's maximum

### US-9.3 — Receive a supplier order

#### Scenario: Received quantity is recorded
* **Given** a supplier shipment arrives and the employee identifies its PO number
* **When** the employee enters received quantities
* **Then** the system records the received quantities and compares them with the order

### US-9.4 — Put away received items

#### Scenario: Received items are put away
* **Given** received inventory is ready to be stored
* **When** the warehouse employee records the destination location
* **Then** the system records the item quantity at that location
