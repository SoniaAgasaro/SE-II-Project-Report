# Feature: Maintain Teams

**Feature ID:** 4  
**Branch pattern:** `feature/4-maintain-teams`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Managers and Admin need to manage teams and assign them to leagues/seasons.  
**Depends on:** [Feature 3 — Maintain Seasons](03-maintain-seasons.md), [Feature 6 — Maintain Locations](06-maintain-locations.md)  

---

## User Stories

### US-4.1: Register a Team
**As a** Manager  
**I want to** register my team and assign a home location  
**So that** my team can participate in the league.  

**Independent test:** Manager logs in, creates "Team A", sets their home field, and adds them to the Fall Season.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow a Manager to create a team and assign themselves as the owner/manager.
- **FR-002**: System MUST require a Home Location (Field) for every team.
- **FR-003**: System MUST allow the Admin to enroll teams into a specific Season.
- **FR-004**: System MUST NOT allow a Manager to edit teams they do not own.
- **FR-005**: System MUST NOT allow a team to be deleted if they have games scheduled.

---

## Key Entities
- **Team**: Represents a group of players. Owned by a Manager, assigned to a Location.

---

## Initial Data Model

### Teams table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `manager_id` | INTEGER FK | Required, Links to Users |
| `location_id` | INTEGER FK | Required, Links to Locations |
| `name` | VARCHAR | Required |
| `is_active` | BOOLEAN | Default true |

---

## Gherkin AC

### US-4.1 — Register a Team
#### Scenario: Manager creates a team (happy path)
*   **Given** a Manager is logged in
*   **When** they enter a team name and select a valid home location
*   **Then** the team is created and visible on their dashboard.

#### Scenario: Manager tries to edit another team (failure)
*   **Given** Manager A is logged in
*   **When** they attempt to edit Manager B's team via URL manipulation
*   **Then** the system denies access and displays "Unauthorized".

## Screen Requirements
- **Team Roster View (Manager View):** A dashboard showing the team name, home location, and a "Manage Roster" button.
- **Team Registration Form:** Input for Team Name and a Dropdown for Home Location (populated from active Locations).
- **Team Assignment View (Admin View):** A list of teams with a checkbox to enroll them in a specific active Season.