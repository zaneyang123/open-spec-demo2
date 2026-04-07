## ADDED Requirements

### Requirement: Continuous video recording
The system SHALL continuously record video from all cameras at ≥1080P resolution.

#### Scenario: Recording starts on camera connection
- **WHEN** camera connects to recording service
- **THEN** system SHALL begin recording video within 5 seconds

#### Scenario: Recording format
- **WHEN** video is recorded
- **THEN** format SHALL be H.264/H.265 encoded MP4 or FLV

#### Scenario: Recording on storage failure
- **WHEN** NAS storage is unavailable
- **THEN** system SHALL continue attempting to write and SHALL log error
- **AND** system SHALL resume recording when storage becomes available

### Requirement: Violation clip preservation
The system SHALL save video clips containing violation events with pre and post context.

#### Scenario: Violation clip capture
- **WHEN** violation is detected
- **THEN** system SHALL save video clip starting 10 seconds before detection
- **AND** system SHALL continue recording until 10 seconds after alarm triggers

#### Scenario: Clip metadata
- **WHEN** violation clip is saved
- **THEN** clip metadata SHALL include: camera_id, start_time, end_time, violation_type, confidence_score

#### Scenario: Clip storage management
- **WHEN** storage utilization reaches 80%
- **THEN** system SHALL send alert to administrators
- **AND** oldest clips SHALL be automatically deleted according to retention policy

### Requirement: Video playback
The system SHALL support playback of recorded video via web interface.

#### Scenario: Live view playback
- **WHEN** user selects a camera in dashboard
- **THEN** system SHALL display live video stream with <3 second latency

#### Scenario: Historical playback
- **WHEN** user selects time range for specific camera
- **THEN** system SHALL retrieve and play video from storage
