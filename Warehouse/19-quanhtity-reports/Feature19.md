# Feature: Delivered Quantity Reporting

**Feature ID:** 19
**Branch pattern:** `feature/19-delivered-quantity-reporting`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Report the quantities customers actually received and support comparison with quantities shipped.

## User Stories

### US-19.1: Review delivered quantities
**As a** warehouse manager
**I want to** view delivered quantities for customer shipments
**So that** monitor what customers actually received

**Priority:** P1
**Independent test:** Verify that the system supports the ability to view delivered quantities for customer shipments.
**Acceptance scenarios:** see US-19.1 under Gherkin AC

### US-19.2: Compare shipped and delivered quantities
**As a** warehouse manager
**I want to** compare quantities shipped with quantities delivered
**So that** identify differences that need follow-up

**Priority:** P1
**Independent test:** Verify that the system supports the ability to compare quantities shipped with quantities delivered.
**Acceptance scenarios:** see US-19.2 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST provide delivered quantity information by item and customer order when delivery quantities have been recorded.
- **FR-002**: The system MUST associate delivered quantities with the related delivery, shipment, customer order, and item.
- **FR-003**: The system MUST support comparing delivered quantity with shipped quantity.
- **FR-004**: The system MUST make quantity differences available for follow-up.
- **FR-005**: [NEEDS CLARIFICATION: Confirm whether this report is separate from or included in Warehouse Reporting and Exceptions, and specify date filters and output format.]

## Assumptions

- This report focuses specifically on the customer-facing delivery accuracy.
- If no delivery has occurred yet, the order does not show up in this specific report (or shows as "Pending Delivery").
- The data is pulled from the Delivery Lines (Feature 16) and Shipment Lines (Feature 15).

## Edge Cases

- A shipment was delivered but the driver failed to record exact delivered quantities (system defaults to shipped quantities, or marks as unknown).
- A customer rejects the entire delivery (delivered quantity is zero).
- Discrepancy exists but was resolved via a return/replacement process (handled outside this system).

## Success Criteria

- Managers can clearly see if customers are receiving exactly what was shipped.
- Discrepancies between shipped and delivered are easily identifiable.
- Data directly supports customer service follow-ups.

## Key Entities

- **Delivery Line**: quantity of each item received by the customer.
- **Shipment Line**: quantity of each item sent to the customer.
- **Customer Order**: the order associated with the shipment and delivery.

## Initial Data Model

- Delivery Line: delivery_id, item_id, quantity_delivered.
- Shipment Line: shipment_id, item_id, quantity_shipped.
- Report result: customer_id, customer_order_id, item_id, quantity_shipped, quantity_delivered, difference, delivery_date.

## Gherkin AC

### US-19.1 — Review delivered quantities

#### Scenario: Delivered quantity is reported
* **Given** delivery records include quantities received by the customer
* **When** the manager requests delivered quantity information
* **Then** the system displays recorded delivered quantities linked to their customer orders and items

### US-19.2 — Compare shipped and delivered quantities

#### Scenario: Shipped and delivered quantities are compared
* **Given** a shipment and its delivery have quantities recorded
* **When** the manager views the comparison
* **Then** the system displays shipped quantity, delivered quantity, and any difference

## Data Ownership

- Read-only feature. Owned by the management/administrative function.
- Relies on data owned by Warehouse Operations (Shipment) and Transportation (Delivery).

## API Requirements

- `GET /reports/delivered-vs-shipped` — retrieve comparison data.
- Optional filters: `customer_id`, `start_date`, `end_date`.
- JSON response.

## Screen Requirements

- **Delivered Quantity Report Screen**: Data grid showing Customer, Order/PO, Item, Qty Shipped, Qty Delivered, and Difference.
- Highlight discrepancies in red or yellow.
- Filter controls for Date Range and Customer.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Gherkin scenarios pass.
- Data matches the source transactions perfectly.
- Screen reviewed against UI mockups.

## Out of Scope

- Automating customer refunds or credits for shortages.
- Tracking returns (reverse logistics).