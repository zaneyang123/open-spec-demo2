## ADDED Requirements

### Requirement: Phone usage detection
The system SHALL use computer vision AI to analyze camera video streams in real-time and detect when employees are using or playing with phones.

#### Scenario: Single person using phone
- **WHEN** one employee holds a phone to their ear or looks at a phone screen for more than 3 seconds
- **THEN** system SHALL mark the detected phone with a bounding box and confidence score ≥ 85%

#### Scenario: Multiple people using phones simultaneously
- **WHEN** more than one person in the camera view is using a phone
- **THEN** system SHALL detect and mark each person with independent bounding boxes

#### Scenario: Detection confidence below threshold
- **WHEN** AI detection confidence is between 50% and 85%
- **THEN** system SHALL log the detection but SHALL NOT trigger an alarm

#### Scenario: Low light condition
- **WHEN** ambient light is below 50 lux
- **THEN** system SHALL apply image preprocessing (contrast enhancement) before detection

#### Scenario: Detection latency
- **WHEN** video frame arrives at detection service
- **THEN** system SHALL complete detection and return results within 500ms

### Requirement: Detection output format
The detection service SHALL output structured results containing timestamp, camera_id, bounding_box coordinates, detection_class, and confidence_score.

#### Scenario: Valid detection output
- **WHEN** detection completes successfully
- **THEN** output SHALL include: timestamp (ISO 8601), camera_id, box {x1, y1, x2, y2}, class "phone", confidence 0.0-1.0

#### Scenario: No detection output
- **WHEN** no phone usage is detected in frame
- **THEN** output SHALL indicate empty detection list for that timestamp
