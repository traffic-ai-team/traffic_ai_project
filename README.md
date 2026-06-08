# 🚦 Intelligent Traffic Control System

An AI-powered traffic management system that combines Computer Vision and Reinforcement Learning to improve traffic flow and reduce vehicle waiting time at road intersections.

The project consists of two independent subsystems:

1. Computer Vision Pipeline for vehicle detection, tracking, and counting.
2. Reinforcement Learning Pipeline for adaptive traffic signal control inside a SUMO simulation environment.

---

## 📖 Overview

Traffic congestion is one of the most common urban transportation challenges. Traditional traffic lights operate using fixed timing schedules and cannot adapt to changing traffic conditions.

This project introduces an intelligent traffic control system capable of:

- Detecting and tracking vehicles from real traffic videos.
- Counting vehicles moving in different directions.
- Simulating realistic traffic environments.
- Optimizing traffic signal timings using Deep Q-Networks (DQN).
- Reducing queue lengths and waiting times.

---

## 🎯 Project Objectives

- Improve traffic flow efficiency.
- Reduce vehicle waiting times.
- Minimize traffic congestion.
- Apply Artificial Intelligence to traffic management.
- Compare intelligent control against traditional fixed-time systems.

---

# 🏗️ System Architecture

The project follows a fully decoupled architecture where both subsystems operate independently.

## 1️⃣ Computer Vision Pipeline

```text
Traffic Video
      │
      ▼
YOLOv8 Detection
      │
      ▼
ByteTrack Tracking
      │
      ▼
Virtual Line Counting
      │
      ▼
Traffic Statistics
```

### Features

- Vehicle detection using YOLOv8.
- Vehicle tracking using ByteTrack.
- Direction estimation.
- Virtual line crossing count.
- Vehicle classification:
  - Car
  - Van
  - Truck
  - Bus
  - Tram

---

## 2️⃣ Reinforcement Learning Pipeline

```text
SUMO Environment
        │
        ▼
Virtual Sensors
        │
        ▼
State Extraction
        │
        ▼
DQN Agent
        │
        ▼
Traffic Signal Control
```

### Features

- Deep Q-Network (DQN).
- Adaptive signal timing.
- Dynamic phase switching.
- Safety threshold override.
- Realistic traffic generation.

---

# 🧠 Reinforcement Learning Design

## State Space

The intersection state is represented as an **8 × 3 matrix** containing:

- Vehicle positions.
- Vehicle velocities.
- Lane occupancy information.

## Action Space

The agent chooses from **12 possible actions**.

Each action controls:

- Traffic signal phase.
- Green light duration.

Possible durations:

- 10 seconds
- 15 seconds
- 20 seconds

## Reward Function

```text
R = (old_total_wait - current_total_wait) × 0.01
    - (current_queue × 0.01)
```

Additional rewards:

- +1.0 when queue length becomes zero.
- +0.5 when queue length is less than 3 vehicles.

---

# 🛡️ Safety Mechanism

To prevent gridlock situations:

- The system continuously monitors road occupancy.
- If occupancy exceeds 80%, the safety controller overrides the DQN decision.
- The congested direction receives immediate priority.

This ensures uninterrupted traffic flow even during abnormal traffic spikes.

---

# 🔍 Computer Vision Methodology

### Vehicle Detection

YOLOv8 is used to detect vehicles in every frame.

Confidence threshold:

```text
0.45
```

### Vehicle Tracking

ByteTrack assigns a unique ID to every detected vehicle and tracks its movement across frames.

### Vehicle Counting

Vehicles are counted when crossing a virtual line positioned at the center of the frame.

The system supports:

- Left → Right counting
- Right → Left counting

---

# 🛠️ Technologies Used

| Technology | Purpose |
|------------|----------|
| Python | Core language |
| YOLOv8 | Vehicle detection |
| ByteTrack | Multi-object tracking |
| OpenCV | Video processing |
| SUMO | Traffic simulation |
| TraCI | Communication with SUMO |
| TensorFlow 1.x | DQN implementation |
| Google Colab | Training environment |

---

# 📂 Project Structure

```text
traffic_ai_project/
│
├── models/
│
├── simulation/
│
├── videos/
│
├── outputs/
│
├── traffic_generator.py
├── training_main.py
├── testing_main.py
├── visualization.py
│
├── yolo_tracking.py
├── requirements.txt
└── README.md
```

---

# 📈 Experimental Results

### Computer Vision Pipeline

- Real-time processing at approximately 25 FPS.
- Accurate vehicle classification.
- Reliable tracking using ByteTrack.

### Reinforcement Learning Pipeline

The DQN agent demonstrated progressive learning behavior and improved traffic signal decisions over multiple test episodes.

Observed improvements:

- Reduced waiting times.
- Reduced queue lengths.
- Improved traffic flow stability.
- Prevention of gridlock situations.

---
## 🚗 Demo
(view the demo)[https://traffic-ai-team.github.io/traffic_ai_project/]

---

# 🚀 Future Improvements

- Real-time integration between YOLOv8 and DQN systems.
- Multi-intersection traffic coordination.
- Smart city deployment.
- IoT sensor integration.
- Emergency vehicle prioritization.

---

# 👥 Team Members

- Abdullah Mohamed
- Hager Mostafa
- Ibrahim Ashraf
- Abdel Fattah Ahmed
- Sylvia Sameh
- Abda Mohamed
- Sara Reda
- Amgad Ali

---

# 👨‍🏫 Supervision

### Academic Supervisor

**Prof. Alaa El-Deen Abd ElHakim**  
Professor of Electrical Engineering  
Faculty of Engineering, Assiut University

### Teaching Assistant

**Eng. Eman Tamam**

---

# 📚 References

- YOLOv8
- ByteTrack
- SUMO
- TensorFlow
- Deep Q-Network (DQN)
- Reinforcement Learning for Traffic Signal Control

---

# 📜 License

This project was developed as a Work-Based Training Project at Sphinx University, Faculty of Computers and Artificial Intelligence (2025/2026).
