# Feature: Supplier Maintenance

**Feature ID:** 5
**Branch pattern:** `feature/5-supplier-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Maintain supplier contacts, ordering details, item relationships, and supplier performance information.

## User Stories

### US-5.1: Add a supplier
**As a** inventory clerk
**I want to** add a supplier and its contact information
**So that** order products from the supplier

**Priority:** P1
**Independent test:** Verify that the system supports the ability to add a supplier and its contact information.
**Acceptance scenarios:** see US-5.1 under Gherkin AC

### US-5.2: Update supplier details
**As a** inventory clerk
**I want to** update supplier information and terms
**So that** use current supplier information

**Priority:** P1
**Independent test:** Verify that the system supports the ability to update supplier information and terms.
**Acceptance scenarios:** see US-5.2 under Gherkin AC

### US-5.3: Deactivate supplier
**As a** inventory clerk
**I want to** deactivate a supplier no longer used
**So that** stop new orders without losing order history

**Priority:** P1
**Independent test:** Verify that the system supports the ability to deactivate a supplier no longer used.
**Acceptance scenarios:** see US-5.3 under Gherkin AC

### US-5.4: Maintain supplier item pricing
**As a** inventory clerk
**I want to** record a supplier's price for an item
**So that** calculate supplier orders using the correct supplier cost

**Priority:** P1
**Independent test:** Verify that the system supports the ability to record a supplier's price for an item.
**Acceptance scenarios:** see US-5.4 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add and update supplier records.
- **FR-002**: The system MUST allow an authorized office employee to deactivate a supplier.
- **FR-003**: The system MUST maintain supplier name, address, phone, email, and the supplier's customer/account number when provided.
- **FR-004**: The system SHOULD support supplier terms, typical shipping time, rating, and active status.
- **FR-005**: The system MUST associate items and supplier-specific prices with the relevant supplier.
- **FR-006**: The system MUST NOT permanently delete a supplier referenced by an order or historical record.
- **FR-007**: The system MUST retain historical supplier order records when a supplier is deactivated.

## Assumptions

- A supplier can provide multiple items, and an item can be provided by multiple suppliers.
- Supplier pricing may change over time; order lines should preserve the cost at the time of ordering.
- Only authorized inventory clerks and office employees can maintain supplier data.

## Edge Cases

- A clerk attempts to add an item to an inactive supplier.
- A supplier is deactivated while a draft supplier order is being created.
- Duplicate supplier names are entered.
- A supplier's contact information is missing or invalid.

## Success Criteria

- Supplier records can be created, updated, and retrieved.
- Deactivated suppliers are hidden from new order creation but visible in history.
- Supplier item prices correctly link to the specific supplier and item combination.

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

## Data Ownership

- **Supplier** and **Supplier Item Price** are owned by the purchasing/administrative function.
- Only authorized clerks may create, update, or deactivate suppliers.
- Receiving and reporting features MAY read supplier data but MUST NOT modify it.

## API Requirements

- `GET /suppliers` — list suppliers (filter: `active`).
- `GET /suppliers/{id}` — retrieve a supplier.
- `POST /suppliers` — create a supplier.
- `PUT /suppliers/{id}` — update a supplier.
- `PATCH /suppliers/{id}/deactivate` — deactivate.
- `POST /suppliers/{id}/items` — associate item and cost.

## Screen Requirements

- **Supplier Maintenance screen**: list with search; Add/Edit form with contact info, terms, shipping time, rating.
- **Supplier Items sub-screen**: list of items and costs associated with the supplier.
- Inline validation and deactivate confirmation.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Validation and deactivation scenarios pass their Gherkin AC.
- Deactivated suppliers blocked from new orders.
- Screen reviewed against UI mockups.

## Out of Scope

- Automated supplier scorecard calculation.
- EDI (Electronic Data Interchange) integration for supplier pricing.