## ADDED Requirements

### Requirement: Violation data dashboard
The system SHALL provide a web dashboard displaying violation statistics.

#### Scenario: Dashboard overview
- **WHEN** supervisor accesses dashboard
- **THEN** system SHALL display: total violations today, violations by camera, violations by hour chart

#### Scenario: Filter by time range
- **WHEN** user selects custom date range
- **THEN** dashboard SHALL update all statistics for selected period

#### Scenario: Filter by camera/area
- **WHEN** user selects specific camera or area
- **THEN** dashboard SHALL filter statistics to show only data from selected scope

### Requirement: Violation data drill-down
The system SHALL allow users to view detailed violation records.

#### Scenario: View violation details
- **WHEN** user clicks on a violation in statistics
- **THEN** system SHALL show: timestamp, camera, snapshot, video clip, acknowledgment status

#### Scenario: Violation list pagination
- **WHEN** violation list has more than 50 items
- **THEN** system SHALL paginate results with 50 items per page
