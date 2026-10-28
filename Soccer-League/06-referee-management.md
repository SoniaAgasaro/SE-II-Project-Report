# Feature: Referee Management

**Feature ID:** 6  
**Branch pattern:** `feature/6-referee-management`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Admin assigns referees, and refs confirm via secure links. If a ref declines, the system auto-escalates.  
**Depends on:** [Feature 3 — Schedule](03-generate-schedules.md)  

---

## User Stories

### US-6.1: Assign Referees to Games
**As an** Administrator  
**I want to** assign a qualified referee to a game  
**So that** the game is officiated.  

**Independent test:** Admin assigns a soccer center ref to a game.

### US-6.2: Confirm/Decline Game Assignment
**As a** Referee  
**I want to** log in via my email link and either confirm or decline an assignment  
**So that** I can manage my own schedule.  

**Independent test:** Ref clicks "Confirm" and the Admin sees it as confirmed.

### US-6.3: Auto-Reassign Referee on Decline
**As an** Administrator  
**I want** the system to automatically assign the next qualified referee if one declines  
**So that** I don't have to manually hunt for replacements.  

**Independent test:** Ref A declines and Ref B gets an automatic email.

### US-6.4: Track and Mark Referee Payments
**As an** Administrator  
**I want to** view a report of completed games and mark referees as "Paid"  
**So that** I know who I have paid and who I still owe.  

**Independent test:** Admin clicks "Mark as Paid" for a referee.

### US-6.5: Update Referee Assignment
**As an** Administrator  
**I want to** manually change a referee assignment if there is an emergency  
**So that** the game isn't left without a referee.  

**Independent test:** Admin manually swaps Ref A for Ref C.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST email referees immediately when assigned.
- **FR-002**: Emails MUST contain a link that redirects to the Login Screen.
- **FR-003**: Upon login, the Ref must see game details (Teams, Location, Date).
- **FR-004**: System MUST allow the Ref to click "I will be there" or "I cannot make it".
- **FR-005**: If a Ref declines, the system MUST automatically assign the next qualified Ref and notify them.
- **FR-006**: System MUST track referee payments.

---

## Key Entities
- **GameReferee**: Links a Ref to a Game.
- **PaymentStatus**: Tracks if the ref has been paid.

---

## Initial Data Model

### GameReferee
| Attribute       | Type    | Description                   |
|-----------------|---------|-------------------------------|
| `GameRefereeID` | Integer | Unique identifier             |
| `GameID`        | Integer | Reference to Game             |
| `RefereeID`     | Integer | Reference to User (Ref)       |
| `Role`          | String  | E.g., Center, Line            |
| `Status`        | String  | Assigned, Confirmed, Declined |
| `IsPaid`        | Boolean | Payment tracking              |

---

## Gherkin AC

### US-6.1 — Assign Referees to Games
#### Scenario: Admin assigns ref (happy path)
*   **Given** a scheduled game
*   **When** the Admin assigns a qualified Ref
*   **Then** the system sends the Ref an email notification.

### US-6.2 — Confirm/Decline Game Assignment
#### Scenario: Ref declines game (edge case)
*   **Given** the Ref logs in via the email link
*   **When** they click "Decline"
*   **Then** the system updates the status to "Declined"
*   **And** triggers the auto-reassign feature.

### US-6.3 — Auto-Reassign Referee on Decline
#### Scenario: System auto-reassigns (happy path)
*   **Given** Ref A has just declined
*   **When** the system finds Ref B is available and qualified
*   **Then** Ref B gets an email and the game shows "Pending Ref B".

### US-6.4 — Track and Mark Referee Payments
#### Scenario: Admin marks payment (happy path)
*   **Given** a completed game with an assigned ref
*   **When** the Admin clicks "Mark as Paid"
*   **Then** the database records the payment date.

### US-6.5 — Update Referee Assignment
#### Scenario: Admin manually swaps ref (edge case)
*   **Given** Ref A is assigned but has an emergency
*   **When** the Admin assigns Ref C
*   **Then** Ref C gets the email and Ref A is notified they are removed.

---

## Screen Requirements

### SR-001: Referee Dashboard
**Authorized users:** Referee

**Display:**
- Upcoming Assigned Games
- Teams playing
- Location and Date

**Actions:**
- "Confirm Attendance" Button
- "Decline" Button

**Behavior:**
- Clicking Confirm updates the Admin dashboard.
- Clicking Decline triggers the auto-assignment algorithm for the next referee.

### SR-002: Admin Payment Report
**Authorized users:** League Owner (Admin)

**Display:**
- List of completed games
- Assigned Referees
- Total Owed

**Actions:**
- "Mark as Paid" Button