# Feature: Employee Maintenance

**Feature ID:** 7
**Branch pattern:** `feature/7-employee-maintenance`
**Status:** Draft
**Created:** 2026-09-28
**Updated:** 2026-10-13
**Input:** Maintain employee information and distinguish office, warehouse, and truck-driver roles.

## User Stories

### US-7.1: Add an employee
**As an** authorized office employee
**I want to** add an employee record
**So that** I identify people who perform warehouse work

**Independent test:** Verify that the system supports the ability to add an employee record.

### US-7.2: Update employee information
**As an** authorized office employee
**I want to** update an employee record
**So that** I keep employee information current

**Independent test:** Verify that the system supports the ability to update an employee record.

### US-7.3: Deactivate an employee
**As an** authorized office employee
**I want to** deactivate an employee who no longer works for the company
**So that** I prevent future assignment while preserving activity history

**Independent test:** Verify that the system supports the ability to deactivate an employee who no longer works for the company.

## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add, update, and deactivate employee records.
- **FR-002**: The system MUST identify an employee as office staff, warehouse staff, or truck driver when applicable.
- **FR-003**: The system MUST associate receiving, inventory adjustment, picking, shipping, and delivery actions with the employee who performed them when that information is captured.
- **FR-004**: The system MUST preserve historical transaction records associated with a deactivated employee.

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
