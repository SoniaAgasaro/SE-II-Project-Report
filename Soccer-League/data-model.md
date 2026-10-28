# Soccer League - System Data Model

Based on the class discussion, the database architecture follows this hierarchy:

- **Users** (Admin, Managers, Refs) own and manage the system.
- **Sports** contain multiple **Leagues**.
- **Leagues** contain multiple **Teams** and multiple **Seasons**.
- **Teams** have multiple **Players** and a **Location** (Home Field).
- **Seasons** contain multiple **Games**.
- **Games** have **Results** (Scores), multiple **Stats** (per player), and assigned **Referees**.
- **Referees** are assigned to Games via a specific Role (e.g., Center Ref).

## Architecture Note
The system utilizes a 3-tier client-server architecture with a load balancer to handle public traffic, ensuring the database remains secure and the web servers can scale horizontally.