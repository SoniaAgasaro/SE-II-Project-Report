# Soccer League System - Overview

**Intent:** 
To replace a manual, spreadsheet-driven sports league management process with a dynamic web application. 
The system aims to:
- Automate schedule generation 
- Allow managers to self-service their rosters and game stats
- Assign referees
- Provide a public-facing portal for fans and families to view schedules, standings, and player statistics.

**Primary Users:**
- **Owner/Admin:** Configures the league, generates schedules, assigns referees, tracks referee payments, and manages all data.
- **Managers:** Register their teams, manage their own player rosters, and enter game scores and player stats (home manager is responsible for submitting the final score).
- **Referees:** View their assigned games, confirm/decline availability via email links, and get tracked for payment.
- **Public/Fans (No login):** View leagues, schedules, team rosters, player stats, and tournament brackets.


# Soccer League - System Data Model

The database architecture follows this hierarchy:

- **Users** (Admin, Managers, Refs) own and manage the system.
- **Sports** contain multiple **Leagues**.
- **Leagues** contain multiple **Teams** and multiple **Seasons**.
- **Teams** have multiple **Players** and a **Location** (Home Field).
- **Seasons** contain multiple **Games**.
- **Games** have **Results** (Scores), multiple **Stats** (per player), and assigned **Referees**.
- **Referees** are assigned to Games via a specific Role (e.g., Center Ref).

**Features:**
 Overview.md
 data-model.md
 01-leagues-and-sports.md
 02-seasons.md
 03-generate-schedules.md
 04-teams-rosters-locations.md
 05-games-and-stats.md
 06-referee-management.md
 07-public-portal.md
 08-user-admiministration.md

 **Architecture:**
As modeled in the LEGO Architecture Kit, the system uses a Client-Server N-Tier architecture. 
- Clients connect via the internet (Cloud) to a Load Balancer.
- The Load Balancer routes requests to redundant, stateless Web/App Servers (Node.js on Linux).
- App servers communicate with a central Database Server (MySQL).
- This allows horizontal scaling to handle increased public traffic without needing to rewrite the application code.