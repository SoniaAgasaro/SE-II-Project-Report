# Feature: Schedule Generator

**Feature ID:** 3  
**Branch pattern:** `feature/3-schedule-generator`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs a "magic sorter" to auto-generate the round-robin schedule based on season rules.  
**Depends on:** [Feature 2 — Seasons](02-seasons.md), [Feature 4 — Teams & Locations](04-teams-rosters-locations.md)  

---

## User Stories

### US-3.1: Generate Games Automatically
**As an** Administrator  
**I want to** click a "Generate Schedule" button  
**So that** the system pairs teams home-and-away and assigns dates and locations.  

**Independent test:** Admin clicks Generate and sees 18 games per team populate the calendar.

### US-3.2: Reschedule a Specific Game
**As an** Administrator  
**I want to** manually reschedule a single game to a new date or location  
**So that** I can handle rainouts or field conflicts.  

**Independent test:** Admin changes Game 5 from Tuesday to Friday at a different field.

### US-3.3: Publish Schedule to Public
**As an** Administrator  
**I want to** click "Publish Schedule"  
**So that** the games become visible to the public and referees are notified.  

**Independent test:** Admin publishes the schedule and it appears on the public portal.

### US-3.4: Mark Game as Completed/Done
**As an** Administrator or Manager  
**I want to** mark a game as "Completed" after the results are entered  
**So that** the standings tabloids update.  

**Independent test:** Admin clicks "Complete" on a game and the win/loss record updates.

### US-3.5: Cancel a Game
**As an** Administrator  
**I want to** cancel a scheduled game (e.g., due to extreme weather)  
**So that** it doesn't count towards standings.  

**Independent test:** Admin clicks "Cancel Game" and it shows as cancelled for the public.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST generate a home-and-home round-robin schedule for all active teams.
- **FR-002**: System MUST automatically assign available referees to the generated games and send notification emails.
- **FR-003**: System MUST mark games as "Done/Completed" once results are recorded.
- **FR-004**: System MUST update standings tabloids immediately upon game completion.

---

## Key Entities
- **Game**: The scheduled matchup.
- **Standings**: Calculated records (Wins/Losses/Ties).

---

## Initial Data Model

### Game
| Attribute    | Type    | Description                     |
|--------------|---------|---------------------------------|
| `GameID`     | Integer | Unique identifier               |
| `SeasonID`   | Integer | Reference to Season             |
| `HomeTeamID` | Integer | Reference to Home Team          |
| `AwayTeamID` | Integer | Reference to Away Team          |
| `LocationID` | Integer | Reference to Location           |
| `GameDate`   | DateTime| Scheduled date/time             |
| `Status`     | String  | Scheduled, Completed, Cancelled |

---

## Gherkin AC

### US-3.1 — Generate Games Automatically
#### Scenario: Generate schedule with magic sorter (happy path)
*   **Given** a season has 10 teams and play days configured
*   **When** the Admin clicks "Generate Schedule"
*   **Then** the system pairs teams, assigns locations, and schedules 18 games per team.

### US-3.2 — Reschedule a Specific Game
#### Scenario: Admin reschedules a game (edge case)
*   **Given** a game is scheduled for Tuesday at Field A
*   **When** the Admin changes it to Friday at Field B
*   **Then** the system updates the date and location
*   **And** notifies the assigned referees of the change.

### US-3.3 — Publish Schedule to Public
#### Scenario: Admin publishes schedule (happy path)
*   **Given** the schedule is in "Draft" status
*   **When** the Admin clicks "Publish"
*   **Then** the games become visible on the Public Portal.

### US-3.4 — Mark Game as Completed/Done
#### Scenario: Game is marked completed (happy path)
*   **Given** results have been entered for a game
*   **When** the Admin clicks "Mark as Completed"
*   **Then** the game status is updated and standings are recalculated.

### US-3.5 — Cancel a Game
#### Scenario: Admin cancels a game (edge case)
*   **Given** a game is scheduled
*   **When** the Admin cancels it
*   **Then** the game status changes to "Cancelled" and doesn't affect standings.

---

## Screen Requirements

### SR-001: Schedule Generator Screen
**Authorized users:** League Owner (Admin)

**Display:**
- Season Name
- Status (Ready/Not Ready)
- Calendar View of Games

**Actions:**
- "Generate Schedule" Button
- "Publish Schedule" Button

**Behavior:**
- The system displays a loading spinner while generating.
- Once complete, the games appear on the calendar.
- Admin must click "Publish" for it to appear on the Public Portal.