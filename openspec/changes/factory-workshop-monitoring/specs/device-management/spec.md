## ADDED Requirements

### Requirement: Device status monitoring
The system SHALL monitor online/offline status of all cameras and alarm devices.

#### Scenario: Camera online status
- **WHEN** camera sends heartbeat within 30 seconds
- **THEN** system SHALL show camera as "Online"

#### Scenario: Camera offline status
- **WHEN** camera fails to send heartbeat for 60 seconds
- **THEN** system SHALL show camera as "Offline"
- **AND** system SHALL send alert to administrators

### Requirement: Device information display
The system SHALL display device details including IP address, location, and model.

#### Scenario: View camera details
- **WHEN** user clicks on camera in device list
- **THEN** system SHALL display: camera_id, IP_address, location, model, status, last_heartbeat

### Requirement: Device remote restart (Admin only)
Administrators SHALL be able to restart cameras and alarm devices remotely.

#### Scenario: Restart camera
- **WHEN** Admin clicks "Restart" on camera device
- **THEN** system SHALL send restart command to camera
- **AND** camera SHALL reboot and reconnect within 2 minutes
