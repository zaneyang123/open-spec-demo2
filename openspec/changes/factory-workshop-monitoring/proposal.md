## Why

Factory workshops face critical management challenges: employees using phones during work hours (risking trade secret leaks), productivity loss from laziness, and high manual inspection costs. A 24/7 intelligent vision monitoring system is needed to automatically detect phone usage violations and trigger real-time alerts, reducing management burden while ensuring product quality and security.

## What Changes

- **New System**: AI-powered vision monitoring system for factory workshops
- **Real-time Detection**: Computer vision AI detects employees playing with phones (玩手机行为检测)
- **Audio-Visual Alarm**: Triggers sound/light alerts within 1 second of violation detection
- **Video Recording**: Continuous 1080P recording with violation clips preserved for traceability
- **Alert Notification**: Pushes violation alerts to supervisors within 5 seconds
- **Data Statistics**: Violation data analysis by time/area/personnel dimensions
- **Report Export**: Generate Excel/PDF statistical reports
- **Permission Management**: Role-based access control (admin/supervisor/viewer)
- **Device Management**: Camera and alarm device status monitoring

## Capabilities

### New Capabilities

- `phone-usage-detection`: AI vision-based real-time detection of employees using/playing with phones during work hours, marking violation targets on监控画面
- `audio-visual-alarm`: Triggers audible alerts and flashing lights when violations detected; configurable duration and volume
- `video-recording`: Continuous video recording of监控区域, automatic violation clip preservation with pre/post context
- `alert-notification`: Pushes violation alerts (time, location, image/video) to designated managers via multiple channels
- `violation-statistics`: Dashboard for violation data analysis by time/camera/area with drill-down support
- `report-export`: Export violation statistics as Excel/PDF reports
- `permission-management`: Multi-level role-based access control (admin/supervisor/viewer)
- `device-management`: Camera and告警设备 status monitoring and remote configuration

### Modified Capabilities

(No existing capabilities being modified)

## Impact

- **New Systems**: AI detection service,告警 service, video storage service
- **Hardware**: ~50 IP cameras (cost <500 RMB each),告警 devices (sound lights)
- **Network**: Requires stable LAN for video streaming from 50 cameras
- **Storage**: Local storage for video recordings (capacity depends on retention policy)
- **Integration**: May integrate with existing factory management systems
