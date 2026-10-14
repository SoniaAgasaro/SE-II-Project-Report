# Feature: Route Maintenance

**Feature ID:** 8
**Branch pattern:** `feature/8-route-maintenance`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Maintain delivery routes and the customers assigned to each route.

## User Stories

### US-8.1: Add a route
**As an** office employee
**I want to** create a delivery route and assign customers
**So that** I organize customer deliveries

**Independent test:** Verify that the system supports the ability to create a delivery route and assign customers.

### US-8.2: Update a route
**As an** office employee
**I want to** change route details or its customer list
**So that** I keep delivery planning current

**Independent test:** Verify that the system supports the ability to change route details or its customer list.

### US-8.3: Deactivate a route
**As an** office employee
**I want to** deactivate a route that is no longer used
**So that** I preserve historical delivery information

**Independent test:** Verify that the system supports the ability to deactivate a route that is no longer used.

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add, update, and deactivate routes.
- **FR-002**: The system MUST associate customers with routes.
- **FR-003**: The system MUST allow a route's customer list to be updated.
- **FR-004**: The system MUST make route information available to delivery planning and delivery operations.
- **FR-005**: The system MUST preserve historical delivery records associated with a route.

## Key Entities

- **Route**: a planned delivery route.
- **Customer**: a customer assigned to a route.
- **Employee**: a driver who may be assigned to delivery work.

## Initial Data Model

- Route: route_id, route_name or route_code, active_status.
- Route Customer: route_customer_id, route_id, customer_id, sequence_number if route order is tracked.

## Gherkin AC

### US-8.1 — Add a route

#### Scenario: Route is created with customers
* **Given** customers exist in the system
* **When** an employee creates a route and assigns customers
* **Then** the system saves the route and its customer associations

### US-8.2 — Update a route

#### Scenario: Route customer list is changed
* **Given** a route already exists
* **When** an employee adds or removes a customer assignment
* **Then** the system stores the updated list

### US-8.3 — Deactivate a route

#### Scenario: Inactive route is not offered for new planning
* **Given** a route is marked inactive
* **When** an employee begins planning a new delivery
* **Then** the inactive route is not offered as an active route
