# Feature: Maintain Players

**Feature ID:** 5  
**Branch pattern:** `feature/5-maintain-players`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Managers need to add and remove players from their team rosters without Admin intervention.  
**Depends on:** [Feature 4 — Maintain Teams](04-maintain-teams.md)  

---

## User Stories

### US-5.1: Add Players to Roster
**As a** Manager  
**I want to** add players to my team's roster  
**So that** they can participate in games and accumulate stats.  

**Independent test:** Manager can add "John Doe" to their team roster.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow Managers to add players to their own team.
- **FR-002**: System MUST require a Player's First Name and Last Name.
- **FR-003**: System MUST allow Managers to remove a player from the active roster (soft delete) without deleting their historical stats.
- **FR-004**: System MUST allow a player's email address to be collected for notifications.
- **FR-005**: System MUST NOT impose a maximum roster size (as per business rules).

---

## Key Entities
- **Player**: Represents a person on a team. Belongs to a Team.

---

## Initial Data Model

### `Players` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `team_id` | INTEGER FK | Required, Links to Teams |
| `first_name` | VARCHAR | Required |
| `last_name` | VARCHAR | Required |
| `email` | VARCHAR | Optional |
| `is_active` | BOOLEAN | Default true |

---

## Gherkin AC

### US-5.1 — Add Players to Roster
#### Scenario: Manager adds a player (happy path)
*   **Given** a Manager is viewing their team roster
*   **When** they enter "Jane", "Smith", and "jane@email.com"
*   **Then** Jane Smith appears on the active roster.

#### Scenario: Manager removes a player (edge case)
*   **Given** Jane Smith has recorded stats
*   **When** the Manager clicks "Deactivate Player"
*   **Then** Jane is removed from the active roster
*   **And** her historical stats remain intact in past game logs.

## Screen Requirements
- **Roster List View:** A table listing Player Name, Email, Status (Active/Inactive), and a "Deactivate" button.
- **Add Player Form:** Text inputs for First Name, Last Name, and Email, with a "Save" button.