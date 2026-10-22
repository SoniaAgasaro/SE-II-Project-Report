# Feature: Maintain Seasons

**Feature ID:** 2  
**Branch pattern:** `feature/2-maintain-seasons`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs to define the specific timeframes and rules for a season.  
**Depends on:** [Feature 1 — Maintain Leagues & Sports](01-leagues-and-sports.md)  

---

## User Stories

### US-2.1: Configure Season Rules
**As an** Administrator  
**I want to** set the start/end dates, play days, and locations for a season  
**So that** the scheduling engine knows the parameters for generating games.  

**Independent test:** Admin can create a season starting Sept 1, ending Nov 1, playing only on Tuesdays.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST require a Start Date, End Date, and at least one Play Day (e.g., Tuesday).
- **FR-002**: System MUST allow the Admin to select which Locations are available for this season.
- **FR-003**: System MUST lock season rules once the schedule has been generated.

---

## Key Entities
- **Season**: A timeframe containing scheduling rules.

---

## Initial Data Model

### Season
| Attribute | Type | Description |
|-----------|------|-------------|
| `SeasonID` | Integer | Unique identifier for the season |
| `LeagueID` | Integer | Reference to League |
| `Name` | String | Name of the season (e.g., Fall 2026) |
| `StartDate` | Date | Season start |
| `EndDate` | Date | Season end |
| `PlayDays` | String | Comma-separated days (e.g., "Tuesday,Friday") |

---

## Gherkin AC

### US-2.1 — Configure Season Rules
#### Scenario: Admin creates a season (happy path)
*   **Given** the Admin is on the Create Season screen
*   **When** they enter valid dates and select Tuesday/Friday as play days
*   **Then** the season is saved and ready for scheduling.

#### Scenario: Invalid dates (failure)
*   **Given** the Admin enters an End Date before the Start Date
*   **When** they click Save
*   **Then** the system blocks it and highlights the error.

---

## Screen Requirements

### SR-001: Season Setup Screen
**Authorized users:** League Owner (Admin)

**Display:**
- Season Name
- Start Date / End Date
- Play Days (Checkboxes)
- Available Locations (Checkboxes)

**Actions:**
- Save Season
- Cancel

**Behavior:**
- The system must not allow saving if no Play Days are selected.