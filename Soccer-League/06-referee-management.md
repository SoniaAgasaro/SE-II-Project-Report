# Feature: Maintain Users & Referees

**Feature ID:** 7  
**Branch pattern:** `feature/7-maintain-users`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs to manage system access, assign roles, and track referee qualifications.  
**Depends on:** [Feature 1 — Maintain Sports](01-maintain-sports.md)  

---

## User Stories

### US-7.1: Manage Users and Roles
**As an** Administrator  
**I want to** assign roles (Admin, Manager, Referee) to users  
**So that** they have the correct permissions in the system.  

**Independent test:** Admin can invite a user and assign them the "Manager" role.

### US-7.2: Define Referee Qualifications
**As an** Administrator  
**I want to** specify which sports and roles (e.g., Center, Line) a Referee is qualified for  
**So that** I only assign them to games they can actually officiate.  

**Independent test:** Admin can mark a referee as qualified for "Soccer - Center Ref".

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow the Admin to create user accounts and assign roles.
- **FR-002**: System MUST enforce Role-Based Access Control (RBAC).
- **FR-003**: System MUST allow the Admin to define a Referee's qualified sports.
- **FR-004**: System MUST allow the Admin to define a Referee's qualified roles (Center, AR, etc.).
- **FR-005**: System MUST allow a Referee to be qualified for multiple sports/roles.
- **FR-006**: System MUST prevent a deactivated user from logging in.

---

## Key Entities
- **User**: A system account. Can have roles.
- **Referee Qualification**: Links a Referee to a Sport and a Role type.

---

## Initial Data Model

### `Users` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `email` | VARCHAR | Required, Unique |
| `password_hash` | VARCHAR | Required |
| `role` | VARCHAR | Admin, Manager, Referee |
| `is_active` | BOOLEAN | Default true |

### `Ref_qualifications` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `user_id` | INTEGER FK | Links to Users |
| `sport_id` | INTEGER FK | Links to Sports |
| `role_type` | VARCHAR | Center, Line, Umpire |

---

## Gherkin AC

### US-7.1 — Manage Users and Roles
#### Scenario: Admin creates a Manager (happy path)
*   **Given** the Admin is on the User Management page
*   **When** they invite "manager@email.com" and assign the Manager role
*   **Then** the user is created and granted Manager permissions.

### US-7.2 — Define Referee Qualifications
#### Scenario: Admin assigns qualifications (happy path)
*   **Given** the Admin is viewing a Referee's profile
*   **When** they select "Soccer" and "Center Ref"
*   **Then** the Referee can now be assigned to Soccer games as a Center Ref.

#### Scenario: Assigning unqualified ref to game (edge case)
*   **Given** a Referee is only qualified for Softball
*   **When** the Admin tries to assign them to a Soccer game
*   **Then** the system blocks the assignment and shows an error.

## Screen Requirements
- **User Management View:** A table listing users, their Email, Role, and Active Status.
- **Referee Qualification View:** A profile page showing the Referee's name, with a checklist of Sports (Soccer, Basketball, etc.) and a checklist of Roles (Center, Line, Umpire) for each sport.