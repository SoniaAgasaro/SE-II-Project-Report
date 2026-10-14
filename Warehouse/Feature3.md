# Feature: Item Maintenance

**Feature ID:** 3
**Branch pattern:** `feature/3-item-maintenance`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Maintain the catalog of products the warehouse buys, stores, and sells.

## User Stories

### US-3.1: Add an item
**As an** office employee
**I want to** add an item with its product details
**So that** I make the product available for ordering and inventory tracking

**Independent test:** Verify that the system supports the ability to add an item with its product details.

### US-3.2: Update an item
**As an** office employee
**I want to** update an item's details
**So that** I keep product information current

**Independent test:** Verify that the system supports the ability to update an item's details.

### US-3.3: Deactivate an item
**As an** office employee
**I want to** deactivate an item that is no longer sold
**So that** I preserve historical order and inventory information

**Independent test:** Verify that the system supports the ability to deactivate an item that is no longer sold.

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add an item.
- **FR-002**: The system MUST allow an authorized office employee to update an item.
- **FR-003**: The system MUST allow an authorized office employee to deactivate an item.
- **FR-004**: The system MUST maintain an item description, SKU, UPC when available, and current selling price.
- **FR-005**: The system MUST identify each item with a stable system-generated identifier.
- **FR-006**: The system MUST prevent duplicate SKU values when SKU is used as a unique item code.
- **FR-007**: The system MUST preserve item records referenced by existing orders or inventory history.

## Key Entities

- **Item**: a product that the warehouse purchases, stores, and sells.
- **Supplier Item Price**: the price a particular supplier charges for a particular item.

## Initial Data Model

- Item: item_id, description, SKU, UPC, selling price, active status.
- Supplier Item Price: supplier_item_price_id, supplier_id, item_id, supplier cost, effective date if tracked.

## Gherkin AC

### US-3.1 — Add an item

#### Scenario: Item is added
* **Given** an authorized employee has a product's required details
* **When** the employee saves the item
* **Then** the system stores the item and makes it available to orders and inventory

### US-3.2 — Update an item

#### Scenario: Duplicate SKU is rejected
* **Given** an item already uses a particular SKU
* **When** the employee attempts to save a different item with that SKU
* **Then** the system reports the duplicate and does not create a second item with that SKU

### US-3.3 — Deactivate an item

#### Scenario: Referenced item is deactivated
* **Given** an item is referenced by an order or inventory record
* **When** the employee deactivates the item
* **Then** the system preserves the historical references and marks the item inactive
