# Feature6: Employee Maintenance
**Feature ID:** 6
**Branch pattern:** `feature/6-employee-maintenance`
**Created:** 2026-09-28
**Input:** Maintaining employees who work in the office, warehouse, or truck drivers

## User Stories

### US-6.1: Add an employee
**As an** authorized office employee
**I want to** add an employee
**So that** I make the employee available to the system

### US-6.2: Edit an employee
**As an** authorized office employee
**I want to** edit an employee
**So that** I keep the employee information current

### US-6.3: Delete an employee
**As an** authorized office employee
**I want to** delete an employee
**So that** I remove an employee who is nolonger working for the warehouse/company


## Functional Requirements

- **FR-001**: The system MUST allow an authorized office employee to add an employee
- **FR-002**: The system MUST allow an authorized office employee to edit an employee
- **FR-003**: The system MUST allow an authorized office employee to remove an employee
- **FR-004**: The system MUST identify the employee's work type as office, warehouse, or truck driver when that information is maintained


## Acceptance Criteria

### US-6.1 — Add an employee

#### Scenario: An employee can be added
* **Given** the authorized employee enters employee's information
* **When** the authorized employee saves the employee's information
* **Then** the new employee is available in the system

### US-6.2 — Edit an employee

#### Scenario: An employee's information can be edited
* **Given** the authorized employee edits employee's information
* **When** the authorized employee saves the employee's information
* **Then** the employee's information is maintained as current

### US-6.3 — Delete an employee

#### Scenario: An employee can be deleted
* **Given** the authorized employee removes/deletes an employee
* **When** the authorized employee saves the record
* **Then** the employee is removed from the system
