# FC-YAW — Reaction Wheel Control Prototype

## Overview

FC-YAW is a **single-axis reaction wheel control prototype** developed to demonstrate fundamental spacecraft **Attitude Determination and Control System (ADCS)** concepts.

The project focuses on building a **working embedded control system** that stabilizes angular motion using inertial sensing and a reaction wheel actuator.

The system serves as a **portfolio demonstration for GNC roles in astronautics and spacecraft engineering.**

---

# Project Goals

The prototype demonstrates:

* embedded control implementation
* inertial sensor integration
* actuator command through motor driver
* disturbance rejection
* telemetry and analysis
* model-based validation

---

# System Concept

A rigid platform with a reaction wheel is controlled using gyroscope measurements.

Control loop:

```
gyro measurement
→ state estimation
→ rate controller
→ motor command
→ reaction wheel torque
→ platform dynamics
```

---

# Hardware Platform

| Component           | Role            |
| ------------------- | --------------- |
| NUCLEO-F446RE       | microcontroller |
| MPU6050             | inertial sensor |
| BTS7960             | motor driver    |
| DC motor + flywheel | reaction wheel  |
| 12V supply          | motor power     |

---

# Control Architecture

The controller stabilizes **angular rate** using proportional feedback.

```
u = -Kp * ω
```

where

* `ω` = measured angular rate
* `u` = motor command

---

# System Dynamics

The rotational dynamics of the platform are approximated by

```
I * dω/dt = τ
```

where

* `I` = system inertia
* `τ` = reaction wheel torque

---

# Key Demonstrations

The system demonstrates:

* real-time control loop
* disturbance rejection
* actuator saturation
* telemetry logging
* simulation vs hardware validation

---

# Future Upgrades

Potential extensions include

* complementary or Kalman filtering
* cascaded attitude + rate control
* multi-axis reaction wheel platform
* momentum management
* dedicated flight-controller PCB

---

# Project Motivation

The project is designed to reflect the workflow used in spacecraft **Guidance, Navigation, and Control engineering**:

1. model the physical system
2. estimate the system state
3. implement feedback control
4. validate behavior experimentally
