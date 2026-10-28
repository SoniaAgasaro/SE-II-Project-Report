# Feature: User Administration

**Feature ID:** 8  
**Branch pattern:** `feature/8-user-administration`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs to manage users and define which sports/roles a referee is qualified for.  
**Depends on:** [Feature 1 — Sports](01-leagues-and-sports.md)  

---

## User Stories

### US-8.1: Add Users and Set Roles
**As an** Administrator  
**I want to** invite users (Admin, Manager, Referee) and set their initial roles  
**So that** they can log into the system and access their specific screens.  

**Independent test:** Admin invites a new Manager and sets their role to "Manager".

### US-8.2: Update User Roles
**As an** Administrator  
**I want to** change a user's role (e.g., promote a Manager to Admin)  
**So that** system permissions adjust automatically.  

**Independent test:** Admin changes a user's role from Manager to Admin.

### US-8.3: Deactivate/Remove a User
**As an** Administrator  
**I want to** deactivate a user's account  
**So that** they can no longer log in, but their historical records remain.  

**Independent test:** Admin deactivates a referee who quit.

### US-8.4: Set/Update Referee Qualifications
**As an** Administrator  
**I want to** check the boxes for which sports and roles (Center, Line) a Ref is qualified for  
**So that** the system only assigns them to games they can actually officiate.  

**Independent test:** Admin checks "Soccer" and "Center Ref" for a referee.


---

## Requirements

### Functional Requirements
- **FR-001**: System MUST enforce Role-Based Access Control (Admin, Manager, Referee).
- **FR-002**: System MUST prevent a deactivated user from logging in.
- **FR-003**: System MUST allow the Admin to specify a Ref's qualified sports and roles.

---

## Key Entities
- **User**: The system account.
- **RefQualification**: Links a Ref to a Sport and Role.

---

## Initial Data Model

### User
| Attribute | Type    | Description             |
|-----------|---------|-------------------------|
| `UserID`  | Integer | Unique identifier       |
| `Email`   | String  | Login email             |
| `Role`    | String  | Admin, Manager, Referee |
| `Status`  | String  | Active/Inactive         |

### RefQualification
| Attribute         | Type    | Description          |
|-------------------|---------|----------------------|
| `QualificationID` | Integer | Unique identifier    |
| `UserID`          | Integer | Reference to User    |
| `SportID`         | Integer | Reference to Sport   |
| `RoleType`        | String  | Center, Line, Umpire |

---

## Gherkin AC

### US-8.1 — Add Users and Set Roles
#### Scenario: Admin creates a Manager (happy path)
*   **Given** the Admin is on the User Management screen
*   **When** they enter an email and set the role to "Manager"
*   **Then** the user is created and receives a setup email.

### US-8.2 — Update User Roles
#### Scenario: Admin changes role (happy path)
*   **Given** a user is a Manager
*   **When** the Admin changes the role to Admin
*   **Then** the user now has access to Admin screens.

### US-8.3 — Deactivate/Remove a User
#### Scenario: Admin deactivates user (edge case)
*   **Given** a user is active
*   **When** the Admin deactivates them
*   **Then** the user cannot log in
*   **And** their past game history remains.

### US-8.4 — Set/Update Referee Qualifications
#### Scenario: Admin sets ref qualifications (happy path)
*   **Given** a Ref's profile is open
*   **When** the Admin checks "Soccer" and "Center Ref"
*   **Then** the Ref becomes eligible for Soccer Center assignments.

---

## Screen Requirements

### SR-001: User Management List
**Authorized users:** League Owner (Admin)

**Display:**
- List of Users
- Role
- Status

**Actions:**
- Edit User
- Deactivate User

### SR-002: Referee Qualification Screen
**Authorized users:** League Owner (Admin)

**Display:**
- Referee Name
- List of Sports (Checkboxes)
- List of Roles per Sport

**Actions:**
- Save Qualifications

**Behavior:**
- The system must only allow assigning a referee to a game if their qualifications match.