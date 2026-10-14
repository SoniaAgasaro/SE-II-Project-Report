# Feature: Ship Customer Orders

**Feature ID:** 15
**Branch pattern:** `feature/15-ship-customer-orders`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Verify picked customer orders, package them, record shipped quantities, and prepare shipment documentation.

## User Stories

### US-15.1: Verify a picked order
**As a** warehouse employee
**I want to** verify the items and quantities before shipment
**So that** I send the correct order

**Independent test:** Verify that the system supports the ability to verify the items and quantities before shipment.

### US-15.2: Record packages
**As a** warehouse employee
**I want to** record the number of boxes or packages prepared
**So that** I identify the shipment contents

**Independent test:** Verify that the system supports the ability to record the number of boxes or packages prepared.

### US-15.3: Create a Bill of Lading
**As a** warehouse employee
**I want to** prepare shipment documentation
**So that** I document what is being shipped and where it is going

**Independent test:** Verify that the system supports the ability to prepare shipment documentation.

### US-15.4: Confirm shipment
**As a** warehouse employee
**I want to** record the shipped quantities and shipment details
**So that** I make the order ready for delivery

**Independent test:** Verify that the system supports the ability to record the shipped quantities and shipment details.

## Functional Requirements

- **FR-001**: The system MUST allow an employee to verify the picked items and quantities before shipping.
- **FR-002**: The system MUST record the quantity shipped for each customer-order line.
- **FR-003**: The system MUST support recording the number of packages or boxes when used by the business.
- **FR-004**: The system MUST support a Bill of Lading containing ship-to and ship-from information, customer number, shipped date, PO number, driver, item/SKU, description, quantity, price, total, delivery date when known, and received-by information when completed.
- **FR-005**: The system MUST associate the shipment with the customer order and customer.
- **FR-006**: The system MUST make a confirmed shipment available to delivery operations.
- **FR-007**: The system SHOULD support electronic shipment records to reduce unnecessary paper handling.

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
