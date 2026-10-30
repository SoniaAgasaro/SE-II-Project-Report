# Feature: Deliver Customer Orders

**Feature ID:** 16
**Branch pattern:** `feature/16-deliver-customer-orders`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Record delivery of shipped customer orders, delivered quantities, and confirmation that the customer received the shipment.

## User Stories

### US-16.1: View deliveries assigned to a driver
**As a** truck driver
**I want to** view the orders assigned for delivery
**So that** know which shipments must be delivered

**Priority:** P1
**Independent test:** Verify that the system supports the ability to view the orders assigned for delivery.
**Acceptance scenarios:** see US-16.1 under Gherkin AC

### US-16.2: Record delivery outcome
**As a** truck driver
**I want to** record delivery date and outcome
**So that** keep delivery status current

**Priority:** P1
**Independent test:** Verify that the system supports the ability to record delivery date and outcome.
**Acceptance scenarios:** see US-16.2 under Gherkin AC

### US-16.3: Confirm quantities received
**As a** truck driver or receiving customer representative
**I want to** record the quantities the customer received and confirmation
**So that** identify delivery differences

**Priority:** P1
**Independent test:** Verify that the system supports the ability to record the quantities the customer received and confirmation.
**Acceptance scenarios:** see US-16.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST make shipped orders available to delivery operations.
- **FR-002**: The system MUST associate delivery activity with the customer order, shipment, and driver when known.
- **FR-003**: The system MUST record the delivery date and delivery outcome.
- **FR-004**: The system MUST record delivered quantity for each item when available.
- **FR-005**: The system MUST record confirmation that the customer received the order, including the receiving person when available.
- **FR-006**: The system MUST allow delivered quantities to be compared with shipped quantities.
- **FR-007**: The system MUST retain delivery confirmation and discrepancy information.

## Assumptions

- Drivers use mobile devices or tablets in their trucks.
- A shipment can be successfully delivered, partially delivered, or refused.
- Customer signature or receiver name is captured for confirmation.

## Edge Cases

- Customer refuses the delivery.
- Delivered quantity is less than shipped quantity (e.g., boxes lost in transit).
- Driver cannot find the delivery location.
- System goes offline while the driver is on the road (requires offline mode sync).

## Success Criteria

- Drivers have a clear list of assigned stops.
- Delivery statuses (Delivered, Failed, Partial) are accurately recorded.
- Discrepancies are immediately visible to office staff for follow-up.

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

## Data Ownership

- **Delivery** is owned by the transportation/delivery function.
- Drivers write to Delivery records. Office staff and managers have read access.
- The **Shipment** status is updated to "Completed" upon successful delivery.

## API Requirements

- `GET /deliveries?driver_id={id}` — get assigned deliveries.
- `POST /deliveries/{id}/status` — update status (Delivered/Failed).
- `POST /deliveries/{id}/lines` — record actual delivered quantities.

## Screen Requirements

- **Driver Delivery List**: List of assigned shipments with customer name and address.
- **Delivery Detail Screen**: Items, Qty Shipped, [Input] Qty Delivered, Receiver Name, Delivery Status dropdown.
- "Confirm Delivery" button.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Gherkin scenarios pass.
- Offline capability (if required by NFRs) is tested.
- Screen reviewed against UI mockups.

## Out of Scope

- Real-time GPS routing or turn-by-turn navigation.
- Signature capture hardware integration (unless required by an NFR).