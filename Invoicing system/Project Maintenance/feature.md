
# Feature: Project Maintenance

## 1. Header
- **Feature Name:** Project Maintenance
- **System:** Invoicing System
- **Description:** Allows project managers and authorized administrators to create, view, and update customer projects. It also allows them to select project roles, establish project-specific billing rates, and assign employees to those roles.
- **Primary Actors:** Project Manager, Administrator, Owner

## 2. User Stories
- As a project manager, I want to create a project so that the company can organize and track work requested by a customer.
- As a project manager, I want to connect a project to a customer so that the system knows who is receiving the consulting services.
- As a project manager, I want to enter project dates and budgets so that the company can plan the work and monitor its cost.
- As a project manager, I want to select roles needed for a project so that the required types of work are identified.
- As a project manager, I want to set a billing rate for each project role so that the company knows how much to charge the customer for each hour of work.
- As a project manager, I want to assign employees to project roles so that everyone knows which work they are responsible for.
- As a project manager, I want to update project information so that changes to the project can be recorded.
- As a project manager, I want to change a project's status so that employees know whether they can enter time for it.
- As an administrator, I want to view project information so that I can monitor the company's consulting projects.
- As an employee, I want to see the projects and roles assigned to me so that I know where I am allowed to enter time.

## 3. Functional Requirements
- FR-1: The system shall allow an authorized project manager or administrator to create a project.
- FR-2: The system shall assign a unique project ID to each project.
- FR-3: The system shall require each project to be associated with an existing customer.
- FR-4: The system shall store the project name, customer ID, start date, estimated end date, initial budget, revised budget, and status.
- FR-5: The system shall allow authorized users to view project information.
- FR-6: The system shall allow authorized users to update project information.
- FR-7: The system shall allow a project manager to select existing company roles for a project.
- FR-8: The system shall create project role records that connect a project to the selected company roles.
- FR-9: The system shall allow the project manager to enter an agreed billing rate for each project role.
- FR-10: The system shall allow multiple roles to be added to one project.
- FR-11: The system shall allow the project manager to assign employees to project roles.
- FR-12: The system shall allow multiple employees to be assigned to the same project role.
- FR-13: The system shall prevent inactive employees from receiving new project assignments.
- FR-14: The system shall allow the project manager to view all employees assigned to a project and their roles.
- FR-15: The system shall allow the project manager to update employee project role assignments.
- FR-16: The system shall support the following project statuses: Pending, Active, and Closed.
- FR-17: The system shall allow a project manager to change a project's status.
- FR-18: The system shall prevent employees from entering new time for projects that are Pending or Closed.
- FR-19: The system shall allow employees to enter time only for Active projects to which they have an assignment.
- FR-20: The system shall store an initial project budget and a revised project budget.
- FR-21: The system shall allow authorized users to update the revised project budget when the agreed project budget changes.
- FR-22: The system shall retain existing project, assignment, and time records when project information is updated.
- FR-23: The system shall validate required project information before saving.
- FR-24: The system shall restrict project creation, updates, and assignments to authorized users.

## 4. Assumptions
- Each project belongs to one customer.
- A customer may have multiple projects.
- Each project has a unique project ID.
- The project manager is responsible for setting up the project, its roles, and employee assignments.
- Company roles must already exist before they can be selected for a project.
- A project role uses a company role as its starting point.
- The project manager and customer agree on the billing rate for each project role.
- Project-specific billing rates may be different from the standard rates stored in Role Maintenance.
- Multiple employees may perform the same role on one project.
- An employee may work on multiple projects.
- Only active employees may receive new project assignments.
- A project may be Pending before work begins.
- A project must be Active before employees can enter time.
- A project becomes Closed when the work is finished.
- The initial budget represents the original agreed budget.
- The revised budget represents the updated budget when project costs or agreements change.
- Changes to the revised budget do not erase the initial budget.
- Project-specific invoice contact information may be maintained so that invoices can be sent to the correct person.
- Project records with existing time or invoice history should not be deleted.

## 5. Edge Cases
- A project manager attempts to create a project without selecting a customer.
- A project manager enters a project name that is already being used for the same customer.
- A project manager enters an estimated end date earlier than the start date.
- A project manager enters a negative project budget.
- A project manager attempts to add a role that does not exist in Role Maintenance.
- A project manager attempts to add the same role to a project more than once.
- A project manager enters a negative or invalid project billing rate.
- A project manager attempts to assign an inactive employee to a project.
- A project manager attempts to assign an employee to a project role that does not belong to the selected project.
- A project has no employees assigned to its roles.
- A project manager attempts to close a project that still has unapproved time.
- An employee attempts to enter time for a Pending project.
- An employee attempts to enter time for a Closed project.
- An employee attempts to enter time for a project to which they have not been assigned.
- A project budget is revised after employees have already entered time.
- A project has existing invoices when its information is updated.
- A user without project management permission attempts to change project information or assignments.

## 6. Success Criteria
- Project managers can successfully create, view, and update projects.
- Every project has a unique project ID and is connected to a customer.
- Project dates, budgets, and statuses are stored correctly.
- Project managers can select existing company roles.
- Each project role has its own agreed billing rate.
- Employees can be assigned to the correct project roles.
- Multiple employees can be assigned to the same role.
- Inactive employees cannot receive new project assignments.
- Project status controls whether employees can enter time.
- Only assigned employees can enter time for an Active project.
- Initial and revised project budgets are maintained separately.
- Changes to project information do not remove historical records.
- Unauthorized users cannot make changes to project information.
- All acceptance criteria pass testing.

## 7. Key Entities
- **Project:** Represents a specific job or assignment that the consulting company performs for a customer.
- **Customer:** Represents the business receiving consulting services.
- **Role:** Represents a type of consulting work, such as Software Developer or Project Manager.
- **Project Role:** Represents a company role selected for a particular project and contains the agreed billing rate for that project.
- **Project Role Assignment:** Connects an employee to a specific project role.
- **Employee:** Represents a person working for the consulting company who may be assigned to project roles.

## 8. Initial Data Model

### Project
- ProjectID (Primary Key)
- Name
- CustomerID (Foreign Key)
- StartDate
- EstimatedEndDate
- InitialBudget
- RevisedBudget
- Status (Pending, Active, Closed)
- InvoiceContactName
- InvoiceContactEmail
- InvoiceContactPhone

### Project Role
- ProjectRoleID (Primary Key)
- ProjectID (Foreign Key)
- RoleID (Foreign Key)
- AgreedRate

### Project Role Assignment
- ProjectRoleAssignmentID (Primary Key)
- ProjectRoleID (Foreign Key)
- EmployeeID (Foreign Key)

### Relationships
- One customer can have many projects.
- Each project belongs to one customer.
- One project can have multiple project roles.
- Each project role belongs to one project.
- Each project role references one company role.
- One project role can have multiple employee assignments.
- Each project role assignment connects one employee to one project role.
- One employee can have multiple project role assignments.
- Project Time records use the Project Role Assignment ID to identify the employee's assigned role and agreed billing rate.

## 9. Gherkin AC

### **Scenario 1: Successfully create a project**

**Given** a project manager is logged into the system
**And** a customer already exists
**When** the project manager enters the project name, customer, dates, and initial budget
**And** selects Save
**Then** the system shall create the project record
**And** assign a unique project ID
**And** set the initial project status to Pending
**And** display a confirmation message.

### **Scenario 2: Add roles to a project**
**Given** a project already exists
**And** company roles are available in the system
**When** the project manager selects roles for the project
**And** enters an agreed billing rate for each role
**And** saves the project roles
**Then** the system shall create the project role records
**And** connect each role to the selected project
**And** store the agreed billing rates.

### **Scenario 3: Assign employees to project roles**
**Given** a project has existing project roles
**And** active employees exist in the system
**When** the project manager selects employees for a project role
**And** saves the assignments
**Then** the system shall create the project role assignments
**And** connect each employee to the selected project role.

### **Scenario 4: Prevent assignment of inactive employees**
**Given** an employee has an Inactive status
**And** a project has an available role
**When** the project manager attempts to assign the inactive employee
**Then** the system shall prevent the assignment
**And** display an appropriate message.

### **Scenario 5: Update project information**
**Given** a project already exists
**When** the project manager changes the project information
**And** selects Save
**Then** the system shall update the project record
**And** display the updated information
**But** shall preserve existing project assignments and historical time records.

### **Scenario 6: Update a project budget**
**Given** a project already has an initial budget
**When** the project manager enters a revised budget
**And** saves the changes
**Then** the system shall store the revised budget
**And** retain the original initial budget.

### **Scenario 7: Change project status to Active**
**Given** a project has been created with Pending status
**When** the project manager changes the status to Active
**And** saves the changes
**Then** the system shall update the project status
**And** allow assigned employees to enter project time.

### **Scenario 8: Close a project**
**Given** a project has an Active status
**When** the project manager changes the status to Closed
**And** saves the changes
**Then** the system shall update the project status
**And** prevent employees from entering additional time
**But** retain existing project time and invoice records.

### **Scenario 9: Prevent time entry for Pending projects**
**Given** a project has a Pending status
**When** an employee attempts to enter time for the project
**Then** the system shall prevent the time entry
**And** display a message explaining that the project is not active.

### **Scenario 10: Prevent time entry for Closed projects**
**Given** a project has a Closed status
**When** an employee attempts to enter new time for the project
**Then** the system shall reject the time entry
**And** display an appropriate message.

### **Scenario 11: Prevent project creation without a customer**
**Given** a project manager is creating a new project
**When** the project manager does not select a customer
**And** selects Save
**Then** the system shall display a validation message
**And** shall not create the incomplete project.

### **Scenario 12: Prevent invalid project dates**
**Given** a project manager is creating or updating a project
**When** the estimated end date is earlier than the start date
**And** selects Save
**Then** the system shall reject the invalid dates
**And** display a validation message.

### **Scenario 13: Prevent duplicate project roles**
**Given** a project already contains a particular role
**When** the project manager attempts to add the same role again
**Then** the system shall prevent the duplicate project role
**And** display an appropriate message.

## 10. Data Ownership
- The Project Maintenance feature owns the Project, Project Role, and Project Role Assignment entities.
- Project managers are responsible for creating projects, selecting roles, setting project-specific rates, and assigning employees.
- Administrators and owners may view and maintain project information if they have the required permissions.
- Customer Maintenance owns the Customer entity. Project Maintenance may read customer information but shall not directly modify customer records.
- Role Maintenance owns the Role entity. Project Maintenance may select existing roles but shall not directly modify company role records.
- Employee Maintenance owns the Employee entity. Project Maintenance may read employee information when creating assignments but shall not directly modify employee records.
- Project Time Entry uses project and assignment information to determine which employees can enter time and which billing rates apply.
- Invoice-related features may read project information and project descriptions when preparing invoices.
- Changes to project roles or assignments shall not erase existing project time or invoice history.

## 11. API Requirements
- POST /api/projects - Create a project.
- GET /api/projects - Retrieve the project list.
- GET /api/projects/{id} - Retrieve project details.
- PUT /api/projects/{id} - Update project information.
- PATCH /api/projects/{id}/status - Update project status.
- POST /api/projects/{id}/roles - Add a role to a project.
- GET /api/projects/{id}/roles - Retrieve project roles.
- PUT /api/projects/{id}/roles/{projectRoleId} - Update a project role and its agreed rate.
- POST /api/projects/{id}/assignments - Assign an employee to a project role.
- GET /api/projects/{id}/assignments - Retrieve project employee assignments.
- PUT /api/projects/{id}/assignments/{assignmentId} - Update an employee assignment.
- The API shall validate customer, role, and employee references.
- The API shall prevent assignments of inactive employees.
- The API shall validate project dates and budget amounts.
- The API shall enforce project status rules for time entry.
- The API shall enforce authorization for project maintenance operations.

## 12. Screen Requirements

### Project List Screen
- Display project ID.
- Display project name.
- Display customer name.
- Display start date.
- Display estimated end date.
- Display initial budget.
- Display revised budget.
- Display project status.
- Provide an Add Project button.
- Provide an option to view and edit project details.
- Allow users to search for projects by project name or customer.
- Allow users to filter projects by status.

### Project Information Screen
- Provide a field for project name.
- Provide a customer selection field.
- Provide a start date field.
- Provide an estimated end date field.
- Provide an initial budget field.
- Provide a revised budget field.
- Provide a project status selection.
- Provide fields for project invoice contact name, email, and phone.
- Provide Save and Cancel buttons.
- Display validation messages for missing or invalid information.

### Project Roles Screen
- Display the roles selected for the project.
- Provide an Add Project Role button.
- Allow the project manager to select an existing company role.
- Display the standard billing rate as a reference.
- Provide a field for the agreed project-specific billing rate.
- Allow the project manager to edit the agreed rate.
- Display the role name and agreed rate for each project role.

### Project Employee Assignment Screen
- Display the project roles.
- Display the employees assigned to each role.
- Provide an Assign Employee option.
- Allow the project manager to select an active employee.
- Prevent inactive employees from being selected for new assignments.
- Allow the project manager to update assignments.
- Display a message when no employees are assigned to a project role.

## 13. Definition of Done
- Project managers can create, view, and update project records.
- Every project has a unique project ID and an associated customer.
- Project dates, budgets, and statuses are stored correctly.
- Project roles can be selected from existing company roles.
- Each project role stores its agreed project-specific billing rate.
- Employees can be assigned to project roles.
- Multiple employees can be assigned to the same project role.
- Inactive employees cannot receive new assignments.
- Project status controls whether employees can enter time.
- Initial and revised budgets are maintained separately.
- Existing project assignments and historical records are preserved.
- Required fields and invalid values are validated.
- All Gherkin acceptance criteria pass testing.
- Only authorized users can perform project maintenance operations.

## 14. Out of Scope
- Creating and maintaining company roles.
- Creating and maintaining employee records.
- Employee payroll and salary calculations.
- Entering employee project time.
- Reviewing and approving project time.
- Recording project expenses.
- Generating invoices.
- Reviewing and approving invoices.
- Processing customer payments.
- Managing full customer contracts.
