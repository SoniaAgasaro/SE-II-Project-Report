
# Feature: Employee Maintenance

## 1. Header
- **Feature Name:** Employee Maintenance
- **System:** Invoicing System
- **Description:** Allows authorized administrators to create, view, and update employee information used for project assignments and time entry.
- **Primary Actors:** Administrator, Owner

## 2. User Stories
- As an administrator, I want to add employees so that they can be assigned to consulting projects.
- As an administrator, I want to update employee information so that the system maintains accurate employee records.
- As an administrator, I want to view employee information so that I can manage the people working for the company.
- As an administrator, I want to change an employee's status so that employees who no longer work for the company cannot be assigned to new projects.
- As an employee, I want my information to be maintained so that I can access the projects assigned to me and enter my time.

## 3. Functional Requirements
- FR-1: The system shall allow an authorized administrator to create an employee record.
- FR-2: The system shall assign a unique employee ID to each employee.
- FR-3: The system shall store the employee's name, title, email address, and status.
- FR-4: The system shall allow authorized administrators to view employee records.
- FR-5: The system shall allow authorized administrators to update employee information.
- FR-6: The system shall allow an administrator to change an employee's status to active or inactive.
- FR-7: The system shall allow only active employees to be assigned to new projects.
- FR-8: The system shall retain employee records when an employee becomes inactive if the employee has existing project or time records.
- FR-9: The system shall validate required employee information before saving a record.
- FR-10: The system shall restrict employee maintenance to authorized users.

## 4. Assumptions
- Employees are created and maintained by an administrator or owner.
- Each employee has a unique employee ID.
- Employee titles describe their position within the consulting company.
- Employee email addresses may be used for reminders about entering project time.
- Employee status indicates whether an employee is currently active.
- This system does not calculate employee salaries or process payroll.

## 5. Edge Cases
- An administrator attempts to create an employee without a name.
- An administrator enters an invalid email address.
- An administrator attempts to create an employee using an email address already assigned to another employee.
- An administrator attempts to assign an inactive employee to a new project.
- An administrator attempts to delete an employee who has existing project time records.
- An unauthorized user attempts to modify employee information.
- An employee becomes inactive while having previously recorded project time.

## 6. Success Criteria
- Administrators can successfully create, view, and update employee records.
- Each employee receives a unique employee ID.
- Required information is validated before saving.
- Employee status can be changed between active and inactive.
- Inactive employees cannot receive new project assignments.
- Historical employee and project time records remain available.
- Unauthorized users cannot modify employee records.

## 7. Key Entities
- **Employee:** Represents a person employed by the consulting company who may be assigned to projects and enter project time.
- **Project Role Assignment:** Connects an employee to a project role on a particular project.

## 8. Initial Data Model
### Employee
- EmployeeID (Primary Key)
- Name
- Title
- Email
- Status (Active, Inactive)

### Relationships
- One employee may have multiple project role assignments.
- Each project role assignment belongs to one employee.
- Employee records may be associated with multiple project time records through project role assignments.

## 9. Gherkin AC

### **Scenario 1: Successfully create an employee**
**Given** an administrator is logged into the system
**When** the administrator enters valid employee information
**And** selects Save
**Then** the system shall create the employee record
**And** assign a unique employee ID
**And** display a confirmation message.

### **Scenario 2: View employee information**
**Given** employee records exist in the system
**When** an administrator opens the employee list
**Then** the system shall display the available employee records
**And** show their names, titles, email addresses, and statuses.

### **Scenario 3: Update employee information**
**Given** an employee record already exists
**When** an administrator changes the employee information
**And** selects Save
**Then** the system shall update the employee record
**And** display the updated information.

### **Scenario 4: Deactivate an employee**
**Given** an active employee exists in the system
**When** an administrator changes the employee status to Inactive
**And** saves the changes
**Then** the system shall update the employee status
**And** prevent the employee from receiving new project assignments
**But** retain existing project and time records.

### **Scenario 5: Prevent incomplete employee records**
**Given** an administrator is creating an employee record
**When** the administrator leaves the employee name empty
**And** selects Save
**Then** the system shall display a validation message
**And** shall not save the incomplete record.

### **Scenario 6: Prevent assignment of inactive employees**
**Given** an employee has an Inactive status
**When** an administrator attempts to assign that employee to a new project
**Then** the system shall prevent the assignment
**And** display an appropriate message.

## 10. Data Ownership
- The Employee Maintenance feature owns the Employee entity.
- Administrators and owners are responsible for creating and maintaining employee information.
- Project Maintenance may read employee information when assigning employees to projects.
- Project Time Entry may read employee information to identify the employee entering time.
- Other features shall not directly modify employee records.
- Historical project and time records shall remain associated with the employee even after deactivation.

## 11. API Requirements
- POST /api/employees - Create an employee record.
- GET /api/employees - Retrieve the employee list.
- GET /api/employees/{id} - Retrieve an individual employee record.
- PUT /api/employees/{id} - Update employee information.
- PATCH /api/employees/{id}/status - Update employee status.
- The API shall validate required fields and email formatting.
- The API shall enforce authorization for employee maintenance.
- The API shall prevent inactive employees from receiving new project assignments.

## 12. Screen Requirements

### Employee List Screen
- Display employee ID.
- Display employee name.
- Display employee title.
- Display employee email.
- Display employee status.
- Provide an Add Employee button.
- Provide an Edit option for each employee.
- Allow administrators to identify active and inactive employees.

### Employee Information Screen
- Provide fields for employee name, title, and email.
- Provide an employee status selection.
- Provide a Save button.
- Provide a Cancel button.
- Display validation messages for missing or invalid information.

## 13. Definition of Done
- Administrators can create, view, and update employee records.
- Employee IDs are unique.
- Required information and email formatting are validated.
- Employee status can be changed.
- Inactive employees cannot be assigned to new projects.
- Historical records remain available.
- All Gherkin acceptance criteria pass testing.
- Unauthorized users cannot modify employee information.

## 14. Out of Scope
- Employee payroll and salary calculations.
- Employee benefits management.
- Employee attendance tracking.
- Employee recruitment and hiring.
- Employee performance evaluations.
- Processing employee payments.
