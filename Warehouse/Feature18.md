# Feature: Warehouse Reporting and Exceptions

**Feature ID:** 18
**Branch pattern:** `feature/18-warehouse-reporting-exceptions`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Provide the manager with information about out-of-stock items, supplier quantity differences, delivery discrepancies, and monthly shipped quantities.

## User Stories

### US-18.1: Report out-of-stock items
**As a** warehouse manager
**I want to** view items that have been out of stock
**So that** I identify inventory risks

**Independent test:** Verify that the system supports the ability to view items that have been out of stock.

### US-18.2: Report supplier discrepancies
**As a** warehouse manager
**I want to** view supplier orders where received quantities differ from ordered quantities
**So that** I identify supplier fulfillment problems

**Independent test:** Verify that the system supports the ability to view supplier orders where received quantities differ from ordered quantities.

### US-18.3: Report delivery discrepancies
**As a** warehouse manager
**I want to** view deliveries where delivered quantities differ from shipped quantities
**So that** I investigate delivery problems

**Independent test:** Verify that the system supports the ability to view deliveries where delivered quantities differ from shipped quantities.

### US-18.4: Review monthly shipped quantities
**As a** warehouse manager
**I want to** view quantities shipped by item and month
**So that** I understand shipment volume

**Independent test:** Verify that the system supports the ability to view quantities shipped by item and month.

## Functional Requirements

- **FR-001**: The system MUST identify items recorded as out of stock.
- **FR-002**: The system MUST report supplier-order lines where quantity received differs from quantity ordered.
- **FR-003**: The system MUST report delivery lines where quantity delivered differs from quantity shipped.
- **FR-004**: The system MUST provide shipped quantity information grouped by month and item.
- **FR-005**: The system MUST allow report results to be traced to the related item, order, shipment, or delivery record where applicable.

## Key Entities

- **Inventory Balance**: on-hand stock information.
- **Supplier Order and Receiving Record**: ordered and received quantities.
- **Shipment and Delivery**: shipped and delivered quantities.
- **Item**: product shown in reports.

## Initial Data Model

- Out-of-Stock Result: item_id, warehouse_id, status date or reporting date.
- Supplier Discrepancy: supplier_order_id, item_id, quantity_ordered, quantity_received, difference.
- Delivery Discrepancy: shipment_id, delivery_id, item_id, quantity_shipped, quantity_delivered, difference.
- Monthly Shipment Summary: month, item_id, quantity_shipped.

## Gherkin AC

### US-18.1 — Report out-of-stock items

#### Scenario: Out-of-stock item appears in report
* **Given** an item's recorded available quantity is zero
* **When** the manager opens the out-of-stock report
* **Then** the item appears with its identifier and stock status

### US-18.2 — Report supplier discrepancies

#### Scenario: Supplier discrepancy appears in report
* **Given** a supplier order line has different ordered and received quantities
* **When** the manager opens the supplier discrepancy report
* **Then** the order line appears with both quantities and their difference

### US-18.3 — Report delivery discrepancies

#### Scenario: Delivery discrepancy appears in report
* **Given** a delivery line has different shipped and delivered quantities
* **When** the manager opens the delivery discrepancy report
* **Then** the delivery line appears with both quantities and their difference

### US-18.4 — Review monthly shipped quantities

#### Scenario: Monthly quantities are summarized
* **Given** shipment records exist across one or more months
* **When** the manager requests the monthly shipped quantity report
* **Then** the system groups shipped quantities by month and item
