# Feature: Generate Season Schedule

**Feature ID:** 8  
**Branch pattern:** `feature/8-generate-schedule`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs the system to automatically generate a round-robin game schedule based on league parameters to save hours of manual spreadsheet work.  
**Depends on:** [Feature 3 — Maintain Seasons](03-maintain-seasons.md), [Feature 4 — Maintain Teams](04-maintain-teams.md), [Feature 6 — Maintain Locations](06-maintain-locations.md)  

---

## User Stories

### US-8.1: Auto-Generate Schedule
**As an** Administrator  
**I want to** click a button to generate a full season schedule based on the teams and play dates  
**So that** I don't have to manually figure out who plays who, where, and when.  

**Independent test:** Admin can trigger generation for a 10-team league and see 18 games per team scheduled on the correct days.

---

## Requirements

### Functional Requirements
- **FR-001**: The system MUST generate a round-robin schedule where every team plays every other team home and away (home-and-home).
- **FR-002**: The system MUST use the Season's configured play days (e.g., Tuesdays & Fridays) and start/end dates to distribute games.
- **FR-003**: The system MUST respect the minimum days between games rule per team (e.g., 3 days).
- **FR-004**: The system MUST assign the Home Team's location as the default game location.
- **FR-005**: If there is an odd number of teams, the system MUST automatically assign a "Bye" week to one team per cycle.
- **FR-006**: The system MUST NOT allow the Admin to generate a schedule if teams are not fully registered for the season.

---

## Key Entities
- **Game**: The generated matchup containing Home Team, Away Team, Date, Time, and Location.

---

## Initial Data Model

### `games` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `season_id` | INTEGER FK | Links to Seasons |
| `home_team_id` | INTEGER FK | Links to Teams |
| `away_team_id` | INTEGER FK | Links to Teams |
| `location_id` | INTEGER FK | Links to Locations |
| `game_date` | DATETIME | Required |
| `status` | VARCHAR | Scheduled, Completed, Cancelled |

---

## Gherkin AC

### US-8.1 — Auto-Generate Schedule
#### Scenario: Generate a standard round-robin schedule (happy path)
*   **Given** a league has 10 active teams
*   **And** the season is configured for Tuesdays and Fridays with a 3-day rest rule
*   **When** the Admin clicks "Generate Schedule"
*   **Then** the system creates exactly 90 games (18 per team)
*   **And** no team plays twice in one day
*   **And** every matchup has a Home and Away game.

#### Scenario: Odd number of teams (edge case)
*   **Given** a league has 9 active teams
*   **When** the Admin clicks "Generate Schedule"
*   **Then** the system creates games for 8 teams
*   **And** assigns a "Bye" to the 9th team for that cycle.

#### Scenario: Admin tries to generate schedule with missing parameters (failure)
*   **Given** the season does not have any play days selected
*   **When** the Admin clicks "Generate Schedule"
*   **Then** the system blocks the action and displays "Please configure play days for this season."

---

## Screen Requirements
- **Season Detail View:** A prominent "Generate Schedule" button.
- **Schedule Preview:** A calendar or list view of the generated games before they are finalized, allowing the Admin to review.