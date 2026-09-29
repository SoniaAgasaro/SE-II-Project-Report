# Feature: Church Member System <Human-readable title>

**Branch pattern:** `feature/1-church-member-system`  
**Status:** Draft  
**Created:** 2026-09-10  
**Input:** A system that will manage the church members' records, track attendance, organize van pick-up routes for kids and QR code registrations  


---

## User Stories

### US-N.1: Registration of members
**As a** Front desk / Admin <role>  
**I want to** register new members by entering their personal details (Full name, email - if they have one, address, date of birth, if they're baptized) and year of birth <capability>  
**So that** the system automatically categorizes them as an adult or a child and link family records appropriately. <benefit>

**Priority:** P1  
**Independent test:** Verify that entering a birthdate under 18 marks the member as a child and prompts for parent /guardian information.   
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Van routes pickup and drop-off tracking
**As a** Van Driver<role>  
**I want to** view assigned routes and check off kids during pickups or drop-offs<capability>  
**So that** I can accurately track who was picked up, dropped off, not picked/dropped marked as "Absent" <benefit>

**Priority:** P2 
**Independent test:** Verify that a driver can mark a child as "Picked up", "Dropped-off" or "Absent" on an active route list. 
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: QR code Registration and Adult attendance
**As a** Admin / Church member<role>  
**I want to** scan and use the QR for member registration and signing in as an adult(>18 years) <capability>  
**So that** attendance, registration and check-in can be completed quickly without delays <benefit>

**Priority:** P3  
**Independent test:** Verify that scanning the QR code, the adult is able to enter their information and the system records their attendance for services. Verify that scanning the QR code a child (<18 years) can add parental/guardian information.
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST deternine whether the member is a "Child" (<18 years) or an "Adult" (>=18 years) based on the enetered year of birth
- **FR-002**: System MUST require parent/guardian full names, contact details, address and school name when registered as a Child
- **FR-003**: System MUST allow van drivers to mark status options "Picked-up", "Dropped-off" or "Absent" for each child assigned to a van route
- **FR-004**: System MUST restrict role permissions to three distinct groups: Front desk/Admin, Van driver and Bible teacher
- **FR-005**: System MUST have a QR code to a form to enhance member registration, and adult attendance check-in
- **FR-006**: System MUST automatically record attendance for kids when a Van Driver checks them off on a route, or if the Bible teacher marks them as present

---

## Data Model Requirements

### `members` table
| Field | Type | Rules |
|-------|------|-------|
| `first_name` | VARCHAR | Required |
| `last_name` | VARCHAR | Required |
| `email` | VARCHAR | Optional |
| `date of birth` | DATE | Required |
| `is_child` | BOOLEAN | Generated (TRUE if age < 18) |
| `parent_name` | VARCHAR | Required if `is_child` is TRUE |
| `school` | VARCHAR | Required if `is_child` is TRUE |
| `address` | VARCHAR | Required |
| `is_baptized` | BOOLEAN | Default FALSE |

### `Van_routes` table
| Field | Type | Rules |
|-------|------|-------|
| `driver_first_name` | VARCHAR | Reference `members.first_name`|
| `driver_last_name` | VARCHAR | Reference `members.last_name` |
| `driver_id` | INTEGER FK | Required |
| `van_number` | INTEGER FK | Required |
| `route_name` | VARCHAR | Required |
| `child_name` | VARCHAR| References `members.id` |
| `pickup_status` | VARCHAR | Options: 'Pending', 'Picked Up', 'Not Picked' |
| `dropoff_status` | VARCHAR | Options: 'Pending', 'Dropped Off', 'Not Dropped' |

---

## Acceptance Criteria

### US-N.1 — Registration of members

#### Scenario: Registering  a child member (happy path)
*   **Given** the user is logged in as a front desk agent <starting state>
*   **When** they enter a new member with a date of birth showing an age under 18 <action>
*   **Then** the system flags the member as a "child" <observable result>
*   **And** requires input for Parent/Guardian name, Address, and school before saving <extra result if needed>

#### Scenario: Missing required parent info for a child  (failure / edge)
*   **Given** the user is registered as a child under 18
*   **When** they leave the parent/guardian contact empty and click save
*   **Then** the system prevents submission and displays an error requiring parent details

### US-N.2 — Van routes pickup and drop-off tracking

#### Scenario: Driver checks off a child on a pickup route (happy path)
*   **Given** a van driver is viewing thier assigned route checklist
*   **When** they mark as "Picked up"
*   **Then** the child's status updates to "Picked Up" and an attendance record is created for today's service.

#### Scenario: Child not present at pickup stop (failure / edge)
*   **Given** a Van Driver is at a designated stop and the child is not present
*   **When** the driver selects "Not Picked"
*   **Then** the system logs the status as "Not Picked" without marking the child present for attendance.

### US-N.3 — QR code Registration and Adult attendance

#### Scenario: Adult checks in using QR code (happy path)
*   **Given** an adult member uses their phones to scan the QR code at the front desk
*   **When** the scanner reads the QR code 
*   **Then** the system records an adult attendance entry for today's date.
