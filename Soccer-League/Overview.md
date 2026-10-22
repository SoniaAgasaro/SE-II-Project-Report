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

**Architecture:**
As modeled in the LEGO Architecture Kit, the system uses a Client-Server N-Tier architecture. 
- Clients connect via the internet (Cloud) to a Load Balancer.
- The Load Balancer routes requests to redundant, stateless Web/App Servers (Node.js on Linux).
- App servers communicate with a central Database Server (MySQL).
- This allows horizontal scaling to handle increased public traffic without needing to rewrite the application code.

**Features:**
 Overview.md
 data-model.md
 01-maintain-sports.md
 02-maintain-leagues.md
 03-maintain-seasons.md
 04-maintain-teams.md
 05-maintain-players.md
 06-maintain-locations.md
 07-maintain-users-and-refs.md
 08-generate-schedule.md
 09-game-management.md
 10-public-display.md
 11-ref-assignment-and-payment.md
 12-email-notifications.md