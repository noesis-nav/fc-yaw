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

## Current Scope and Exclusions

The current prototype focuses on validating the core control architecture for a **single-axis reaction wheel stabilization system**.

To maintain rapid prototyping and focus on core Guidance, Navigation, and Control (GNC) functionality, several capabilities commonly present in spacecraft Attitude Determination and Control Systems (ADCS) are intentionally excluded from the current implementation.

### Current System Scope

The prototype includes:

* single-axis angular rate control
* gyroscope-based rate measurement
* proportional feedback controller
* reaction wheel actuation
* embedded real-time control loop
* telemetry logging and experiment validation

### Exclusions (Current Prototype)

The following capabilities are intentionally **out of scope for this phase**:

| Capability                           | Reason                                        |
| ------------------------------------ | --------------------------------------------- |
| three-axis attitude control          | mechanical complexity outside prototype scope |
| multi-sensor fusion                  | unnecessary for single-axis rate control      |
| reaction wheel arrays                | only one actuator required for demonstration  |
| spacecraft-grade attitude estimation | simplified estimation sufficient              |
| CAN or distributed avionics buses    | single-node embedded system                   |
| custom flight controller PCB         | prototype uses development board              |

These features may be introduced in future iterations once the single-axis control architecture has been validated experimentally.

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
