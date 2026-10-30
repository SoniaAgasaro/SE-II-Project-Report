# Feature: Warehouse Maintenance

**Feature ID:** 2
**Branch pattern:** `feature/2-warehouse-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Maintain one or more warehouse locations where the company stores inventory.

## User Stories

### US-2.1: Add a warehouse
**As a** office employee
**I want to** add a warehouse location
**So that** track inventory across the company's warehouses

**Priority:** P1
**Independent test:** Verify that the system supports the ability to add a warehouse location.
**Acceptance scenarios:** see US-2.1 under Gherkin AC

### US-2.2: Update a warehouse
**As a** office employee
**I want to** update warehouse information
**So that** keep location information accurate

**Priority:** P1
**Independent test:** Verify that the system supports the ability to update warehouse information.
**Acceptance scenarios:** see US-2.2 under Gherkin AC

### US-2.3: Deactivate a warehouse
**As a** office employee
**I want to** deactivate a warehouse that is no longer used
**So that** preserve historical inventory and order records

**Priority:** P1
**Independent test:** Verify that the system supports the ability to deactivate a warehouse that is no longer used.
**Acceptance scenarios:** see US-2.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add a warehouse.
- **FR-002**: The system MUST allow an authorized office employee to update warehouse information.
- **FR-003**: The system MUST allow an authorized office employee to deactivate a warehouse.
- **FR-004**: The system MUST associate inventory locations with a specific warehouse.
- **FR-005**: The system MUST preserve historical records associated with a warehouse that has inventory or transaction history.
- **FR-006**: The system MUST assign each warehouse a stable system-generated identifier.
- **FR-007**: The system MUST prevent a deactivated warehouse from being selected for new inventory, receiving, or put-away operations.

## Assumptions

- A warehouse is a physical site; storage locations within it are modeled by the Inventory Location entity.
- Only authorized office employees can create, update, or deactivate warehouses.
- A deactivated warehouse remains queryable for historical reporting.

## Edge Cases

- Deactivation attempted on a warehouse with active inventory.
- Warehouse name duplicated within the company.
- Warehouse address left blank.
- Two employees edit the same warehouse concurrently.
- A warehouse is referenced by an open supplier order or customer order.

## Success Criteria

- A warehouse can be created and retrieved by its identifier.
- Deactivation marks the warehouse inactive without deleting history.
- Inactive warehouses do not appear in active-location pickers for new operations.
- Validation rejects missing required fields with clear messages.

## Key Entities

- **Warehouse**: a physical warehouse operated by the company.
- **Inventory Location**: a slot, bin, or other storage location inside a warehouse.

## Initial Data Model

- Warehouse: warehouse_id, name, address, contact information, active status.
- Inventory Location: location_id, warehouse_id, location code, location type, active status.

## Gherkin AC

### US-2.1 — Add a warehouse

#### Scenario: Warehouse is added
* **Given** an authorized office employee has valid warehouse details
* **When** the employee saves the new warehouse
* **Then** the system stores the warehouse and assigns it a stable identifier

### US-2.2 — Update a warehouse

#### Scenario: Warehouse is deactivated with history
* **Given** a warehouse has existing inventory or transaction history
* **When** an authorized employee deactivates it
* **Then** the system marks it inactive and retains its historical records

### US-2.3 — Deactivate a warehouse

#### Scenario: Inventory is assigned to a warehouse
* **Given** two or more warehouses exist
* **When** an employee records inventory at one warehouse
* **Then** the system associates the inventory with the selected warehouse

## Data Ownership

- **Warehouse** and **Inventory Location** are owned by the office/administrative function.
- Only authorized office employees may create, update, or deactivate them.
- Warehouse-operations features (receiving, put-away, picking, shipping) MAY read warehouse/location data but MUST NOT modify warehouse attributes.

## API Requirements

- `GET /warehouses` — list warehouses (filter: `active=true|false`).
- `GET /warehouses/{id}` — retrieve one warehouse.
- `POST /warehouses` — create a warehouse.
- `PUT /warehouses/{id}` — update a warehouse.
- `PATCH /warehouses/{id}/deactivate` — deactivate.
- `GET /warehouses/{id}/locations` — list locations for a warehouse.
- JSON bodies; server-side validation of required fields.

## Screen Requirements

- **Warehouse Maintenance screen**: list of warehouses with active/inactive filter; Add/Edit form with name, address, contact; Deactivate action with confirmation.
- **Location Maintenance sub-screen**: list of locations per warehouse with code, type, and active status.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Validation and deactivation scenarios pass their Gherkin AC.
- Deactivated warehouses are excluded from new-operation pickers.
- History retained for warehouses with inventory or transactions.
- Screen reviewed against the UI mockups in `Warehouse/docs/`.

## Out of Scope

- Automatic warehouse selection for orders (handled by fulfillment features).
- Warehouse capacity planning / slotting optimization.
- Physical floor-plan visualization.