# SHIELD-AI: Multi-Layer Missile Defense Simulation
### Project Roadmap & Architecture Document
**Version:** 1.0  
**Author:** Muhammad Ahmad Khan  
**Status:** Planning Phase

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Goals](#2-goals)
3. [Tools & Technologies](#3-tools--technologies)
4. [System Architecture](#4-system-architecture)
5. [Communication Protocol (Unity ↔ Python)](#5-communication-protocol-unity--python)
6. [Threat System Design](#6-threat-system-design)
7. [Defense System Design](#7-defense-system-design)
8. [AI & Decision Engine](#8-ai--decision-engine)
9. [Expandability Design](#9-expandability-design)
10. [Project Roadmap](#10-project-roadmap)
11. [File Structure](#11-file-structure)
12. [Configuration Reference](#12-configuration-reference)

---

## 1. Project Overview

SHIELD-AI is a real-time missile defense simulation system that models a 3-layer air defense network defending a city against multiple types of incoming missile threats. The system combines a Unity 3D simulation engine for visualization with a Python AI backend for threat tracking, classification, and interception decision-making.

The project is designed as a **digital twin** of a layered missile defense scenario — conceptually similar to the Iron Dome, David's Sling, and Arrow defense systems — built for research, simulation, and AI decision-making study.

> **Important:** This is a pure simulation/research system. No real weapon behavior, classified data, or real-world targeting information is used or intended.

---

## 2. Goals

### 2.1 Primary Goals

| Goal | Description |
|------|-------------|
| **Simulate 3 threat types** | Ballistic, Cruise, and Hypersonic missiles with distinct behaviors |
| **Simulate 3 defense layers** | Arrow (long-range), David's Sling (mid-range), Iron Dome (short-range) |
| **AI threat classification** | ML model classifies incoming threats by type and danger level |
| **AI interception decisions** | BMC (Battle Management Computer) decides when, what, and how many interceptors to fire |
| **Realistic failure modeling** | Probability of Kill (Pk) system simulates real-world interception failures |
| **Real-time visualization** | Unity 3D scene showing radar, trajectories, intercepts, and city status |

### 2.2 Secondary Goals

| Goal | Description |
|------|-------------|
| **Expandability** | Plugin architecture — new missiles and defense layers require zero changes to core |
| **Config-driven** | All parameters (speed, Pk, range) live in JSON config, not hardcoded |
| **Self-generating training data** | Simulation generates its own ML training data |
| **Replay system** | Deterministic simulation clock enables scenario replay |
| **Research quality** | System is structured to support a research paper or academic report |

### 2.3 Success Criteria

- [ ] All 3 missile types simulate correct flight paths
- [ ] All 3 defense layers detect, track, and attempt interception
- [ ] Layer handoff works (Layer 3 miss → Layer 2 engages → Layer 1 last resort)
- [ ] Pk system produces realistic failure rates
- [ ] Unity visualizes all events in real-time
- [ ] Python AI classifies threats with >85% accuracy
- [ ] System runs a full attack scenario end-to-end without crashes

---

## 3. Tools & Technologies

### 3.1 Python AI Backend

| Tool | Purpose | Version |
|------|---------|---------|
| **Python** | Core language | 3.10+ |
| **NumPy** | Vector math, trajectory calculations | Latest |
| **FilterPy** | Kalman filter multi-object tracking | Latest |
| **SciPy** | Hungarian algorithm (data association) | Latest |
| **scikit-learn** | Threat classifier (Random Forest / SVM) | Latest |
| **PyTorch** *(optional)* | Neural network for advanced BMC decisions | Latest |
| **asyncio** | Async socket communication with Unity | Built-in |
| **PyYAML / JSON** | Config file loading | Built-in |
| **Matplotlib** | Headless trajectory debugging plots | Latest |

### 3.2 Unity Simulation Engine

| Tool | Purpose | Version |
|------|---------|---------|
| **Unity** | 3D simulation engine | 2022 LTS+ |
| **C#** | Unity scripting language | .NET 6+ |
| **Unity Particle System** | Explosion, radar sweep effects | Built-in |
| **Unity UI Toolkit** | Real-time dashboard | Built-in |
| **Unity LineRenderer** | Trajectory and prediction line drawing | Built-in |
| **Newtonsoft JSON** | JSON parsing for socket messages | NuGet |

### 3.3 Communication Layer

| Tool | Purpose |
|------|---------|
| **TCP Sockets** | Primary Unity ↔ Python bridge |
| **JSON** | Message serialization format |
| **asyncio (Python)** | Non-blocking socket server |
| **System.Net.Sockets (C#)** | Unity TCP client |

### 3.4 Development Tools

| Tool | Purpose |
|------|---------|
| **VS Code** | Python development |
| **Visual Studio / Rider** | Unity C# development |
| **Git** | Version control |
| **Jupyter Notebook** | Algorithm prototyping and visualization |

---

## 4. System Architecture

### 4.1 High-Level Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     UNITY ENGINE                        │
│                                                         │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐  │
│  │  3D World   │  │  Radar Viz   │  │   Dashboard   │  │
│  │  Missiles   │  │  Sweep FX    │  │  Risk Scores  │  │
│  │ Interceptors│  │  Track Lines │  │  City Health  │  │
│  └─────────────┘  └──────────────┘  └───────────────┘  │
│                          │                              │
│                   Unity TCP Client                      │
└──────────────────────────┼──────────────────────────────┘
                           │  JSON over TCP
                           │  Port 5000
┌──────────────────────────┼──────────────────────────────┐
│                   PYTHON AI CORE                        │
│                          │                              │
│                   Socket Server                         │
│                          │                              │
│  ┌────────────┐  ┌───────────────┐  ┌───────────────┐  │
│  │  Sensor    │  │    Multi-     │  │   Threat      │  │
│  │  Fusion    │→ │    Object     │→ │  Classifier   │  │
│  │  Module    │  │   Tracker     │  │  (ML Model)   │  │
│  └────────────┘  └───────────────┘  └───────┬───────┘  │
│                                             │           │
│                                    ┌────────▼───────┐   │
│                                    │  BMC Decision  │   │
│                                    │    Engine      │   │
│                                    │ (AI/Rules)     │   │
│                                    └────────┬───────┘   │
└─────────────────────────────────────────────┼───────────┘
                                              │
                           ┌──────────────────▼──────────┐
                           │   Interception Physics      │
                           │   Proportional Navigation   │
                           │   Pk Probability Engine     │
                           └─────────────────────────────┘
```

### 4.2 Python Module Architecture

```
python/
├── core/
│   ├── sim_clock.py          # Central simulation time controller
│   ├── event_bus.py          # Event system (pub/sub)
│   └── config_loader.py      # JSON config loader
│
├── threats/
│   ├── base_missile.py       # Abstract base class
│   ├── ballistic_missile.py  # Parabolic trajectory
│   ├── cruise_missile.py     # Waypoint-following
│   └── hypersonic_missile.py # Glide + jitter
│
├── defense/
│   ├── base_layer.py         # Abstract defense layer
│   ├── arrow_system.py       # Long-range (Layer 3)
│   ├── davids_sling.py       # Mid-range (Layer 2)
│   ├── iron_dome.py          # Short-range (Layer 1)
│   ├── base_radar.py         # Abstract radar
│   └── base_bmc.py           # Abstract BMC (AI brain)
│
├── ai/
│   ├── kalman_tracker.py     # Multi-object Kalman filter
│   ├── data_association.py   # Hungarian algorithm
│   ├── threat_classifier.py  # ML threat classification
│   ├── bmc_rules.py          # Rule-based decision engine
│   └── bmc_rl.py             # RL-based engine (Phase 2)
│
├── physics/
│   ├── prop_nav.py           # Proportional navigation
│   ├── pk_engine.py          # Probability of Kill calculator
│   └── trajectory.py         # Trajectory math utilities
│
├── comms/
│   └── socket_server.py      # TCP socket bridge to Unity
│
├── simulation.py             # Main simulation loop
└── config.json               # All parameters
```

### 4.3 Unity Scene Architecture

```
Unity/
├── Scenes/
│   └── MainSimulation.unity
│
├── Scripts/
│   ├── Network/
│   │   ├── TCPClient.cs          # Socket connection to Python
│   │   └── MessageParser.cs      # JSON message handler
│   │
│   ├── Entities/
│   │   ├── MissileController.cs  # Controls missile movement
│   │   ├── InterceptorController.cs
│   │   └── ExplosionController.cs
│   │
│   ├── Visualization/
│   │   ├── RadarSweep.cs         # Radar sweep animation
│   │   ├── TrajectoryRenderer.cs # LineRenderer for paths
│   │   └── PredictionRenderer.cs # Predicted impact lines
│   │
│   └── UI/
│       ├── DashboardController.cs
│       ├── ThreatListUI.cs
│       └── CityHealthBar.cs
│
└── Prefabs/
    ├── BallisticMissile.prefab
    ├── CruiseMissile.prefab
    ├── HypersonicMissile.prefab
    ├── Interceptor.prefab
    └── ExplosionFX.prefab
```

---

## 5. Communication Protocol (Unity ↔ Python)

### 5.1 Connection Setup

```
Python (Server)          Unity (Client)
    │                        │
    │  TCP Server on :5000   │
    │◄───────────────────────│ Connect
    │───────────────────────►│ ACK
    │                        │
    │  60 FPS update loop    │
    │◄───────────────────────│ SensorData (every frame)
    │───────────────────────►│ AIResponse (every frame)
```

### 5.2 Message Format

All messages are **newline-delimited JSON** (`\n` terminates each message).

---

**Unity → Python: Sensor Data**

Sent every frame. Contains all currently simulated object positions.

```json
{
  "type": "sensor_data",
  "timestamp": 1234567890.123,
  "frame": 420,
  "objects": [
    {
      "id": "missile_001",
      "position": {"x": 1200.5, "y": 8500.0, "z": -300.2},
      "velocity": {"x": -150.0, "y": -200.0, "z": 50.0},
      "detected_by_layer": 3
    },
    {
      "id": "missile_002",
      "position": {"x": 800.0, "y": 200.0, "z": 100.0},
      "velocity": {"x": -80.0, "y": 0.0, "z": 20.0},
      "detected_by_layer": 1
    }
  ]
}
```

---

**Python → Unity: AI Response**

Sent every frame. Contains tracking output, predictions, and commands.

```json
{
  "type": "ai_response",
  "timestamp": 1234567890.145,
  "tracks": [
    {
      "id": "missile_001",
      "threat_type": "ballistic",
      "confidence": 0.94,
      "risk_score": 0.87,
      "predicted_impact": {"x": 0.0, "y": 0.0, "z": 0.0},
      "predicted_impact_time": 12.5,
      "assigned_layer": 3,
      "state": "tracked"
    }
  ],
  "commands": [
    {
      "action": "fire_interceptor",
      "layer": 3,
      "target_id": "missile_001",
      "interceptor_count": 2,
      "intercept_point": {"x": 600.0, "y": 5000.0, "z": -100.0}
    }
  ],
  "city_status": {
    "health": 85,
    "hits": 1
  }
}
```

---

**Python → Unity: Event Notifications**

Sent on discrete events (not every frame).

```json
{
  "type": "event",
  "event": "intercept_result",
  "target_id": "missile_001",
  "interceptor_id": "interceptor_003",
  "result": "success",
  "pk_rolled": 0.72,
  "pk_threshold": 0.80,
  "layer": 3,
  "position": {"x": 600.0, "y": 5000.0, "z": -100.0}
}
```

| Event Type | Trigger |
|------------|---------|
| `intercept_result` | Interceptor hits or misses |
| `layer_handoff` | Threat passed to next layer |
| `city_hit` | Missile reaches city |
| `threat_detected` | New object enters radar range |
| `threat_destroyed` | Missile successfully intercepted |
| `wave_complete` | All threats in wave resolved |

---

### 5.3 Update Rate

| Channel | Rate | Reason |
|---------|------|--------|
| Sensor data (Unity → Python) | 60 Hz | Match Unity frame rate |
| AI response (Python → Unity) | 60 Hz | Smooth visualization |
| Event notifications | On-demand | Async, not frame-locked |

---

## 6. Threat System Design

### 6.1 Missile Types Comparison

| Property | Ballistic | Cruise | Hypersonic |
|----------|-----------|--------|------------|
| Speed (km/h) | 14,000–25,000 | 800–1,000 | 18,000–36,000+ |
| Altitude | Very high (exo-atm) | Very low (50–100m) | High then glide |
| Trajectory | Fixed parabola | Waypoints | Ballistic + glide |
| Predictability | High | Medium | Very low |
| Detection layer | Layer 3 (early) | Layer 1-2 (late) | Layer 3 (early) |
| Simulation method | Parabolic math | Lerp + waypoints | Parabola + jitter |

### 6.2 Trajectory Math

**Ballistic Missile (Parabolic Arc)**

```python
# Simple 3D parabolic trajectory
def update(self, dt):
    self.velocity.y += GRAVITY * dt        # gravity pulls down
    self.position   += self.velocity * dt  # integrate position
    # That's it. Beautiful.
```

**Cruise Missile (Waypoint Following)**

```python
# Lerp between waypoints at fixed low altitude
def update(self, dt):
    target = self.waypoints[self.current_waypoint]
    direction = normalize(target - self.position)
    self.position += direction * self.speed * dt

    if distance(self.position, target) < THRESHOLD:
        self.current_waypoint += 1   # advance to next waypoint
```

**Hypersonic Missile (Ballistic + Glide Phase + Jitter)**

```python
def update(self, dt):
    if self.altitude > GLIDE_THRESHOLD:
        # Phase 1: Ballistic arc (same as ballistic missile)
        self.velocity.y += GRAVITY * dt
    else:
        # Phase 2: Glide toward target + random jitter
        direction = normalize(self.target - self.position)
        jitter = random.uniform(-JITTER_MAGNITUDE, JITTER_MAGNITUDE)
        self.velocity = direction * self.speed + jitter
    
    self.position += self.velocity * dt
```

### 6.3 Threat Detection Rules

| Missile Type | Detected By | Reason |
|-------------|-------------|--------|
| Ballistic | Layer 3 first | High altitude, early detection |
| Hypersonic | Layer 3 first | Fast but high altitude launch |
| Cruise | Layer 2 or 1 | Low altitude hides from long-range radar |

---

## 7. Defense System Design

### 7.1 Defense Layers Overview

| Layer | System | Range | Pk Base | Handles |
|-------|--------|-------|---------|---------|
| 3 (outermost) | Arrow | 2,400 km | 80% | Ballistic, Hypersonic |
| 2 (mid) | David's Sling | 300 km | 75% | Ballistic, Cruise, Hypersonic |
| 1 (innermost) | Iron Dome | 70 km | 90% | Cruise, short-range |

### 7.2 Interceptor Guidance: Proportional Navigation

Real missiles use Proportional Navigation (PN). We implement it for all interceptors.

```
Core idea: Don't chase the missile. Aim at where it WILL BE.

If the Line-Of-Sight angle between interceptor and target 
is NOT rotating → you are on a collision course → do nothing
If it IS rotating → correct your heading to stop the rotation
```

```python
def proportional_navigation(interceptor, target, dt, N=4):
    """
    N = navigation constant (typically 3-5)
    Higher N = more aggressive corrections
    """
    # Line of sight vector
    los = target.position - interceptor.position
    los_direction = normalize(los)
    
    # Rate of change of LOS angle
    los_rate = cross(los_direction, target.velocity - interceptor.velocity) / magnitude(los)
    
    # Commanded acceleration
    acceleration = N * interceptor.speed * los_rate
    
    # Update interceptor velocity
    interceptor.velocity += acceleration * dt
    interceptor.position += interceptor.velocity * dt
```

### 7.3 Probability of Kill (Pk) Engine

The Pk engine determines if an interception succeeds or fails on each attempt.

```python
def calculate_pk(missile, base_pk, active_threats):
    pk = base_pk
    
    # Missile type modifiers
    if missile.type == "hypersonic":
        pk -= 0.30    # Very hard to kill
    
    # Maneuvering penalty
    if missile.is_maneuvering:
        pk -= 0.15
    
    # Saturation penalty (too many simultaneous threats)
    if active_threats > 3:
        pk -= 0.15
    
    # Clamp between 0 and 1
    pk = max(0.0, min(1.0, pk))
    
    # Roll the dice
    return random.random() < pk
```

### 7.4 Layer Handoff Logic

```
Threat enters Layer 3 range?
    YES → Arrow evaluates threat
        → Fires 1 interceptor (2 if hypersonic)
        → Pk roll → SUCCESS → destroy missile
                  → FAIL    → emit "layer_handoff" event
                              → Layer 2 takes over
                              → David's Sling fires
                              → Pk roll → SUCCESS → destroy
                                        → FAIL    → Layer 1 takes over
                                                    → Iron Dome fires
                                                    → Pk roll → SUCCESS → destroy
                                                              → FAIL    → CITY HIT

Cruise missile detected by Layer 2 first?
    → Skip Layer 3
    → David's Sling engages directly
```

---

## 8. AI & Decision Engine

### 8.1 Multi-Object Tracking Pipeline

```
Raw sensor positions (noisy)
         │
         ▼
  ┌─────────────┐
  │   Kalman    │  ← Reduces noise, smooths position estimates
  │   Filter    │
  └──────┬──────┘
         │
         ▼
  ┌─────────────┐
  │  Hungarian  │  ← Matches detections to existing tracks
  │  Algorithm  │     (solves "which blob is which missile?")
  └──────┬──────┘
         │
         ▼
  ┌─────────────┐
  │   Track     │  ← Maintains consistent ID per missile
  │  Manager    │     even when temporarily lost
  └──────┬──────┘
         │
         ▼
  Stable tracks with ID, position, velocity, history
```

### 8.2 Threat Classifier (ML Model)

The classifier identifies what type of missile each track is.

**Input Features:**

| Feature | Description |
|---------|-------------|
| `speed` | Magnitude of velocity vector |
| `altitude` | Current Y position |
| `trajectory_angle` | Angle of descent |
| `altitude_change_rate` | dAlt/dt |
| `velocity_variance` | Jitter indicator (hypersonic) |
| `estimated_range` | Distance from city |

**Model:** Random Forest (start simple, upgrade to neural network later)

**Training Data:** Generated by the simulation itself

```python
# Auto-generate training data during simulation
def log_track_for_training(track, true_label):
    features = extract_features(track)
    dataset.append({
        "features": features,
        "label": true_label   # "ballistic", "cruise", "hypersonic"
    })
# After 10,000 simulated launches → train classifier
```

**Output:**
```python
{
    "type": "ballistic",
    "confidence": 0.94,
    "risk_score": 0.87    # Composite: speed + altitude + time_to_impact
}
```

### 8.3 BMC Decision Engine

**Phase 1 — Rule-Based (Build First)**

```python
def decide(self, tracks, interceptor_inventory):
    commands = []
    
    for track in sorted(tracks, key=lambda t: t.risk_score, reverse=True):
        
        # Which layer should engage?
        layer = self.assign_layer(track)
        
        # How many interceptors?
        count = 2 if track.type == "hypersonic" else 1
        
        # Do we have inventory?
        if interceptor_inventory[layer] >= count:
            commands.append(FireCommand(layer, track, count))
            interceptor_inventory[layer] -= count
        else:
            # Pass to next available layer
            commands.append(LayerHandoff(track, layer - 1))
    
    return commands
```

**Phase 2 — Reinforcement Learning (Later)**

```
State:  [threat_count, threat_types, interceptor_inventory, city_health]
Action: [which_layer_fires, how_many_interceptors, priority_order]
Reward: +100 city survives full wave
        +10  per successful intercept
        -5   per wasted interceptor
        -50  per city hit
        -100 city destroyed

Train:  Self-play in simulation (no external data needed)
```

---

## 9. Expandability Design

### 9.1 Core Principle

> Adding a new missile type or defense layer must require **zero changes** to existing code. New behavior = new class + new config entry.

### 9.2 Base Classes (Never Modified)

```python
# base_missile.py
class Missile(ABC):
    def __init__(self, config: dict): ...
    
    @abstractmethod
    def update(self, dt: float) -> None:
        """Update position each timestep"""
    
    @abstractmethod
    def get_trajectory_preview(self) -> List[Vector3]:
        """Return next N predicted positions"""
    
    @property
    def position(self) -> Vector3: ...
    @property
    def velocity(self) -> Vector3: ...
    @property
    def is_active(self) -> bool: ...
```

```python
# base_layer.py
class DefenseLayer(ABC):
    def __init__(self, config: dict): ...
    
    @abstractmethod
    def can_engage(self, track: Track) -> bool:
        """Is this threat within our range and capability?"""
    
    @abstractmethod
    def engage(self, track: Track) -> FireCommand:
        """Return interception command"""
    
    @property
    def interceptor_count(self) -> int: ...
```

### 9.3 Adding New Components

| What to Add | Steps Required |
|------------|----------------|
| New missile type | 1. Create `drone_swarm.py` extending `Missile` 2. Add config entry |
| New defense layer | 1. Create `patriot_system.py` extending `DefenseLayer` 2. Add config entry |
| New AI strategy | 1. Create `bmc_aggressive.py` extending `BaseBMC` 2. Set in config |
| Multi-city scenario | Config change only — add multiple city targets |
| Replay mode | Already works via `sim_clock.py` deterministic seeding |

### 9.4 Event System

Components communicate through events, never directly.

```python
# event_bus.py
class EventBus:
    def subscribe(self, event_type: str, handler: Callable): ...
    def publish(self, event_type: str, data: dict): ...

# Usage
event_bus.subscribe("missile_detected", bmc.on_detection)
event_bus.subscribe("intercept_failed", next_layer.on_handoff)
event_bus.publish("missile_detected", {"id": "m001", "track": track})
```

---

## 10. Project Roadmap

### Phase 1 — Python Core (Weeks 1–2)

**Goal:** Working AI brain with no visuals.

| Task | Details | Done |
|------|---------|------|
| `sim_clock.py` | Central deterministic simulation clock | ☐ |
| `event_bus.py` | Publish/subscribe event system | ☐ |
| `config.json` | Full config file with all parameters | ☐ |
| `base_missile.py` | Abstract missile base class | ☐ |
| `ballistic_missile.py` | Parabolic trajectory math | ☐ |
| `cruise_missile.py` | Waypoint-following at low altitude | ☐ |
| `hypersonic_missile.py` | Ballistic + glide + jitter | ☐ |
| `kalman_tracker.py` | Multi-object Kalman filter | ☐ |
| `data_association.py` | Hungarian algorithm | ☐ |
| Terminal debug output | Print tracking results to console | ☐ |

**Milestone:** Run 3 missile types in headless simulation, see tracking output in terminal.

---

### Phase 2 — Defense Logic (Week 3)

**Goal:** Complete defense pipeline working in Python only.

| Task | Details | Done |
|------|---------|------|
| `base_layer.py` | Abstract defense layer class | ☐ |
| `arrow_system.py` | Layer 3 — long range, high altitude | ☐ |
| `davids_sling.py` | Layer 2 — mid range | ☐ |
| `iron_dome.py` | Layer 1 — short range, high Pk | ☐ |
| `prop_nav.py` | Proportional navigation guidance | ☐ |
| `pk_engine.py` | Probability of Kill calculator | ☐ |
| `bmc_rules.py` | Rule-based Battle Management Computer | ☐ |
| Layer handoff logic | Miss → pass to next layer | ☐ |
| City hit detection | Track damage when all layers fail | ☐ |

**Milestone:** Run full attack scenario. See intercept success/fail. Layer handoffs working.

---

### Phase 3 — Communication Bridge (Week 4)

**Goal:** Unity and Python talking in real-time.

| Task | Details | Done |
|------|---------|------|
| `socket_server.py` | Python async TCP server | ☐ |
| `TCPClient.cs` | Unity TCP client | ☐ |
| `MessageParser.cs` | JSON deserializer in Unity | ☐ |
| Message protocol | Define all JSON message types | ☐ |
| Sync test | Simple cube moves in Unity driven by Python | ☐ |
| Latency measurement | Confirm <16ms round trip (1 frame) | ☐ |

**Milestone:** Python moves objects in Unity via socket. No AI yet, just connection proof.

---

### Phase 4 — Unity Visualization (Weeks 5–6)

**Goal:** Full 3D scene with real-time visualization.

| Task | Details | Done |
|------|---------|------|
| 3D scene setup | Sky, ground, city model, defense zones | ☐ |
| Missile prefabs | 3 missile types with distinct models | ☐ |
| Interceptor prefabs | Per-layer distinct interceptors | ☐ |
| `RadarSweep.cs` | Rotating radar sweep effect per layer | ☐ |
| `TrajectoryRenderer.cs` | LineRenderer for flight paths | ☐ |
| `PredictionRenderer.cs` | Predicted impact point lines | ☐ |
| Explosion FX | Particle system on intercept/impact | ☐ |
| `DashboardController.cs` | Real-time threat list + risk scores | ☐ |
| `CityHealthBar.cs` | City damage bar | ☐ |
| Layer defense zone rings | Visual range rings per layer | ☐ |

**Milestone:** Watch a full attack scenario with all visuals running. It looks impressive.

---

### Phase 5 — AI Integration (Week 7)

**Goal:** ML threat classifier trained and running live.

| Task | Details | Done |
|------|---------|------|
| Training data generator | Run 10,000 simulations, log features | ☐ |
| `threat_classifier.py` | Train Random Forest on sim data | ☐ |
| Integrate classifier into pipeline | Live classification during simulation | ☐ |
| Confidence display in Unity | Show classifier output on dashboard | ☐ |
| BMC improvement | Use classifier output in firing decisions | ☐ |

**Milestone:** BMC uses ML classifications, not just rules. Classifier shown on Unity dashboard.

---

### Phase 6 — Polish & Testing (Week 8)

**Goal:** Stable, demo-ready system.

| Task | Details | Done |
|------|---------|------|
| Scenario designer | Config-based scenario definitions | ☐ |
| Saturation scenario test | 10+ simultaneous missiles | ☐ |
| Replay system | Deterministic replay via seeded clock | ☐ |
| Performance profiling | Ensure stable 60 FPS | ☐ |
| Error handling | Graceful disconnect/reconnect | ☐ |
| Documentation | Code comments + README | ☐ |
| Demo video recording | Record final showcase scenario | ☐ |

**Milestone:** Full demo scenario. Stable. Recordable. Presentable.

---

### Phase 7 — Advanced AI (Post-MVP, Optional)

| Task | Details |
|------|---------|
| RL-based BMC | Train reinforcement learning agent in simulation |
| Attacker AI | Intelligent attacker that adapts to defense patterns |
| Saturation strategy | Attacker learns to overwhelm specific layers |
| Decoy detection | Classifier distinguishes real vs decoy objects |
| Multi-city defense | Expand to defend multiple targets simultaneously |
| Research paper | Write up architecture, results, AI performance metrics |

---

## 11. File Structure

```
SHIELD-AI/
│
├── python/
│   ├── core/
│   │   ├── sim_clock.py
│   │   ├── event_bus.py
│   │   └── config_loader.py
│   │
│   ├── threats/
│   │   ├── base_missile.py
│   │   ├── ballistic_missile.py
│   │   ├── cruise_missile.py
│   │   └── hypersonic_missile.py
│   │
│   ├── defense/
│   │   ├── base_layer.py
│   │   ├── base_radar.py
│   │   ├── base_bmc.py
│   │   ├── arrow_system.py
│   │   ├── davids_sling.py
│   │   └── iron_dome.py
│   │
│   ├── ai/
│   │   ├── kalman_tracker.py
│   │   ├── data_association.py
│   │   ├── threat_classifier.py
│   │   ├── bmc_rules.py
│   │   └── bmc_rl.py
│   │
│   ├── physics/
│   │   ├── prop_nav.py
│   │   ├── pk_engine.py
│   │   └── trajectory.py
│   │
│   ├── comms/
│   │   └── socket_server.py
│   │
│   ├── data/
│   │   └── training_data.csv   (auto-generated)
│   │
│   ├── simulation.py
│   └── config.json
│
├── unity/
│   └── SHIELD-AI-Unity/
│       ├── Assets/
│       │   ├── Scripts/
│       │   │   ├── Network/
│       │   │   ├── Entities/
│       │   │   ├── Visualization/
│       │   │   └── UI/
│       │   ├── Prefabs/
│       │   ├── Scenes/
│       │   └── Materials/
│       └── ProjectSettings/
│
├── notebooks/
│   ├── trajectory_debug.ipynb
│   ├── kalman_test.ipynb
│   └── classifier_training.ipynb
│
├── docs/
│   └── SHIELD_AI_ROADMAP.md    (this file)
│
└── README.md
```

---

## 12. Configuration Reference

```json
{
  "simulation": {
    "timestep": 0.016,
    "time_scale": 1.0,
    "random_seed": 42,
    "city_position": {"x": 0, "y": 0, "z": 0}
  },

  "network": {
    "host": "127.0.0.1",
    "port": 5000,
    "update_rate_hz": 60
  },

  "missiles": {
    "ballistic": {
      "speed_kmh": 14000,
      "launch_altitude": 150000,
      "pk_penalty": 0.0,
      "jitter": 0.0
    },
    "cruise": {
      "speed_kmh": 900,
      "flight_altitude": 100,
      "pk_penalty": 0.0,
      "jitter": 0.0,
      "waypoint_count": 4
    },
    "hypersonic": {
      "speed_kmh": 20000,
      "glide_threshold_altitude": 40000,
      "pk_penalty": 0.30,
      "jitter": 0.05
    }
  },

  "defense_layers": {
    "arrow": {
      "layer_id": 3,
      "range_km": 2400,
      "pk_base": 0.80,
      "intercept_altitude_min": 50000,
      "interceptor_count": 20,
      "handles": ["ballistic", "hypersonic"]
    },
    "davids_sling": {
      "layer_id": 2,
      "range_km": 300,
      "pk_base": 0.75,
      "intercept_altitude_min": 1000,
      "interceptor_count": 30,
      "handles": ["ballistic", "cruise", "hypersonic"]
    },
    "iron_dome": {
      "layer_id": 1,
      "range_km": 70,
      "pk_base": 0.90,
      "intercept_altitude_min": 0,
      "interceptor_count": 50,
      "handles": ["cruise"]
    }
  },

  "bmc": {
    "strategy": "rules",
    "saturation_threshold": 3,
    "saturation_pk_penalty": 0.15,
    "hypersonic_double_fire": true
  }
}
```

---

*SHIELD-AI Project — Research Simulation System*  
*Built for academic and educational purposes only*
