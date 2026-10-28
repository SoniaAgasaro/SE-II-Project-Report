# Feature: Public Portal

**Feature ID:** 7  
**Branch pattern:** `feature/7-public-portal`  
**Status:** Draft  
**Created:** 2026-10-24  
**Input:** Fans need a read-only view of schedules, scores, and standings.  
**Depends on:** [Feature 5 — Game Management](05-games-and-stats.md)  

---

## User Stories

### US-7.1: View Leagues and Schedules
**As a** Public Visitor  
**I want to** view the list of active leagues and their schedules  
**So that** I know when and where games are happening.  

**Independent test:** Public user selects "Fall Soccer" and sees the schedule.

### US-7.2: View Game Results and Standings
**As a** Public Visitor  
**I want to** view the updated standings tabloids and past game scores  
**So that** I can track team performance.  

**Independent test:** Public user sees "Team A: 3 Wins, 1 Loss" on the standings page.

### US-7.3: View Team Rosters and Player Stats
**As a** Public Visitor  
**I want to** click on a team and see their players, and click a player to see their stats  
**So that** I can track my family/friends.  

**Independent test:** Public user clicks a player and sees their 5 goals.

### US-7.4: View Playoff/Tournament Bracket
**As a** Public Visitor  
**I want to** view the end-of-season tournament bracket  
**So that** I can see who is advancing to the finals.  

**Independent test:** Public user views the top 4 bracket.

---

## Requirements

### Functional Requirements
- **FR-001**: System MUST be accessible without logging in.
- **FR-002**: System MUST strictly be read-only.
- **FR-003**: System MUST display the live updated tabloids/standings.
- **FR-004**: System MUST display team rosters and player stats.

---

## Key Entities
- **Read-Only Views**: Aggregates data from Games and Stats.


---

## Gherkin AC

### US-7.1 — View Leagues and Schedules
#### Scenario: Public views schedule (happy path)
*   **Given** the schedule is published
*   **When** a public user navigates to the site
*   **Then** they see the dates, times, and locations.

### US-7.2 — View Game Results and Standings
#### Scenario: Public views standings (happy path)
*   **Given** games have been completed
*   **When** a public user views the standings page
*   **Then** the win/loss records are displayed.

### US-7.3 — View Team Rosters and Player Stats
#### Scenario: Public views player (happy path)
*   **Given** a public user is on a Team page
*   **When** they click a player
*   **Then** the player's stats page loads.

### US-7.4 — View Playoff/Tournament Bracket
#### Scenario: Public views bracket (edge case)
*   **Given** the regular season is over
*   **When** the public user goes to the bracket page
*   **Then** the top 4 teams are displayed in a playoff format.

---

## Screen Requirements

### SR-001: Public Home Screen
**Authorized users:** Public Visitor

**Display:**
- Recent Scores
- Upcoming Games
- League Standings (Tabloids)

**Actions:**
- View Team (Link)
- View Player Stats (Link)

**Behavior:**
- All data is read-only. No edit buttons are visible.