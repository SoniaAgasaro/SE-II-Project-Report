# Feature: Inventory Maintenance and Counting

**Feature ID:** 4
**Branch pattern:** `feature/4-inventory-maintenance-counting`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Track item quantities by warehouse and storage location and support inventory counts and adjustments.

## User Stories

### US-4.1: View inventory by location
**As a** warehouse employee
**I want to** view the recorded quantity of an item at a warehouse location
**So that** I find stock and know where it is stored

**Independent test:** Verify that the system supports the ability to view the recorded quantity of an item at a warehouse location.

### US-4.2: Count inventory
**As a** warehouse employee
**I want to** record a physical count of an item
**So that** I compare the actual quantity with the recorded quantity

**Independent test:** Verify that the system supports the ability to record a physical count of an item.

### US-4.3: Adjust inventory
**As an** authorized warehouse employee
**I want to** record an approved inventory adjustment
**So that** I keep recorded stock accurate

**Independent test:** Verify that the system supports the ability to record an approved inventory adjustment.

### US-4.4: Move inventory
**As a** warehouse employee
**I want to** record inventory moved between locations
**So that** I keep the system's location quantities accurate

**Independent test:** Verify that the system supports the ability to record inventory moved between locations.

## Functional Requirements

- **FR-001**: The system MUST track inventory by item, warehouse, and storage location.
- **FR-002**: The system MUST record the on-hand quantity for an item at a location.
- **FR-003**: The system MUST allow a warehouse employee to record a physical count.
- **FR-004**: The system MUST show the difference between the recorded quantity and the physical count.
- **FR-005**: The system MUST record an inventory adjustment and the employee responsible for it.
- **FR-006**: The system MUST update the source and destination quantities when inventory is moved between locations.
- **FR-007**: The system MUST retain a record of inventory adjustments and movements.

## Key Entities

- **Inventory Balance**: quantity of an item at a particular warehouse location.
- **Inventory Movement**: a recorded transfer of stock between locations.
- **Inventory Count**: a physical count used to compare actual and recorded stock.

## Initial Data Model

- Inventory Balance: inventory_balance_id, item_id, warehouse_id, location_id, quantity_on_hand.
- Inventory Count: inventory_count_id, item_id, location_id, counted_quantity, recorded_quantity, count_date, employee_id.
- Inventory Movement: movement_id, item_id, source_location_id, destination_location_id, quantity, movement_date, employee_id.

## Gherkin AC

### US-4.1 — View inventory by location

#### Scenario: Physical count reveals a difference
* **Given** an item has a recorded on-hand quantity
* **When** a warehouse employee enters the physical count
* **Then** the system shows the recorded quantity, counted quantity, and difference

### US-4.2 — Count inventory

#### Scenario: Inventory adjustment is recorded
* **Given** an authorized employee has identified and approved a quantity adjustment
* **When** the employee enters the adjustment and reason
* **Then** the system updates the balance and records who made the adjustment

### US-4.3 — Adjust inventory

#### Scenario: Inventory is moved
* **Given** an item has a quantity at a source location
* **When** the employee records a move to a destination location
* **Then** the system decreases the source balance and increases the destination balance by the moved quantity
