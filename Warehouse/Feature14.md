# Feature: Pick Customer Orders

**Feature ID:** 14
**Branch pattern:** `feature/14-pick-customer-orders`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Guide warehouse workers through picking the right item, from the right location, in the required quantity.

## User Stories

### US-14.1: View picking instructions
**As a** warehouse worker
**I want to** view the customer order's items, quantities, and picking locations
**So that** I pick orders efficiently

**Independent test:** Verify that the system supports the ability to view the customer order's items, quantities, and picking locations.

### US-14.2: Verify the item being picked
**As a** warehouse worker
**I want to** scan or otherwise verify an item before picking it
**So that** I avoid picking the wrong product

**Independent test:** Verify that the system supports the ability to scan or otherwise verify an item before picking it.

### US-14.3: Record actual picked quantity
**As a** warehouse worker
**I want to** record how many units were picked
**So that** I report what can actually be shipped

**Independent test:** Verify that the system supports the ability to record how many units were picked.

### US-14.4: Record a picking shortage
**As a** warehouse worker
**I want to** record when a location does not contain enough stock
**So that** I make the shortage visible before shipment

**Independent test:** Verify that the system supports the ability to record when a location does not contain enough stock.

## Functional Requirements

- **FR-001**: The system MUST show the items and quantities to pick for a customer order.
- **FR-002**: The system MUST show the primary picking location for an item when a location is assigned.
- **FR-003**: The system MUST support a picking sequence for the order or route when sequence information is available.
- **FR-004**: The system MUST allow the worker to verify the picked item using a barcode or item code.
- **FR-005**: The system MUST record the actual quantity picked for each order line.
- **FR-006**: The system MUST allow a worker to record a shortage when the available quantity is less than the requested quantity.
- **FR-007**: The system MUST retain both the ordered quantity and the actual picked quantity.
- **FR-008**: The system MUST update or reserve inventory according to the configured picking process.

## Key Entities

- **Customer Order**: order being picked.
- **Customer Order Line**: ordered and picked quantities.
- **Inventory Balance**: stock available at a location.
- **Inventory Location**: location from which an item is picked.
- **Employee**: picker.

## Initial Data Model

- Customer Order Line: item_id, quantity_ordered, quantity_picked, shortage_quantity or shortage status.
- Pick Activity: pick_activity_id, customer_order_id, item_id, location_id, quantity_picked, employee_id, picked_at.

## Gherkin AC

### US-14.1 — View picking instructions

#### Scenario: Picker sees picking instructions
* **Given** a customer order is ready for picking and its items have locations
* **When** the warehouse worker opens the order
* **Then** the system displays each item, requested quantity, and available picking location

### US-14.2 — Verify the item being picked

#### Scenario: Wrong item is scanned
* **Given** the picker is working on an order line for a specific item
* **When** the picker scans a different item
* **Then** the system identifies that the scanned item does not match the expected item

### US-14.3 — Record actual picked quantity

#### Scenario: Shortage is recorded
* **Given** the requested quantity exceeds stock available at the picking location
* **When** the picker records the actual quantity picked
* **Then** the system saves the picked quantity and identifies the shortage

### US-14.4 — Record a picking shortage

#### Scenario: Correct quantity is picked
* **Given** the picker has the correct item and sufficient stock
* **When** the picker verifies the item and enters the picked quantity
* **Then** the system records the actual quantity picked for that order line
