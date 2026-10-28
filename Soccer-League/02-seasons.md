# Feature: Maintain Seasons

**Feature ID:** 2  
**Branch pattern:** `feature/2-maintain-seasons`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs to define the specific timeframes and rules for a season.  
**Depends on:** [Feature 1 — Maintain Leagues & Sports](01-leagues-and-sports.md)  

---

## User Stories

### US-2.1: Create a Season and Set Dates
**As an** Administrator  
**I want to** add a new season and set the Start Date, End Date, and Play Days  
**So that** the scheduling engine knows when games can be played.  

**Independent test:** Admin creates a season starting Sept 1, ending Nov 1, playing only on Tuesdays.

### US-2.2: Update Season Rules
**As an** Administrator  
**I want to** update the start/end dates or play days before scheduling begins  
**So that** I can fix mistakes in the season setup.  

**Independent test:** Admin changes the end date from Nov 1 to Nov 15 and saves.

### US-2.3: Set Available Locations
**As an** Administrator  
**I want to** assign which locations (fields) are available for this specific season  
**So that** the schedule generator only uses valid fields.  

**Independent test:** Admin checks only "Field 1" and "Field 2" for the Fall season.

### US-2.4: Remove/Deactivate a Season
**As an** Administrator  
**I want to** deactivate a season that was cancelled  
**So that** it doesn't clutter the public portal or active lists.  

**Independent test:** Admin deactivates the "Spring 2020" season and it is hidden from the public view.

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
| Attribute  | Type    | Description                                   |
|------------|---------|-----------------------------------------------|
| `SeasonID` | Integer | Unique identifier for the season              |
| `LeagueID` | Integer | Reference to League                           |
| `Name`     | String  | Name of the season (e.g., Fall 2026)          |
| `StartDate`| Date    | Season start                                  |
| `EndDate`  | Date    | Season end                                    |
| `PlayDays` | String  | Comma-separated days (e.g., "Tuesday Friday") |

---

## Gherkin AC

### US-2.1 — Create a Season and Set Dates
#### Scenario: Admin creates a season (happy path)
*   **Given** the Admin is on the Create Season screen
*   **When** they enter valid dates and select Tuesday/Friday as play days
*   **Then** the season is saved and ready for scheduling.

### US-2.2 — Update Season Rules
#### Scenario: Admin updates season dates (happy path)
*   **Given** a season has been created but no schedule generated yet
*   **When** the Admin edits the End Date
*   **Then** the system saves the new date successfully.

#### Scenario: Admin edits dates after schedule is generated (failure)
*   **Given** the schedule has already been generated
*   **When** the Admin attempts to change the Start Date
*   **Then** the system locks the field and shows "Cannot edit dates after schedule generation."

### US-2.3 — Set Available Locations
#### Scenario: Admin assigns locations to season (happy path)
*   **Given** the Admin is on the Season setup screen
*   **When** they check the boxes for "Field A" and "Field B"
*   **Then** those fields are saved as available for the magic sorter.

### US-2.4 — Remove/Deactivate a Season
#### Scenario: Admin deactivates a season (edge case)
*   **Given** a season is active
*   **When** the Admin clicks "Deactivate"
*   **Then** the season is hidden from the public portal.

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