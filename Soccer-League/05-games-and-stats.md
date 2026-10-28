# Feature: Game Management, Stats & Results

**Feature ID:** 5  
**Branch pattern:** `feature/5-game-management-stats`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Managers need a screen to view past games and input scores, stats, and cards.  
**Depends on:** [Feature 3 — Schedule](03-generate-schedules.md)  

---

## User Stories

### US-5.1: Enter Final Score
**As a** Home Manager  
**I want to** input the final score for both teams (Home and Away)  
**So that** the standings tabloid updates.  

**Independent test:** Manager enters 3-2 and saves.

### US-5.2: Add Player Stats
**As a** Home Manager  
**I want to** add specific stats (Goals, Assists, Cards) for players from both teams  
**So that** player profiles reflect their performance.  

**Independent test:** Manager adds 2 goals for John Doe.

### US-5.3: Update/Edit Game Result
**As an** Administrator  
**I want to** edit a game result after it has been saved (e.g., if a manager made a mistake)  
**So that** the standings remain accurate.  

**Independent test:** Admin corrects a score from 3-2 to 3-3.

### US-5.4: Verify Game Result (Referee)
**As a** Referee  
**I want to** verify the game result submitted by the manager  
**So that** the system is not vulnerable to managers cheating or making errors.  

**Independent test:** Ref logs in and clicks "Verify" on the game.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST show a list of "Held" (Past) games for the Manager's team.
- **FR-002**: System MUST allow the Manager to click "Edit" on a past game to input the score.
- **FR-003**: System MUST provide a dynamic list of stats based on the Sport (e.g., Goals for Soccer, Points for Basketball).
- **FR-004**: System MUST allow inputting Red/Yellow cards.
- **FR-005**: System MUST require Referee verification (if applicable) or Admin override before finalizing.
- **FR-006**: System MUST automatically update the Standings/Tabloids once saved.

---

## Key Entities
- **Result**: The final score of a game.
- **StatisticType**: The allowed stats for that sport.
- **PlayerGameStatistic**: The recorded stat value.

---

## Initial Data Model

### GameResult
| Attribute      | Type    | Description             |
|----------------|---------|-------------------------|
| `GameResultID` | Integer | Unique identifier       |
| `GameID`       | Integer | Reference to Game       |
| `HomeScore`    | Integer | Home team's final score |
| `AwayScore`    | Integer | Away team's final score |

### StatisticType
| Attribute         | Type    | Description                             |
|-------------------|---------|-----------------------------------------|
| `StatisticTypeID` | Integer | Unique identifier                       |
| `SportID`         | Integer | Reference to Sport                      |
| `Name`            | String  | E.g., "Goals", "Assists", "Yellow Card" |

### PlayerGameStatistic
| Attribute          | Type    | Description                     |
|--------------------|---------|---------------------------------|
| `PlayerGameStatID` | Integer | Unique identifier               |
| `PlayerID`         | Integer | Reference to Player             |
| `GameID`           | Integer | Reference to Game               |
| `StatisticTypeID`  | Integer | Reference to StatisticType      |
| `Value`            | Integer | The stat amount (e.g., 2 goals) |

---

## Gherkin AC

### US-5.1 — Enter Final Score
#### Scenario: Manager enters score (happy path)
*   **Given** the game has been played
*   **When** the Manager enters the score and clicks Save
*   **Then** the standings update.

### US-5.2 — Add Player Stats
#### Scenario: Manager adds stats (happy path)
*   **Given** the Manager is on the Stats screen
*   **When** they input 2 goals for a player
*   **Then** the player's season total increases by 2.

### US-5.3 — Update/Edit Game Result
#### Scenario: Admin edits a completed result (edge case)
*   **Given** a game is marked as "Completed"
*   **When** the Admin edits the score
*   **Then** the system updates the standings and logs the change.

### US-5.4 — Verify Game Result (Referee)
#### Scenario: Referee verifies result (happy path)
*   **Given** a result has been submitted
*   **When** the Referee clicks "Verify"
*   **Then** the result is locked and final.

---

## Screen Requirements

### SR-001: Game Management Menu Screen
**Authorized users:** Home Manager, League Owner (Admin)

**Display:**
- Menu of past games (Date, Teams)
- Status (Needs Score, Completed)

**Actions:**
- "Edit Game" (Button)

### SR-002: Edit Game Stats Screen
**Authorized users:** Home Manager, League Owner (Admin)

**Display:**
- Home Team Score Input
- Away Team Score Input
- Player list for both teams

**Fields:**
- For each player: Stat inputs (Goals, Assists, Red/Yellow cards)

**Actions:**
- Save Results
- Cancel

**Behavior:**
- The system shall display the existing information when editing.
- Save shall update the standings tabloid instantly.