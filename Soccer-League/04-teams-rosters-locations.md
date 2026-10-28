# Feature: Manage Teams, Rosters & Locations

**Feature ID:** 4  
**Branch pattern:** `feature/4-teams-rosters-locations`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Managers need to manage their team, add players, and select a home location.  
**Depends on:** [Feature 1 — Leagues](01-leagues-and-sports.md)  

---

## User Stories

### US-4.1: Add and Register a Team
**As a** Manager  
**I want to** add my team to the league and set a Home Location  
**So that** my team is registered for the season.  

**Independent test:** Manager creates "Team A" and sets "Field 3" as their home location.

### US-4.2: Update Team Details
**As a** Manager  
**I want to** update my team's name or change our home location  
**So that** the information is accurate for the season.  

**Independent test:** Manager changes home location from Field 3 to Field 4.

### US-4.3: Remove/Deactivate a Team
**As an** Administrator  
**I want to** deactivate a team that drops out of the league  
**So that** they are removed from future scheduling.  

**Independent test:** Admin deactivates a team and they don't appear in the next schedule generator run.

### US-4.4: Add Players to Roster
**As a** Manager  
**I want to** add players (First Name, Last Name, Email) to my team roster  
**So that** they can be tracked for stats.  

**Independent test:** Manager adds "John Doe" to the roster.

### US-4.5: Update Player Details
**As a** Manager  
**I want to** edit a player's name or email  
**So that** their profile remains accurate.  

**Independent test:** Manager corrects a typo in a player's last name.

### US-4.6: Remove/Deactivate a Player
**As a** Manager  
**I want to** deactivate a player who is no longer on the team  
**So that** they are removed from the active roster but keep their stats.  

**Independent test:** Manager deactivates a player and they no longer appear in the scoring menu, but their past goals remain.

### US-4.7: Set/Add Locations
**As an** Administrator  
**I want to** add new locations (fields) and set their addresses  
**So that** teams can select them as home fields.  

**Independent test:** Admin adds "New Park Field 1" to the system.

### US-4.8: Remove/Deactivate a Location
**As an** Administrator  
**I want to** deactivate a location that is no longer usable (e.g., field destroyed)  
**So that** it cannot be selected for future games.  

**Independent test:** Admin deactivates a flooded field.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow Managers to add/remove players (soft delete).
- **FR-002**: System MUST require a Team to have a Home Location.
- **FR-003**: System MUST enforce that a Manager can only edit their own team.

---

## Key Entities
- **Team**: The participating group.
- **Player**: Individuals on the team.
- **Location**: The physical field.

---

## Initial Data Model

### Team
| Attribute     | Type    | Description           |
|---------------|---------|-----------------------|
| `TeamID`      | Integer | Unique identifier     |
| `ManagerID`   | Integer | Reference to User     |
| `LocationID`  | Integer | Reference to Location |
| `Name`        | String  | Team Name             |

### Player
| Attribute   | Type    | Description         |
|-------------|---------|---------------------|
| `PlayerID`  | Integer | Unique identifier   |
| `TeamID`    | Integer | Reference to Team   |
| `FirstName` | String  | Player's first name |
| `LastName`  | String  | Player's last name  |

### Location
| Attribute    | Type    | Description                     |
|--------------|---------|---------------------------------|
| `LocationID` | Integer | Unique identifier               |
| `Name`       | String  | Field name (e.g., Central Park) |
| `Address`    | String  | Physical address                |

---

## Gherkin AC

### US-4.1 — Add and Register a Team
#### Scenario: Manager registers team (happy path)
*   **Given** the Manager is on the Team Management screen
*   **When** they enter "Team A" and select a location
*   **Then** the team is created.

### US-4.2 — Update Team Details
#### Scenario: Manager updates location (happy path)
*   **Given** the team exists
*   **When** the Manager selects a new location and saves
*   **Then** the new location is reflected on the team profile.

### US-4.3 — Remove/Deactivate a Team
#### Scenario: Admin deactivates team (edge case)
*   **Given** a team is active
*   **When** the Admin deactivates them
*   **Then** they are excluded from future game generation.

### US-4.4 — Add Players to Roster
#### Scenario: Manager adds a player (happy path)
*   **Given** the Manager is on the Roster screen
*   **When** they enter "John Doe" and click Add
*   **Then** John Doe appears on the roster.

### US-4.5 — Update Player Details
#### Scenario: Manager edits player (happy path)
*   **Given** John Doe is on the roster
*   **When** the Manager updates his last name
*   **Then** the new name is saved.

### US-4.6 — Remove/Deactivate a Player
#### Scenario: Manager deactivates player with stats (edge case)
*   **Given** a player has recorded goals
*   **When** the Manager deactivates them
*   **Then** the player is removed from the active roster
*   **And** their historical stats remain in the database.

### US-4.7 — Set/Add Locations
#### Scenario: Admin adds location (happy path)
*   **Given** the Admin is on the Location screen
*   **When** they enter "New Park" and save
*   **Then** the new field is available for teams.

### US-4.8 — Remove/Deactivate a Location
#### Scenario: Admin deactivates location (failure)
*   **Given** a location has upcoming scheduled games
*   **When** the Admin tries to deactivate it
*   **Then** the system blocks it and warns "Reassign games first."

---

## Screen Requirements

### SR-001: Team Management Screen
**Authorized users:** Manager, League Owner (Admin)

**Display:**
- Team Name
- Home Location (Dropdown)
- Player Roster List (Name, Status)

**Actions:**
- Add Player (Button)
- Deactivate Player (Button)
- Edit Team Location (Dropdown)

**Behavior:**
- The system must not allow a Manager to delete a player who has recorded stats (only deactivate).