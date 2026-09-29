# Feature10: Customer Order Maintenance
**Feature ID:** 10
**Branch pattern:** `feature/10-customer-order-maintenance`
**Created:** 2026-09-28
**Input:** Maintaining customer orders received by the warehouse, receive cutomer orders so they can be picked, shipped, and delivered, Pick the items requested by customer, verify package and ship the customer order, record delivery of customer orders, and confirmation of the quantity received

## User Stories

### US-10.1: Add a customer order
**As a** office employee
**I want to** add a customer order
**So that** I record what a customer wants to purchase

### US-10.2: Edit a customer order
**As a** office employee
**I want to** edit a customer order
**So that** I correct or update the order before processing

### US-10.3: Delete a customer order
**As a** office employee
**I want to** delete a customer order from the system
**So that** I remove an order that should no longer be maintained in the system

### US-10.4: Receive a customer order
**As a** office employee
**I want to** record a customer's order
**So that** I start fulfillment of the customer order

### US-10.5: Pick items on a customer order
**As a** warehouse employee
**I want to** pick the requested items
**So that** I prepare the order for shipment

### US-10.6: Record picked quantity
**As a** warehouse employee
**I want to** record the actual quantity picked
**So that** I identify shortages before shipping

### US-10.7: Ship a customer order
**As a** warehouse employee
**I want to** verify and package a picked order
**So that** I send the order to the customer

### US-10.8: Prepare shipment documentation
**As a** warehouse employee
**I want to** prepare a Bill of Lading
**So that** I document what is being shipped

### US-10.9: Deliver a customer order
**As a** truck driver
**I want to** deliver a customer shipment
**So that** I complete the delivery

### US-10.10: Confirm delivery
**As a** truck driver or receiving customer representative
**I want to** record confirmation of the order received
**So that** I document what the customer actually received

### US-10.11: Review delivered quantities
**As a** warehouse manager
**I want to** view delivered quantities for customer shipments
**So that** I monitor what customers received

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add a customer order.
- **FR-002**: The system MUST allow an authorized office employee to edit a customer order.
- **FR-003**: The system MUST allow an authorized office employee to delete a customer order.
- **FR-004**: The system MUST associate a customer order with a customer.
- **FR-005**: The system MUST record the item and quantity ordered for each customer order line.
- **FR-006**: The system MUST allow an authorized employee to receive a customer order.
- **FR-007**: The system MUST record the customer, order date, PO number, items, and quantities provided by the customer order information.
- **FR-008**: The system MUST make a received customer order available for picking.
- **FR-009**: The system MUST show the items and quantities to be picked for a customer order.
- **FR-010**: The system MUST allow a warehouse employee to record the quantity picked for each item.
- **FR-011**: The system MUST allow the picked quantity to be less than the ordered quantity when insufficient inventory is available.
- **FR-012**: The system MUST retain the actual picked quantity for the customer order.
- **FR-013**: The system MUST support verification of the item being picked using its product information.
- **FR-014**: The system MUST allow an authorized warehouse employee to verify a picked customer order before shipment.
- **FR-015**: The system MUST allow an authorized warehouse employee to record that the order has been packaged for shipment.
- **FR-016**: The system MUST support a Bill of Lading for a customer shipment.
- **FR-017**: The system MUST record the quantity shipped for the customer order.
- **FR-018**: The system MUST associate the shipment with the customer order and customer.
- **FR-019**: The system MUST allow a driver to record delivery information for a customer order.
- **FR-020**: The system MUST record the quantity delivered for each item when delivery information is available.
- **FR-021**: The system MUST record confirmation that the customer received the order.
- **FR-022**: The system MUST make delivered quantity available for comparison with the shipped quantity.
- **FR-023**: The system MUST provide the warehouse manager with delivered quantity information.
- **FR-024**: The system MUST allow delivered quantities to be associated with the corresponding customer order and item.
- **FR-025**: The system MUST support comparing delivered quantity with the quantity shipped.


## Acceptance Criteria

### US-10.1 — Add a customer order

#### Scenario: A customer order can be added
* **Given** the employee enters the customer and ordered items
* **When** the employee saves the order
* **Then** the customer order is available for processing

### US-10.2 — Receive a customer order

#### Scenario: A customer order becomes available for fulfillment
* **Given** a valid customer order is received
* **When** the order is saved
* **Then** the order is available to the picking process

### US-10.3 — Pick items on a customer order

#### Scenario: A customer order is picked
* **Given** a customer order is ready for picking
* **When** the warehouse employee records quantities picked
* **Then** the system stores the actual picked quantities for the order

### US-10.4 — Ship a customer order

#### Scenario: A picked order is shipped
* **Given** the customer order has been picked
* **When** the employee verifies and packages the order and records shipment
* **Then** the system records the shipment and its quantity

### US-10.5 — Deliver a customer order

#### Scenario: A delivery is confirmed
* **Given** a driver delivers a customer order
* **When** delivery information and received quantities are recorded
* **Then** the system stores the delivery confirmation and delivered quantity

### US-10.6 — Review delivered quantities

#### Scenario: Delivered quantities can be reviewed
* **Given** a manager requests delivered quantity information
* **When** the system retrieves recorded delivery quantities
* **Then** the manager can see delivered quantities associated with the shipment/order
