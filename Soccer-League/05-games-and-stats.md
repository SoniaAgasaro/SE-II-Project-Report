# Feature: Maintain Locations

**Feature ID:** 6  
**Branch pattern:** `feature/6-maintain-locations`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs to manage the list of available fields/arenas to prevent double-booking.  
**Depends on:** None  

---

## User Stories

### US-6.1: Manage Locations
**As an** Administrator  
**I want to** add, edit, and deactivate game locations  
**So that** games can be assigned to valid, available fields.  

**Independent test:** Admin can add "Central Park Field 1" and mark "Old Gym" as inactive.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow the Admin to create a Location with a Name and Address.
- **FR-002**: System MUST allow the Admin to deactivate a Location if it is no longer usable (e.g., field destroyed).
- **FR-003**: System MUST prevent assigning a game to an inactive Location.
- **FR-004**: System MUST allow a Location to be shared by multiple teams.

---

## Key Entities
- **Location**: A physical field or court where games are played.

---

## Initial Data Model

### `Locations` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `name` | VARCHAR | Required |
| `address` | TEXT | Optional |
| `is_active` | BOOLEAN | Default true |

---

## Gherkin AC

### US-6.1 — Manage Locations
#### Scenario: Admin deactivates a location (happy path)
*   **Given** a location is active
*   **When** the Admin marks it inactive
*   **Then** the location cannot be selected for new games.

#### Scenario: Admin tries to deactivate a location with upcoming games (edge case)
*   **Given** a location has games scheduled for next week
*   **When** the Admin attempts to deactivate it
*   **Then** the system warns "This location has upcoming games. Please reassign them first."

## Screen Requirements
- **Location List View:** A table showing Location Name, Address, Status, and an "Edit" button.
- **Location Create/Edit Form:** Text inputs for Name and Address, and a toggle for Active Status. 