# Feature: Ship Customer Orders

**Feature ID:** 15
**Branch pattern:** `feature/15-ship-customer-orders`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Verify picked customer orders, package them, record shipped quantities, and prepare shipment documentation.

## User Stories

### US-15.1: Verify a picked order
**As a** warehouse employee
**I want to** verify the items and quantities before shipment
**So that** send the correct order

**Priority:** P1
**Independent test:** Verify that the system supports the ability to verify the items and quantities before shipment.
**Acceptance scenarios:** see US-15.1 under Gherkin AC

### US-15.2: Record packages
**As a** warehouse employee
**I want to** record the number of boxes or packages prepared
**So that** identify the shipment contents

**Priority:** P1
**Independent test:** Verify that the system supports the ability to record the number of boxes or packages prepared.
**Acceptance scenarios:** see US-15.2 under Gherkin AC

### US-15.3: Create a Bill of Lading
**As a** warehouse employee
**I want to** prepare shipment documentation
**So that** document what is being shipped and where it is going

**Priority:** P1
**Independent test:** Verify that the system supports the ability to prepare shipment documentation.
**Acceptance scenarios:** see US-15.3 under Gherkin AC

### US-15.4: Confirm shipment
**As a** warehouse employee
**I want to** record the shipped quantities and shipment details
**So that** make the order ready for delivery

**Priority:** P1
**Independent test:** Verify that the system supports the ability to record the shipped quantities and shipment details.
**Acceptance scenarios:** see US-15.4 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an employee to verify the picked items and quantities before shipping.
- **FR-002**: The system MUST record the quantity shipped for each customer-order line.
- **FR-003**: The system MUST support recording the number of packages or boxes when used by the business.
- **FR-004**: The system MUST support a Bill of Lading containing ship-to and ship-from information, customer number, shipped date, PO number, driver, item/SKU, description, quantity, price, total, delivery date when known, and received-by information when completed.
- **FR-005**: The system MUST associate the shipment with the customer order and customer.
- **FR-006**: The system MUST make a confirmed shipment available to delivery operations.
- **FR-007**: The system SHOULD support electronic shipment records to reduce unnecessary paper handling.

## Assumptions

- Shipping happens at a packing station.
- The Bill of Lading is generated as a printable document (PDF) or electronic record.
- Once shipped, the customer order status changes to "Shipped".

## Edge Cases

- Quantity shipped is less than quantity picked (due to damage during packing).
- Multiple boxes are used for a single order (packing list per box).
- The driver is not assigned at the time of shipping.
- System must handle concurrent shipping of different orders by different workers.

## Success Criteria

- Shipments accurately reflect the items leaving the warehouse.
- Bill of Lading contains all required information and matches the physical shipment.
- Order status updates to indicate it is ready for delivery.

## Key Entities

- **Shipment**: a customer order prepared and sent for delivery.
- **Bill of Lading**: shipment document recording origin, destination, and shipped items.
- **Customer Order**: order fulfilled by the shipment.
- **Employee**: employee who verifies and ships the order.

## Initial Data Model

- Shipment: shipment_id, customer_order_id, shipped_date, driver_employee_id, package_count, status.
- Shipment Line: shipment_line_id, shipment_id, item_id, quantity_shipped, unit_price.
- Bill of Lading: bill_of_lading_id, shipment_id, ship_from, ship_to, PO_number, delivery_date, received_by.

## Gherkin AC

### US-15.1 — Verify a picked order

#### Scenario: Order is verified and shipped
* **Given** a customer order has picked quantities recorded
* **When** the employee verifies the order and confirms shipment
* **Then** the system records the shipped quantities and shipment status

### US-15.2 — Record packages

#### Scenario: Bill of Lading is prepared
* **Given** a shipment has customer and item details
* **When** the employee creates the Bill of Lading
* **Then** the document includes the available ship-from, ship-to, PO, driver, item, quantity, and shipment details

### US-15.3 — Create a Bill of Lading

#### Scenario: Shipment quantity differs from picked quantity
* **Given** a picked order is being verified
* **When** the employee enters a different shipped quantity
* **Then** the system records the actual shipped quantity and makes the difference visible

## Data Ownership

- **Shipment** and **Bill of Lading** are owned by warehouse operations.
- The **Customer Order** status is updated by this feature.
- Delivery operations have read access to Shipments.

## API Requirements

- `GET /shipments` — list shipments (filter: `status`).
- `POST /shipments` — create a shipment from a picked order.
- `PUT /shipments/{id}` — update shipment details (packages, shipped qty).
- `GET /shipments/{id}/bill-of-lading` — generate/retrieve BoL.

## Screen Requirements

- **Shipping Verification screen**: List of picked items and quantities. Input for actual shipped quantity and number of packages.
- **Print Bill of Lading** action button.
- Dropdown to assign a Driver (optional at this stage).

## Definition of Done

- All functional requirements implemented and demonstrated.
- Bill of Lading generates correctly with accurate data.
- Inventory is decremented (if not done during picking).
- Screen reviewed against UI mockups.

## Out of Scope

- Integration with external shipping carriers (FedEx, UPS) for label printing.
- Calculating shipping costs or freight charges.