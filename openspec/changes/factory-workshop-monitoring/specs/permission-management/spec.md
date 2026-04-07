## ADDED Requirements

### Requirement: User authentication
The system SHALL authenticate users with username and password.

#### Scenario: Successful login
- **WHEN** user enters valid credentials
- **THEN** system SHALL create session and redirect to dashboard

#### Scenario: Failed login
- **WHEN** user enters invalid credentials
- **THEN** system SHALL display error message and SHALL NOT create session

### Requirement: Role-based access control
The system SHALL support three roles: Admin, Supervisor, Viewer.

#### Scenario: Admin can access all features
- **WHEN** user with Admin role is authenticated
- **THEN** user SHALL have access to: system configuration, device management, user management, all dashboards

#### Scenario: Supervisor can view and acknowledge
- **WHEN** user with Supervisor role is authenticated
- **THEN** user SHALL have access to: dashboard, violation list, alert acknowledgment
- **AND** user SHALL NOT have access to: system configuration, device management

#### Scenario: Viewer can only view
- **WHEN** user with Viewer role is authenticated
- **THEN** user SHALL have access to: dashboard (read-only), violation list (read-only)
- **AND** user SHALL NOT have access to: alert acknowledgment, system configuration

### Requirement: User management (Admin only)
Admin users SHALL be able to create, modify, and deactivate user accounts.

#### Scenario: Create new user
- **WHEN** Admin creates user with username, password, and role
- **THEN** system SHALL create user account with specified role

#### Scenario: Deactivate user
- **WHEN** Admin deactivates a user
- **THEN** user SHALL NOT be able to log in
- **AND** existing sessions SHALL be invalidated
