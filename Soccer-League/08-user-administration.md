# Feature: Game Management (Scores, Stats, and Adjustments)

**Feature ID:** 9  
**Branch pattern:** `feature/9-game-management`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Managers need to enter game scores and stats, while the Admin needs the ability to change locations if fields are rained out.  
**Depends on:** [Feature 8 — Generate Schedule](08-generate-schedule.md)  

---

## User Stories

### US-9.1: Enter Game Scores and Stats
**As a** Home Manager  
**I want to** enter the final score and my players' stats after the game  
**So that** the league standings and player records are updated.  

**Independent test:** Home Manager logs in, enters a 3-2 score, and assigns 2 goals to a player.

### US-9.2: Modify Game Location
**As an** Administrator  
**I want to** change the location of a scheduled game  
**So that** I can handle rainouts or double-booking issues.  

**Independent test:** Admin can change a game from "Field A" to "Field B".

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow the Home Manager to submit the final score for a scheduled game.
- **FR-002**: System MUST allow the Home Manager to input sport-specific stats for players on both teams (optional but encouraged).
- **FR-003**: System MUST lock the score and stats from further edits by the Manager once submitted (Admin can still override).
- **FR-004**: System MUST allow the Admin to change the `location_id` of any scheduled game.
- **FR-005**: System MUST NOT allow a Manager to enter a score for a game they are not managing.

---

## Key Entities
- **Result**: The final score of a game.
- **Stat**: A specific record of a player's performance in a game.

---

## Initial Data Model

### `results` table
| Field | Type | Rules |
|-------|------|-------|
| `game_id` | INTEGER FK | Links to Games |
| `home_score` | INTEGER | Required, >= 0 |
| `away_score` | INTEGER | Required, >= 0 |

### `stats` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `game_id` | INTEGER FK | Links to Games |
| `player_id` | INTEGER FK | Links to Players |
| `stat_type` | VARCHAR | E.g., "Goals", "Assists" |
| `stat_value` | INTEGER | Required |

---

## Gherkin AC

### US-9.1 — Enter Game Scores and Stats
#### Scenario: Manager enters final score (happy path)
*   **Given** the Home Manager is logged in and the game is marked "Completed"
*   **When** they enter a score of 3-2 and click Submit
*   **Then** the league standings update automatically
*   **And** the game status changes to "Final".

#### Scenario: Away manager tries to edit score (failure)
*   **Given** the Away Manager is logged in
*   **When** they attempt to edit the score submitted by the Home Manager
*   **Then** the system denies access and shows "Only the Home Manager can submit the score."

### US-9.2 — Modify Game Location
#### Scenario: Admin changes game location due to rain (happy path)
*   **Given** a game is scheduled at "Field A" which is flooded
*   **When** the Admin edits the game and selects "Field B"
*   **Then** the location is updated on the public schedule
*   **And** the assigned referees are notified of the change.