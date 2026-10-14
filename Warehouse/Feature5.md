# Feature: Supplier Maintenance

**Feature ID:** 5
**Branch pattern:** `feature/5-supplier-maintenance`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Maintain supplier contacts, ordering details, item relationships, and supplier performance information.

## User Stories

### US-5.1: Add a supplier
**As an** inventory clerk
**I want to** add a supplier and its contact information
**So that** I order products from the supplier

**Independent test:** Verify that the system supports the ability to add a supplier and its contact information.

### US-5.2: Update supplier details
**As an** inventory clerk
**I want to** update supplier information and terms
**So that** I use current supplier information

**Independent test:** Verify that the system supports the ability to update supplier information and terms.

### US-5.3: Deactivate supplier
**As an** inventory clerk
**I want to** deactivate a supplier no longer used
**So that** I stop new orders without losing order history

**Independent test:** Verify that the system supports the ability to deactivate a supplier no longer used.

### US-5.4: Maintain supplier item pricing
**As an** inventory clerk
**I want to** record a supplier's price for an item
**So that** I calculate supplier orders using the correct supplier cost

**Independent test:** Verify that the system supports the ability to record a supplier's price for an item.

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add and update supplier records.
- **FR-002**: The system MUST allow an authorized office employee to deactivate a supplier.
- **FR-003**: The system MUST maintain supplier name, address, phone, email, and the supplier's customer/account number when provided.
- **FR-004**: The system SHOULD support supplier terms, typical shipping time, rating, and active status.
- **FR-005**: The system MUST associate items and supplier-specific prices with the relevant supplier.
- **FR-006**: The system MUST NOT permanently delete a supplier referenced by an order or historical record.
- **FR-007**: The system MUST retain historical supplier order records when a supplier is deactivated.

## Key Entities

- **Supplier**: a business from which the warehouse buys products.
- **Item**: a product that may be purchased from a supplier.
- **Supplier Item Price**: a supplier's cost for an item.

## Initial Data Model

- Supplier: supplier_id, name, address, phone, email, supplier_account_number, terms, shipping_time, rating, active_status.
- Supplier Item Price: supplier_item_price_id, supplier_id, item_id, cost, effective date if tracked.

## Gherkin AC

### US-5.1 — Add a supplier

#### Scenario: Supplier is added
* **Given** an inventory clerk has the supplier's required information
* **When** the clerk saves the supplier
* **Then** the system stores the supplier and makes it available for supplier orders

### US-5.2 — Update supplier details

#### Scenario: Supplier with order history is deactivated
* **Given** a supplier has historical orders
* **When** the clerk deactivates the supplier
* **Then** the system marks the supplier inactive and keeps its orders

### US-5.3 — Deactivate supplier

#### Scenario: Supplier item cost is maintained
* **Given** a supplier and item exist
* **When** the clerk records the supplier's cost for the item
* **Then** the system associates that cost with the correct supplier and item
