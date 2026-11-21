
# Feature: Role Maintenance

## 1. Header
- **Feature Name:** Role Maintenance
- **System:** Invoicing System
- **Description:** Allows authorized administrators to create, view, and update company roles and their standard billing rates. These roles are used when setting up project roles and determining the rates charged for consulting services.
- **Primary Actors:** Administrator, Owner

## 2. User Stories
- As an administrator, I want to create company roles so that employees can be assigned to specific roles on consulting projects.
- As an administrator, I want to assign a standard billing rate to each role so that the company has a default rate for its consulting services.
- As an administrator, I want to update role information so that role names and standard rates remain accurate.
- As an administrator, I want to view available roles so that I can select the appropriate roles when setting up projects.
- As an administrator, I want to maintain standard billing rates so that project managers have a reference when agreeing on project rates.

## 3. Functional Requirements
- FR-1: The system shall allow an authorized administrator to create a role record.
- FR-2: The system shall assign a unique role ID to each role.
- FR-3: The system shall store the role name.
- FR-4: The system shall store a standard billing rate for each role.
- FR-5: The system shall allow administrators to view existing roles.
- FR-6: The system shall allow administrators to update role names and standard billing rates.
- FR-7: The system shall make available roles accessible when setting up project roles.
- FR-8: The system shall use the standard billing rate as a reference when establishing project-specific rates.
- FR-9: The system shall validate that the role name and billing rate are entered before saving.
- FR-10: The system shall reject negative billing rates.
- FR-11: The system shall prevent duplicate role names.
- FR-12: The system shall restrict role maintenance to authorized users.
- FR-13: The system shall preserve existing project records when a role's standard billing rate is updated.

## 4. Assumptions
- Roles represent the types of consulting work performed by employees.
- Each role has a unique role ID.
- Each role has a name and standard billing rate.
- Standard billing rates are expressed as hourly amounts.
- Project-specific rates may differ from the standard rate.
- Project-specific rates are maintained through Project Maintenance.
- Administrators or owners are responsible for maintaining company roles.
- Roles with existing project history should not be deleted if doing so would affect historical records.

## 5. Edge Cases
- An administrator attempts to create a role without a name.
- An administrator attempts to create a role without a billing rate.
- An administrator enters a negative billing rate.
- An administrator enters an invalid billing rate format.
- An administrator attempts to create a duplicate role name.
- An administrator changes a standard billing rate after the role has been assigned to projects.
- An administrator attempts to delete a role associated with existing project records.
- An unauthorized user attempts to modify role information.

## 6. Success Criteria
- Administrators can create, view, and update roles.
- Every role receives a unique role ID.
- Each role has a name and standard billing rate.
- Invalid or negative rates are rejected.
- Duplicate role names are prevented.
- Available roles can be selected during project setup.
- Updating a standard rate does not automatically change previously agreed project-specific rates.
- Existing project history remains available.
- Unauthorized users cannot modify roles.

## 7. Key Entities
- **Role:** Represents a type of consulting work performed by employees and contains the standard billing rate.
- **Project Role:** Represents a role selected for a specific project and contains the agreed project-specific billing rate.
- **Project Role Assignment:** Connects an employee to a project role.

## 8. Initial Data Model

### Role
- RoleID (Primary Key)
- Name
- StandardRate

### Relationships
- One role may be used in multiple projects.
- A project role references one company role.
- Each project role may have multiple employee assignments.
- The standard rate provides a reference when creating a project-specific role rate.

## 9. Gherkin AC

### **Scenario 1: Successfully create a role**
**Given** an administrator is logged into the system
**When** the administrator enters a valid role name and standard billing rate
**And** selects Save
**Then** the system shall create the role record
**And** assign a unique role ID
**And** display a confirmation message.

### **Scenario 2: View available roles**
**Given** role records exist in the system
**When** an administrator opens the role list
**Then** the system shall display all available roles
**And** show their names and standard billing rates.

### **Scenario 3: Update a role**
**Given** a role already exists
**When** an administrator changes the role name or standard billing rate
**And** selects Save
**Then** the system shall update the role record
**And** display the updated information.

### **Scenario 4: Prevent a negative billing rate**
**Given** an administrator is creating or updating a role
**When** the administrator enters a negative billing rate
**And** selects Save
**Then** the system shall reject the billing rate
**And** display a validation message.

### **Scenario 5: Prevent duplicate role names**
**Given** a role already exists with a particular name
**When** an administrator attempts to create another role using the same name
**Then** the system shall reject the duplicate role
**And** display an appropriate validation message.

### **Scenario 6: Preserve project-specific rates**
**Given** a role has already been used in existing projects
**When** an administrator changes the role's standard billing rate
**Then** the system shall update the standard rate
**But** shall not automatically change previously agreed project-specific rates.

### **Scenario 7: Prevent deletion of roles with project history**
**Given** a role is associated with existing project records
**When** an administrator attempts to delete the role
**Then** the system shall prevent deletion
**And** preserve the associated project history.

## 10. Data Ownership
- The Role Maintenance feature owns the Role entity.
- Administrators and owners are responsible for creating and updating roles.
- Project Maintenance may read available roles when setting up project roles.
- Project Maintenance owns the Project Role entity and its project-specific billing rates.
- Project Role Assignment maintains the connection between employees and project roles.
- Other features shall not directly modify company role records.

## 11. API Requirements
- POST /api/roles - Create a role.
- GET /api/roles - Retrieve all available roles.
- GET /api/roles/{id} - Retrieve an individual role.
- PUT /api/roles/{id} - Update role information.
- The API shall validate role names and billing rates.
- The API shall reject negative billing rates.
- The API shall prevent duplicate role names.
- The API shall enforce authorization for role maintenance.
- Updating a standard rate shall not automatically modify existing project-specific rates.

## 12. Screen Requirements

### Role List Screen
- Display role ID.
- Display role name.
- Display standard billing rate.
- Provide an Add Role button.
- Provide an Edit option for each role.
- Allow administrators to view available roles.

### Role Information Screen
- Provide a field for role name.
- Provide a field for standard billing rate.
- Display the billing rate as an hourly amount.
- Provide a Save button.
- Provide a Cancel button.
- Display validation messages for missing or invalid information.

## 13. Definition of Done
- Administrators can create, view, and update role records.
- Every role receives a unique ID.
- Role names and standard billing rates are stored correctly.
- Negative and invalid billing rates are rejected.
- Duplicate role names are prevented.
- Available roles can be accessed during project setup.
- Changes to standard rates do not overwrite existing project-specific rates.
- Existing project history is preserved.
- All Gherkin acceptance criteria pass testing.
- Unauthorized users cannot modify role records.

## 14. Out of Scope
- Assigning employees to project roles.
- Creating project-specific role rates.
- Managing employee salaries or payroll.
- Calculating employee compensation.
- Entering project time.
- Generating customer invoices.
- Managing employee job performance.
