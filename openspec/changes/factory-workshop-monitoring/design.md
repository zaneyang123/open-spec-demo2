## Context

Factory workshop intelligent monitoring system aims to detect employees playing with phones in real-time and trigger audio-visual alarms. The system must handle 50 camera points with <2s detection latency and <5s notification latency, operating 24/7 with 99% detection accuracy.

**Current State**: No existing monitoring system. Need to build from scratch.

**Constraints**:
- Hardware budget: <500 RMB per camera, total system ≤200,000 RMB
- Single camera resolution: ≥1080P
- Detection response time: <2 seconds
- Alarm trigger latency: <1 second
- Notification latency: <5 seconds

**Stakeholders**: Workshop managers, supervisors/team leaders, security staff

## Goals / Non-Goals

**Goals:**
- Real-time phone usage detection using computer vision AI
- Instant audio-visual alarm when violations detected
- Continuous video recording with violation clip preservation
- Alert push to designated supervisors
- Violation data dashboard and report export
- Role-based access control

**Non-Goals:**
- Facial recognition / employee identification
- License plate detection
- Multi-factory centralized management (single factory scope)
- Integration with ERP/MES systems (Phase 1)
- Mobile app development (web-based only)

## Decisions

### 1. Architecture: Edge + Cloud Hybrid

**Decision**: Deploy AI inference at edge (camera-adjacent servers) for low latency, with cloud for storage and web dashboard.

**Rationale**:
- 50 cameras streaming simultaneously requires significant bandwidth; edge inference reduces bandwidth by sending only alerts vs full video streams
- <2s detection requirement is challenging with cloud-only architecture (network latency)
- Local storage ensures data security and reduces cloud costs

**Alternatives Considered**:
- Cloud-only: Lower hardware cost but network latency risks violating <2s requirement
- Full edge: Better latency but higher hardware cost and harder to manage 50 edge devices

### 2. Video Streaming: RTSP + HTTP FLV

**Decision**: Use RTSP for camera-to-server streaming, HTTP FLV for server-to-browser playback.

**Rationale**:
- RTSP is standard protocol supported by most IP cameras
- HTTP FLV works through standard firewalls without special ports
- FFmpeg handles RTSP ingestion and conversion efficiently

**Alternatives Considered**:
- WebRTC: Lower latency but complex setup, browser compatibility issues
- HLS: Low latency version (LL-HLS) available but still higher latency than FLV

### 3. AI Detection: YOLOv8-based Model

**Decision**: Use YOLOv8 for object detection, fine-tuned for phone detection.

**Rationale**:
- YOLOv8 offers best accuracy/speed tradeoff for real-time detection
- Open-source with extensive community support
- Can be fine-tuned on factory-specific data after initial deployment
- Pre-trained model can detect phones immediately

**Alternatives Considered**:
- MediaPipe: Lighter but less accurate for small object detection
- Custom CNN: Higher accuracy but requires significant training data and compute

### 4. Alarm Control: MQTT-based IoT Protocol

**Decision**: Use MQTT for alarm device control between detection server and告警 devices.

**Rationale**:
- MQTT is lightweight IoT protocol with minimal overhead
- Pub/sub model allows easy scaling to multiple alarm devices
- QoS levels ensure reliable message delivery
- Widely supported by ESP32/Arduino-based alarm hardware

**Alternatives Considered**:
- HTTP/REST: Simpler but polling required; not real-time friendly
- WebSocket: Bidirectional but heavier than MQTT for IoT use cases

### 5. Data Storage: Local NAS + PostgreSQL

**Decision**: Store video on local NAS, structured data in PostgreSQL.

**Rationale**:
- Video storage is large; local NAS is cost-effective for 50-camera system
- PostgreSQL handles time-series violation data efficiently
- Separation allows independent scaling

**Alternatives Considered**:
- Cloud storage: Higher latency for video playback, ongoing costs
- Object storage (S3-compatible): Good for large files but overkill for this scale

### 6. Web Framework: FastAPI + React

**Decision**: FastAPI for backend API, React for frontend dashboard.

**Rationale**:
- FastAPI: High-performance async Python framework, automatic API docs, Pydantic validation
- React: Component-based, good ecosystem for dashboard development
- TypeScript provides type safety across frontend/backend

**Alternatives Considered**:
- Django: Heavier, slower request handling
- Vue.js: Also viable but team familiarity with React assumed

## Risks / Trade-offs

- [Risk] Low light conditions affect detection accuracy → Mitigation: Recommend IR-capable cameras; apply image preprocessing (contrast enhancement)
- [Risk] Multiple violations simultaneously (multiple people on phones) → Mitigation: Detection queue with configurable batch size; alarm throttling to prevent alert flooding
- [Risk] Storage growth without management → Mitigation: Implement automatic cleanup policy; alert when storage reaches 80% capacity
- [Risk] False positives cause unnecessary alarms → Mitigation: Confidence threshold of 85%; 3-frame confirmation before triggering alarm
- [Risk] Network congestion affects 50-camera streaming → Mitigation: VLAN segmentation; QoS prioritization for RTSP streams
- [Trade-off] Edge inference increases hardware cost → Accept given latency requirements and 20万 budget allows headroom

## Migration Plan

**Phase 1 - Infrastructure (Week 1-2)**:
1. Deploy network switches and cabling for camera connectivity
2. Set up edge inference servers (2-3 servers for ~50 cameras)
3. Configure NAS storage
4. Deploy PostgreSQL database

**Phase 2 - Core System (Week 3-4)**:
1. Deploy video streaming infrastructure (FFmpeg + media server)
2. Integrate AI detection models
3. Implement alarm control via MQTT
4. Basic monitoring dashboard

**Phase 3 - Full Feature (Week 5-6)**:
1. Complete alert notification system
2. Statistics and report export
3. Permission management
4. Device management interface

**Phase 4 - Testing & Deployment (Week 7-8)**:
1. System integration testing
2. Performance testing with all 50 cameras
3. User acceptance testing
4. Production deployment

**Rollback**: Keep existing manual monitoring process during pilot; can disable system entirely if critical issues arise.

## Open Questions

1. **Video retention period**: 7 days, 30 days, or 90 days? (Storage cost varies significantly)
2. **Notification channels**: APP push, SMS, or instant messaging (WeChat/钉钉)? Cost and complexity differ.
3. **Camera distribution**: Exact placement of 50 cameras by area/zone TBD with workshop managers.
4. **Alarm sound level**: Configurable but initial default? Must balance alert effectiveness vs noise pollution.
5. **Night/weekend operation**: Full 24/7 or specific working hours only?
