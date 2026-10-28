# Feature: Maintain Leagues & Sports

**Feature ID:** 1  
**Branch pattern:** `feature/1-maintain-leagues-sports`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs to group teams and seasons under specific leagues and sports, and manage their active status.  
**Depends on:** None  

---

## User Stories

### US-1.1: Add and View Sports
**As an** Administrator  
**I want to** add a new sport (e.g., Soccer, Basketball) and view a list of all active sports  
**So that** I can organize leagues under the correct game type.  

**Independent test:** Admin clicks "Add Sport", enters "Soccer", saves, and sees it in the list.

### US-1.2: Edit Sport Details
**As an** Administrator  
**I want to** update the name or description of an existing sport  
**So that** corrections can be made without deleting historical data.  

**Independent test:** Admin edits the name "Soccer" to "Outdoor Soccer" and sees it updated in the list.

### US-1.3: Deactivate/Remove a Sport
**As an** Administrator  
**I want to** mark a sport as inactive (soft delete)  
**So that** it no longer appears in dropdown menus, but old records remain intact.  

**Independent test:** Admin deactivates "Flag Football" and it disappears from the "Create League" sport dropdown.

### US-1.4: Add and Set League Details
**As an** Administrator  
**I want to** add a new league, link it to a sport, and set its division (e.g., Men's, Women's, Co-Ed)  
**So that** teams know which division they are playing in. 

**Independent test:** Admin creates "Men's Fall League", links it to Soccer, and sets division to "Men's".

### US-1.5: Update League Information
**As an** Administrator  
**I want to** update a league's name or description  
**So that** the public portal always reflects the correct current league information.  

**Independent test:** Admin updates the league name from "Fall League" to "Autumn Classic".

### US-1.6: Deactivate/Remove a League
**As an** Administrator  
**I want to** deactivate a league that is no longer operating  
**So that** it is hidden from new registrations while keeping past seasons accessible.  

**Independent test:** Admin deactivates "Winter Basketball" and it is removed from the active leagues list.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow the Admin to add a new Sport with a Name and Description.
- **FR-002**: System MUST allow the Admin to update a Sport's name and description.
- **FR-003**: System MUST allow the Admin to set a Sport's status to "Inactive" (soft delete).
- **FR-004**: System MUST allow the Admin to add a League, linking it to an active Sport and setting a Division.
- **FR-005**: System MUST allow the Admin to update a League's details.
- **FR-006**: System MUST allow the Admin to deactivate a League.
- **FR-007**: System MUST NOT allow a Manager or Referee to perform any Sport or League actions.

---

## Key Entities
- **Sport**: The highest level of categorization.
- **League**: Groups teams together under a Sport.

---

## Initial Data Model

### Sport
| Attribute     | Type    | Description                     |
|---------------|---------|---------------------------------|
| `SportID`     | Integer | Unique identifier for the sport |
| `Name`        | String  | Name of the sport (e.g., Soccer)|
| `Description` | String  | Details about the sport         |
| `Status`      | String  | Active/Inactive                 |

### League
| Attribute  | Type    | Description                            |
|----------- |---------|----------------------------------------|
| `LeagueID` | Integer | Unique identifier for the league       |
| `SportID`  | Integer | Reference to Sport                     |
| `Name`     | String  | Name of the league (e.g., Men's Fall)  |
| `Division` | String  | Men's, Women's, Co-Ed                  |
| `Status`   | String  | Active/Inactive                        |
---

### US-1.1 — Add and View Sports
#### Scenario: Admin adds a new sport (happy path)
*   **Given** the Admin is on the Sports List screen
*   **When** they click "Add Sport" and enter "Soccer" and click Save
*   **Then** "Soccer" appears in the active Sports list.

### US-1.2 — Edit Sport Details
#### Scenario: Admin edits a sport name (happy path)
*   **Given** "Soccer" exists in the system
*   **When** the Admin edits the name to "Outdoor Soccer" and saves
*   **Then** the updated name displays in the list.

### US-1.3 — Deactivate/Remove a Sport
#### Scenario: Admin deactivates a sport (edge case)
*   **Given** "Flag Football" exists with no active leagues
*   **When** the Admin clicks "Deactivate"
*   **Then** the sport is removed from active dropdowns but remains in historical records.

### US-1.4 — Add and Set League Details
#### Scenario: Admin creates a league (happy path)
*   **Given** the Admin is on the League Creation screen
*   **When** they enter "Fall Soccer", select the "Soccer" sport, and select "Men's" division
*   **Then** the league is saved and active.

### US-1.5 — Update League Information
#### Scenario: Admin updates a league name (happy path)
*   **Given** "Fall Soccer" exists
*   **When** the Admin changes the name to "Autumn Classic" and saves
*   **Then** the new name is reflected immediately.

### US-1.6 — Deactivate/Remove a League
#### Scenario: Admin deactivates a league (edge case)
*   **Given** a league has historical games
*   **When** the Admin deactivates it
*   **Then** it is hidden from new registrations but historical data remains.

---

## Screen Requirements

### SR-001: League & Sport List Screen
**Authorized users:** League Owner (Admin), Public Visitor

**Display:**
- League name
- Sport
- Division
- Status (Active/Inactive)

**Actions:**
- View league information
- Add League (Admin only)
- Edit League (Admin only)
- Deactivate League (Admin only)

### SR-002: League Edit/Create Screen
**Authorized users:** League Owner (Admin)

**Fields:**
- League Name
- Sport (Dropdown)
- Division (Dropdown)
- Status (Toggle)

**Actions:**
- Save
- Cancel

**Behavior:**
- The system shall display existing information when editing.
- The system shall save valid changes.
- Cancel shall return to the League List Screen without saving changes.