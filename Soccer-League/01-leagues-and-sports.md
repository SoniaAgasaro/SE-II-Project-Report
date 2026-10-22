# Feature: Maintain Leagues & Sports

**Feature ID:** 1  
**Branch pattern:** `feature/1-maintain-leagues-sports`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin needs to group teams and seasons under specific leagues and sports.  
**Depends on:** None  

---

## User Stories

### US-1.1: Manage Sports and Leagues
**As an** Administrator  
**I want to** create sports and organize leagues under them  
**So that** the system has a hierarchy for seasons and teams.  

**Independent test:** Admin can create "Basketball" and then create a "Men's Fall League" under it.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST allow the Admin to create a Sport (e.g., Soccer, Basketball).
- **FR-002**: System MUST allow the Admin to create a League and link it to a Sport.
- **FR-003**: System MUST allow the Admin to deactivate a Sport or League without deleting historical data.
- **FR-004**: System MUST NOT allow a Manager or Referee to create or edit Sports/Leagues.

---

## Key Entities
- **Sport**: The highest level of categorization.
- **League**: Groups teams together under a Sport.

---

## Initial Data Model

### Sport
| Attribute | Type | Description |
|-----------|------|-------------|
| `SportID` | Integer | Unique identifier for the sport |
| `Name` | String | Name of the sport (e.g., Soccer) |
| `Description` | String | Details about the sport |
| `Status` | String | Active/Inactive |

### League
| Attribute | Type | Description |
|-----------|------|-------------|
| `LeagueID` | Integer | Unique identifier for the league |
| `SportID` | Integer | Reference to Sport |
| `Name` | String | Name of the league (e.g., Men's Fall) |
| `Status` | String | Active/Inactive |

---

## Gherkin AC

### US-1.1 — Manage Sports and Leagues
#### Scenario: Admin creates a league (happy path)
*   **Given** the Admin is on the League creation screen
*   **When** they enter "Co-Ed Softball" and link it to the "Softball" sport
*   **Then** the league is saved and active.

#### Scenario: Admin tries to create duplicate league (failure)
*   **Given** "Fall Soccer" already exists for the Soccer sport
*   **When** the Admin tries to create another "Fall Soccer" for Soccer
*   **Then** the system blocks it and shows "League already exists for this sport".

---

## Screen Requirements

### SR-001: League & Sport List Screen
**Authorized users:** League Owner (Admin), Public Visitor

**Display:**
- League name
- Sport
- Status (Active/Inactive)

**Actions:**
- View league information
- Add League (Admin only)
- Edit League (Admin only)

### SR-002: League Edit/Create Screen
**Authorized users:** League Owner (Admin)

**Fields:**
- League Name
- Sport (Dropdown)
- Status (Toggle)

**Actions:**
- Save
- Cancel

**Behavior:**
- The system shall display existing info when editing.
- Cancel returns to List Screen without saving.