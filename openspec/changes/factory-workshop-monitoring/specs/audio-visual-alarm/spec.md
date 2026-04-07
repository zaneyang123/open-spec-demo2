## ADDED Requirements

### Requirement: Alarm trigger
The system SHALL trigger audio-visual alarms within 1 second of receiving a confirmed violation detection (confidence ≥ 85%, 3-frame confirmation).

#### Scenario: Alarm triggered on violation
- **WHEN** violation detection meets confidence threshold and frame confirmation
- **THEN** system SHALL send MQTT message to alarm device within 1 second
- **AND** alarm device SHALL activate within 1 second of receiving message

#### Scenario: Alarm auto-stop
- **WHEN** alarm has been active for configured duration (default 10 seconds)
- **THEN** system SHALL automatically send stop command to alarm device

#### Scenario: Alarm throttling
- **WHEN** same camera triggers more than 3 alarms within 1 minute
- **THEN** system SHALL throttle further alarms from that camera for 5 minutes

### Requirement: Alarm configuration
The system SHALL allow administrators to configure alarm volume and duration.

#### Scenario: Configure alarm volume
- **WHEN** administrator sets alarm volume to level 7
- **THEN** alarm device SHALL emit sound at the configured volume level

#### Scenario: Configure alarm duration
- **WHEN** administrator sets alarm duration to 15 seconds
- **THEN** alarm SHALL automatically stop after 15 seconds
