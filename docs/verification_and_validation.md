# Verification and Validation

## Purpose

This document defines the experimental procedures used to evaluate the performance of the FC-YAW reaction wheel control system.

Verification ensures that the system behaves as intended.

Validation compares the observed system behavior with the expected response derived from a simple dynamic model.

---

# System Model

The rotational dynamics of the platform can be approximated as

```
I · dω/dt = τ
```

where

| Variable | Description                  |
| -------- | ---------------------------- |
| I        | effective rotational inertia |
| ω        | angular rate                 |
| τ        | reaction wheel torque        |

The controller attempts to regulate the angular rate toward zero.

---

# Test Environment

The prototype consists of:

| Component       | Role                |
| --------------- | ------------------- |
| reaction wheel  | actuator            |
| gyroscope       | rate measurement    |
| microcontroller | control computation |
| motor driver    | actuator interface  |

Telemetry is streamed to a host computer for analysis.

---

# Experiment 1 — Sensor Noise Characterization

### Objective

Measure baseline gyroscope noise.

### Procedure

1. keep platform stationary
2. record angular rate measurements
3. log raw and filtered data

### Metrics

* mean bias
* standard deviation
* filter effectiveness

---

# Experiment 2 — Open-Loop Actuator Response

### Objective

Observe system response to a fixed motor command.

### Procedure

1. apply constant motor command
2. measure resulting angular acceleration
3. log angular rate over time

### Outcome

Used to estimate effective plant gain.

---

# Experiment 3 — Disturbance Rejection

### Objective

Evaluate closed-loop stabilization performance.

### Procedure

1. disturb platform manually
2. release platform
3. measure recovery response

### Metrics

| Metric           | Description              |
| ---------------- | ------------------------ |
| peak rate        | maximum angular rate     |
| settling time    | time to stabilize        |
| damping behavior | oscillation or stability |

---

# Experiment 4 — Actuator Saturation

### Objective

Observe system behavior near actuator limits.

### Procedure

1. apply strong disturbance
2. allow controller to respond
3. monitor motor command limits

### Metrics

* control saturation
* recovery performance

---

# Telemetry Variables

The following signals are recorded during experiments:

```
time
gyro_rate
rate_estimate
motor_command
```

These data are stored in the experiments directory for analysis.

---

# Simulation Comparison

A simple simulation model of the system is implemented in the `simulation` directory.

The simulation uses the same control law as the hardware system.

Simulation results are compared with experimental data to evaluate:

* controller performance
* model accuracy
* disturbance response

---

# Expected Outcome

Successful validation demonstrates:

* stable closed-loop behavior
* measurable disturbance rejection
* predictable system response

These results confirm that the prototype implements the intended control architecture.
