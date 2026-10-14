# Feature: Deliver Customer Orders

**Feature ID:** 16
**Branch pattern:** `feature/16-deliver-customer-orders`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Record delivery of shipped customer orders, delivered quantities, and confirmation that the customer received the shipment.

## User Stories

### US-16.1: View deliveries assigned to a driver
**As a** truck driver
**I want to** view the orders assigned for delivery
**So that** I know which shipments must be delivered

**Independent test:** Verify that the system supports the ability to view the orders assigned for delivery.

### US-16.2: Record delivery outcome
**As a** truck driver
**I want to** record delivery date and outcome
**So that** I keep delivery status current

**Independent test:** Verify that the system supports the ability to record delivery date and outcome.

### US-16.3: Confirm quantities received
**As a** truck driver or receiving customer representative
**I want to** record the quantities the customer received and confirmation
**So that** I identify delivery differences

**Independent test:** Verify that the system supports the ability to record the quantities the customer received and confirmation.

## Functional Requirements

- **FR-001**: The system MUST make shipped orders available to delivery operations.
- **FR-002**: The system MUST associate delivery activity with the customer order, shipment, and driver when known.
- **FR-003**: The system MUST record the delivery date and delivery outcome.
- **FR-004**: The system MUST record delivered quantity for each item when available.
- **FR-005**: The system MUST record confirmation that the customer received the order, including the receiving person when available.
- **FR-006**: The system MUST allow delivered quantities to be compared with shipped quantities.
- **FR-007**: The system MUST retain delivery confirmation and discrepancy information.

## Key Entities

- **Delivery**: the delivery event for a shipment.
- **Shipment**: the order and quantities sent out.
- **Customer**: recipient of the delivery.
- **Employee**: driver delivering the order.

## Initial Data Model

- Delivery: delivery_id, shipment_id, driver_employee_id, delivery_date, delivery_status, received_by, confirmation_details.
- Delivery Line: delivery_line_id, delivery_id, item_id, quantity_delivered.

## Gherkin AC

### US-16.1 — View deliveries assigned to a driver

#### Scenario: Driver views assigned deliveries
* **Given** shipments have been assigned for delivery
* **When** the driver opens the delivery list
* **Then** the system displays the assigned shipments and customer information

### US-16.2 — Record delivery outcome

#### Scenario: Delivery is confirmed
* **Given** a shipment has been delivered to a customer
* **When** the driver records the delivery date and confirmation
* **Then** the system stores the delivery confirmation and updates delivery status

### US-16.3 — Confirm quantities received

#### Scenario: Delivered quantity differs from shipped quantity
* **Given** a shipment has a recorded shipped quantity
* **When** the driver records the quantity actually delivered
* **Then** the system retains the delivered quantity and makes the difference available for reporting
