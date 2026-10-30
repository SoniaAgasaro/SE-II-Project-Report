# Feature: Route Maintenance

**Feature ID:** 8
**Branch pattern:** `feature/8-route-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Maintain delivery routes and the customers assigned to each route.

## User Stories

### US-8.1: Add a route
**As a** office employee
**I want to** create a delivery route and assign customers
**So that** organize customer deliveries

**Priority:** P1
**Independent test:** Verify that the system supports the ability to create a delivery route and assign customers.
**Acceptance scenarios:** see US-8.1 under Gherkin AC

### US-8.2: Update a route
**As a** office employee
**I want to** change route details or its customer list
**So that** keep delivery planning current

**Priority:** P1
**Independent test:** Verify that the system supports the ability to change route details or its customer list.
**Acceptance scenarios:** see US-8.2 under Gherkin AC

### US-8.3: Deactivate a route
**As a** office employee
**I want to** deactivate a route that is no longer used
**So that** preserve historical delivery information

**Priority:** P1
**Independent test:** Verify that the system supports the ability to deactivate a route that is no longer used.
**Acceptance scenarios:** see US-8.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add, update, and deactivate routes.
- **FR-002**: The system MUST associate customers with routes.
- **FR-003**: The system MUST allow a route's customer list to be updated.
- **FR-004**: The system MUST make route information available to delivery planning and delivery operations.
- **FR-005**: The system MUST preserve historical delivery records associated with a route.
- **FR-006**: The system MUST support sequencing of customers within a route.

## Assumptions

- Routes are geographical paths driven by truck drivers.
- A customer can be assigned to multiple routes (e.g., different days of the week).
- Only active routes are available for new delivery planning.

## Edge Cases

- Adding a customer to a route when the customer is inactive.
- Deactivating a route that has pending shipments assigned to it.
- Reordering customers within an existing route.
- Creating a route with no customers assigned yet.

## Success Criteria

- Routes can be created, updated, and deactivated.
- Customer lists and sequence numbers update correctly.
- Historical delivery data remains linked to deactivated routes.

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

## Data Ownership

- **Route** and **Route Customer** are owned by the office/administrative function.
- Only authorized office employees may create, update, or deactivate routes.
- Delivery and shipping features MAY read route data to assign shipments to drivers.

## API Requirements

- `GET /routes` — list routes (filter: `active`).
- `GET /routes/{id}` — retrieve a route and its customers.
- `POST /routes` — create a route.
- `PUT /routes/{id}` — update route details.
- `POST /routes/{id}/customers` — add/update route customer assignments.
- `PATCH /routes/{id}/deactivate` — deactivate.

## Screen Requirements

- **Route Maintenance screen**: list with search; Add/Edit form with route name/code, active status.
- **Route Customers sub-screen**: add/remove customers and set sequence order.
- Inline validation and deactivate confirmation.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Validation and deactivation scenarios pass their Gherkin AC.
- Inactive routes blocked from new delivery planning.
- Screen reviewed against UI mockups.

## Out of Scope

- GPS tracking or real-time route optimization.
- Automatic dispatch/assignment of routes to drivers.