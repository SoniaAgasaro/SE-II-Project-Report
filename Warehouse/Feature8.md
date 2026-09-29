# Feature8: Warehouse Tracking
**Feature ID:** 8
**Branch pattern:** `feature/8-warehouse-tracking`
**Created:** 2026-09-28
**Input:** Providing manager informmation about quantity lows, differences and warehouse exceptions identified during operations

## User Stories

### US-8.1: Review out of stock items
**As an** warehouse manager
**I want to** view items that have been out of stock
**So that** I identify inventory issues or restock

### US-8.2: Review supplier quantity differences
**As an** warehouse manager
**I want to** view order records where received quantities differs from ordered quantities
**So that** I identify supplier shortages

### US-8.3: Review delivery quantity differences
**As an** warehouse manager
**I want to** view shipment where delivered quantity differs from shipped quantity
**So that** I identify delivery discrepancies

### US-8.4: Review monthly shipping quantities
**As an** warehouse manager
**I want to** view quantities shipped by month
**So that** I understand the shipping activity of the warehouse


## Functional Requirements

- **FR-001**: The system MUST identify items that have been out of stock
- **FR-002**: The system MUST identify supplier orders where quantity received differs from quantity ordered
- **FR-003**: The system MUST identify deliveries where quantity delivered differs from quantity shipped
- **FR-004**: The system MUST provide monthly shipping quantity information
- **FR-005**: The system MUST make a new order if the item is marked as a shortage in stock

## Initial Data Model

- Reporting data: item stock status, ordered/received quantities, shipped/delivered quantities, shipment date/month


## Acceptance Criteria

### US-8.1 — Review out of stock items

#### Scenario: Stock quantity is reported
* **Given** a warehouse manager views out os stock items
* **When** the manager opens the out of stock report
* **Then** the out of stock record of items appears

### US-8.2 — Review Supplier quantity difference

#### Scenario: Supplier quantity differences are reported
* **Given** the warehouse has receive quantity different from the ordered quantity
* **When** the manager opens an exception report
* **Then** the supplier orders appears as a quantity difference

### US-8.3 — Review delivery quantity difference

#### Scenario: Customer quantity differences are reported
* **Given** the warehouse has shipped quantity different from the customer order quantity 
* **When** the manager opens an exception report
* **Then** the customer shipped order quantity appears as a quantity difference

### US-8.4 — Review monthly shipping quantity

#### Scenario: Monthly shipments are reported
* **Given** the warehouse manager views the monthly shipping quantity
* **When** the manager opens an exception report
* **Then** the monthly shipments appear in monthly quantities
