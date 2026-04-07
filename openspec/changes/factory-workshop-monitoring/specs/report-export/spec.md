## ADDED Requirements

### Requirement: Report generation
The system SHALL generate statistical reports on violation data.

#### Scenario: Generate Excel report
- **WHEN** user requests report with format "Excel"
- **THEN** system SHALL generate .xlsx file containing: summary statistics, violations by camera table, violations by time chart data

#### Scenario: Generate PDF report
- **WHEN** user requests report with format "PDF"
- **THEN** system SHALL generate .pdf file with formatted tables and charts

### Requirement: Report content
Reports SHALL include configurable time range and violation categories.

#### Scenario: Report with custom date range
- **WHEN** user sets report date range from 2026-03-01 to 2026-03-31
- **THEN** report SHALL include only violations within that date range

#### Scenario: Report export download
- **WHEN** report generation completes
- **THEN** system SHALL provide download link valid for 24 hours
