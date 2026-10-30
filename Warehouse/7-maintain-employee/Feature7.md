# Feature: Employee Maintenance

**Feature ID:** 7
**Branch pattern:** `feature/7-employee-maintenance`
**Status:** Draft
**Created:** 2026-10-13
**Input:** Maintain employee information and distinguish office, warehouse, and truck-driver roles.

## User Stories

### US-7.1: Add an employee
**As a** authorized office employee
**I want to** add an employee record
**So that** identify people who perform warehouse work

**Priority:** P1
**Independent test:** Verify that the system supports the ability to add an employee record.
**Acceptance scenarios:** see US-7.1 under Gherkin AC

### US-7.2: Update employee information
**As a** authorized office employee
**I want to** update an employee record
**So that** keep employee information current

**Priority:** P1
**Independent test:** Verify that the system supports the ability to update an employee record.
**Acceptance scenarios:** see US-7.2 under Gherkin AC

### US-7.3: Deactivate an employee
**As a** authorized office employee
**I want to** deactivate an employee who no longer works for the company
**So that** prevent future assignment while preserving activity history

**Priority:** P1
**Independent test:** Verify that the system supports the ability to deactivate an employee who no longer works for the company.
**Acceptance scenarios:** see US-7.3 under Gherkin AC

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add, update, and deactivate employee records.
- **FR-002**: The system MUST identify an employee as office staff, warehouse staff, or truck driver when applicable.
- **FR-003**: The system MUST associate receiving, inventory adjustment, picking, shipping, and delivery actions with the employee who performed them when that information is captured.
- **FR-004**: The system MUST preserve historical transaction records associated with a deactivated employee.
- **FR-005**: The system MUST prevent a deactivated employee from logging in or being assigned to new tasks.

## Assumptions

- Every person interacting with the system has an Employee record.
- Role determines what system functions the employee can access.
- An employee may hold multiple roles if necessary (e.g., warehouse staff who also drives).

## Edge Cases

- Deactivating an employee while they have active tasks assigned.
- Adding an employee without specifying a role.
- Duplicate employee IDs or names.
- Reassigning tasks from a deactivated employee.

## Success Criteria

- Employees can be created with specific roles.
- Historical records (like who picked an order) remain intact after deactivation.
- Role-based access controls function correctly based on the assigned role.

## Key Entities

- **Employee**: a person who performs work for the company.
- **Employee Role**: the type of work the employee performs.

## Initial Data Model

- Employee: employee_id, name, contact information, role, active_status.

## Gherkin AC

### US-7.1 — Add an employee

#### Scenario: Employee role is recorded
* **Given** an authorized employee is adding a worker
* **When** the employee selects office, warehouse, or truck-driver role and saves
* **Then** the system stores the employee with the selected role

### US-7.2 — Update employee information

#### Scenario: Deactivated employee remains in history
* **Given** an employee has performed recorded warehouse actions
* **When** an authorized user deactivates the employee
* **Then** the system prevents new assignment where applicable but preserves the employee's historical actions

## Data Ownership

- **Employee** is owned by the office/HR/administrative function.
- Only authorized office employees may create, update, or deactivate employees.
- All operational features (receiving, picking, etc.) MAY read employee data to record task ownership.

## API Requirements

- `GET /employees` — list employees (filter: `active`, `role`).
- `GET /employees/{id}` — retrieve an employee.
- `POST /employees` — create an employee.
- `PUT /employees/{id}` — update an employee.
- `PATCH /employees/{id}/deactivate` — deactivate.
- JSON bodies; server-side validation of role and required fields.

## Screen Requirements

- **Employee Maintenance screen**: list with search and role filter; Add/Edit form with name, contact info, role selection.
- Inline validation and deactivate confirmation.

## Definition of Done

- All functional requirements implemented and demonstrated.
- Validation and deactivation scenarios pass their Gherkin AC.
- Role enforcement tested across at least two other features (e.g., picking, office).
- Screen reviewed against UI mockups.

## Out of Scope

- Payroll and HR benefits.
- Time-clock or shift-scheduling features.