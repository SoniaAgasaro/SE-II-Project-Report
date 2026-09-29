# Feature7: Route Maintenance
**Feature ID:** 7
**Branch pattern:** `feature/7-route-maintenance`
**Created:** 2026-09-28
**Input:** Maintaining delivery routes and the customer included on each route

## User Stories

### US-7.1: Add a route
**As an** office employee
**I want to** add a route and its customer list
**So that** I organize deliveries

### US-7.2: Edit a route
**As an** office employee
**I want to** edit a route
**So that** I keep delivery information current

### US-7.3: Delete an employee
**As an** office employee
**I want to** delete a route
**So that** I remove a route that nolonger has customers to deliver at


## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add a route
- **FR-002**: The system MUST allow an authorized office employee to edit a route
- **FR-003**: The system MUST allow an authorized office employee to remove a route
- **FR-004**: The system MUST maintain customers associated with each route
- **FR-005**: The system MUST allow an authorized office employee to add, edit, or remove more customers on a saved route


## Acceptance Criteria

### US-7.1 — Add a route

#### Scenario: An route can be added
* **Given** the authorized employee enters route and the customers on that route
* **When** the authorized employee saves the route's information
* **Then** the new route is available for delivery operations

### US-7.2 — Edit a route

#### Scenario: An route can be dited
* **Given** the authorized employee edits the route and the customers on that route
* **When** the authorized employee saves the new route's information
* **Then** the route's information is saved as current

### US-7.3 — Delete a route

#### Scenario: An route can be deleted
* **Given** the authorized employee removes/deletes a route
* **When** the authorized employee saves the record
* **Then** the route is removed from delivery operations
