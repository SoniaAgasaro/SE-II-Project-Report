# Feature: Delivered Quantity Reporting

**Feature ID:** 19
**Branch pattern:** `feature/19-delivered-quantity-reporting`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Report the quantities customers actually received and support comparison with quantities shipped.

## User Stories

### US-19.1: Review delivered quantities
**As a** warehouse manager
**I want to** view delivered quantities for customer shipments
**So that** I monitor what customers actually received

**Independent test:** Verify that the system supports the ability to view delivered quantities for customer shipments.

### US-19.2: Compare shipped and delivered quantities
**As a** warehouse manager
**I want to** compare quantities shipped with quantities delivered
**So that** I identify differences that need follow-up

**Independent test:** Verify that the system supports the ability to compare quantities shipped with quantities delivered.

## Functional Requirements

- **FR-001**: The system MUST provide delivered quantity information by item and customer order when delivery quantities have been recorded.
- **FR-002**: The system MUST associate delivered quantities with the related delivery, shipment, customer order, and item.
- **FR-003**: The system MUST support comparing delivered quantity with shipped quantity.
- **FR-004**: The system MUST make quantity differences available for follow-up.

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
