## 1. Infrastructure Setup

- [ ] 1.1 Set up network switches and VLAN configuration for camera network
- [ ] 1.2 Deploy 2-3 edge inference servers with GPU support
- [ ] 1.3 Configure NAS storage with sufficient capacity for 50-camera recording
- [ ] 1.4 Set up PostgreSQL database with schema for violations, alerts, users, devices
- [ ] 1.5 Configure MQTT broker (Mosquitto) for alarm device communication

## 2. Video Streaming Infrastructure

- [ ] 2.1 Deploy FFmpeg for RTSP ingestion from all 50 cameras
- [ ] 2.2 Set up media server (SRS or similar) for HTTP FLV streaming
- [ ] 2.3 Implement video recording service with NAS storage integration
- [ ] 2.4 Implement violation clip capture with pre/post context buffering
- [ ] 2.5 Set up WebSocket server for live video playback to browser

## 3. AI Detection Service

- [ ] 3.1 Set up YOLOv8 model environment with GPU acceleration
- [ ] 3.2 Implement camera video stream consumer
- [ ] 3.3 Implement phone detection inference pipeline
- [ ] 3.4 Add confidence threshold filtering (85% minimum)
- [ ] 3.5 Implement 3-frame confirmation before alarm trigger
- [ ] 3.6 Add low-light image preprocessing (contrast enhancement)
- [ ] 3.7 Create detection output API for alarm service integration

## 4. Alarm Control System

- [ ] 4.1 Implement MQTT alarm control client
- [ ] 4.2 Implement alarm trigger logic with 1-second latency requirement
- [ ] 4.3 Add configurable alarm duration (default 10 seconds)
- [ ] 4.4 Implement alarm throttling (3 alarms/minute per camera limit)
- [ ] 4.5 Create alarm device management (volume, duration configuration)
- [ ] 4.6 Add alarm auto-stop timer functionality

## 5. Web Dashboard Backend

- [ ] 5.1 Set up FastAPI project structure
- [ ] 5.2 Implement authentication endpoint with session management
- [ ] 5.3 Implement role-based access control middleware
- [ ] 5.4 Create violation alert API endpoints
- [ ] 5.5 Implement statistics aggregation endpoints
- [ ] 5.6 Add report generation endpoints (Excel/PDF)
- [ ] 5.7 Implement device management API (status, restart)

## 6. Web Dashboard Frontend

- [ ] 6.1 Set up React project with TypeScript
- [ ] 6.2 Implement login page with authentication
- [ ] 6.3 Create main dashboard with live camera grid
- [ ] 6.4 Add video playback component with WebSocket integration
- [ ] 6.5 Implement violation statistics charts and filters
- [ ] 6.6 Create alert notification panel with acknowledgment
- [ ] 6.7 Build user management interface (Admin)
- [ ] 6.8 Build device management interface with status indicators

## 7. Alert Notification System

- [ ] 7.1 Implement WebSocket push for real-time alerts to dashboard
- [ ] 7.2 Add alert storage with PostgreSQL
- [ ] 7.3 Implement alert acknowledgment workflow
- [ ] 7.4 Add notification retry mechanism with exponential backoff
- [ ] 7.5 Create alert query and filtering API

## 8. Report Export System

- [ ] 8.1 Implement statistics aggregation service
- [ ] 8.2 Add Excel generation using openpyxl
- [ ] 8.3 Add PDF generation using reportlab
- [ ] 8.4 Implement report download with time-limited links
- [ ] 8.5 Add configurable date range and camera filters

## 9. System Integration & Testing

- [ ] 9.1 Integrate all services end-to-end
- [ ] 9.2 Perform load testing with 50 cameras streaming simultaneously
- [ ] 9.3 Test detection latency (<2s requirement)
- [ ] 9.4 Test alarm trigger latency (<1s requirement)
- [ ] 9.5 Test notification latency (<5s requirement)
- [ ] 9.6 User acceptance testing with workshop managers
- [ ] 9.7 Security testing (authentication, authorization)
