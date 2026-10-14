# Feature: Put Away Received Items

**Feature ID:** 12
**Branch pattern:** `feature/12-put-away-received-items`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Move received products from the receiving area to primary picking or reserve storage locations and record their destinations.

## User Stories

### US-12.1: Find a destination for received stock
**As a** warehouse worker
**I want to** identify an appropriate location for received items
**So that** I store stock in a known place

**Independent test:** Verify that the system supports the ability to identify an appropriate location for received items.

### US-12.2: Replenish a primary picking location
**As a** warehouse worker
**I want to** put stock into a primary location when it needs replenishment
**So that** I keep items available for picking

**Independent test:** Verify that the system supports the ability to put stock into a primary location when it needs replenishment.

### US-12.3: Use reserve storage
**As a** warehouse worker
**I want to** place stock in a reserve location when the primary location does not need stock
**So that** I use warehouse space effectively

**Independent test:** Verify that the system supports the ability to place stock in a reserve location when the primary location does not need stock.

### US-12.4: Record put-away movement
**As a** warehouse worker
**I want to** record the destination and quantity put away
**So that** I keep location inventory accurate

**Independent test:** Verify that the system supports the ability to record the destination and quantity put away.

## Functional Requirements

- **FR-001**: The system MUST display the item and its primary location when the item is identified during put-away, when that location is configured.
- **FR-002**: The system MUST support distinguishing primary picking locations from reserve storage locations.
- **FR-003**: The system MUST support directing received stock to a primary location when replenishment is needed.
- **FR-004**: The system MUST support recording stock in a reserve location when stock is not needed in the primary location, subject to configured warehouse rules.
- **FR-005**: The system MUST record the item, quantity, source receiving location, destination location, date, and employee for a put-away movement when available.
- **FR-006**: The system MUST update inventory quantities for the source and destination locations when put-away is recorded.
- **FR-007**: The system SHOULD support sequencing put-away tasks to reduce unnecessary travel.

## Key Entities

- **Inventory Movement**: recorded movement from one location to another.
- **Inventory Location**: primary, reserve, or receiving location.
- **Item**: product being put away.
- **Employee**: worker performing put-away.

## Initial Data Model

- Inventory Location: location_id, warehouse_id, location_code, location_type (receiving, primary, reserve).
- Put-Away Movement: movement_id, item_id, source_location_id, destination_location_id, quantity, employee_id, movement_date.

## Gherkin AC

### US-12.1 — Find a destination for received stock

#### Scenario: Primary location needs replenishment
* **Given** an item has a configured primary location that is below its target quantity
* **When** the worker begins put-away for that item
* **Then** the system identifies the primary location as a destination option

### US-12.2 — Replenish a primary picking location

#### Scenario: Reserve location is selected
* **Given** the primary location does not need the received stock or configured rules direct stock to reserve
* **When** the worker records a reserve destination
* **Then** the system records the quantity at the selected reserve location

### US-12.3 — Use reserve storage

#### Scenario: Put-away updates locations
* **Given** received stock is recorded at a receiving location
* **When** the worker confirms a destination and quantity
* **Then** the system decreases the source quantity and increases the destination quantity
