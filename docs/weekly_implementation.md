# FC-YAW Prototype — Weekly Implementation Plan

## Project Objective

Develop a **single-axis reaction wheel stabilization prototype** demonstrating core **Guidance, Navigation, and Control (GNC)** principles used in spacecraft **Attitude Determination and Control Systems (ADCS)**.

The project emphasizes:

* real-time embedded control
* inertial sensing
* actuator command
* disturbance rejection
* telemetry and analysis
* model-based validation

The focus is **rapid prototyping combined with aerospace-style engineering documentation**.

---

# Week 0 — System Definition and Architecture

### Objective

Define the system architecture, select components, and establish project structure.

This phase has already been completed.

### Tasks Completed

#### System Concept

Define a **single-axis reaction wheel control system** capable of stabilizing angular rate using gyroscope feedback.

Control architecture defined as:

```text
gyro → state estimation → rate controller → motor driver → reaction wheel
```

#### Component Selection

| Component           | Role                      |
| ------------------- | ------------------------- |
| NUCLEO-F446RE       | microcontroller platform  |
| MPU6050             | inertial measurement unit |
| BTS7960             | motor driver              |
| DC motor + flywheel | reaction wheel actuator   |
| 12 V power supply   | motor power               |

#### Repository Initialization

Repository structure established with directories for:

* firmware
* documentation
* simulation
* experiments

#### Documentation Created

* system architecture document
* bill of materials
* repository README
* initial weekly plan

### Deliverable

* finalized system architecture
* selected hardware platform
* documented project structure

---

# Week 1 — Hardware Integration

### Objective

Construct the physical test platform and verify electrical connections.

### Mechanical Tasks

* mount DC motor
* attach flywheel disk
* align shaft and coupler
* secure rig base
* verify minimal wobble

### Electrical Integration

| Component            | Connection          |
| -------------------- | ------------------- |
| MPU6050              | I2C → NUCLEO-F446RE |
| BTS7960 motor driver | PWM + DIR GPIO      |
| DC motor             | driver output       |
| Motor supply         | 12 V adapter        |
| Telemetry            | UART over USB       |

### Power Rails

| Rail  | Source                   |
| ----- | ------------------------ |
| 12 V  | motor power supply       |
| 5 V   | USB                      |
| 3.3 V | Nucleo onboard regulator |

### Deliverable

* mechanical rig assembled
* wiring verified
* motor spins safely
* sensor detected over I2C

---

# Week 2 — Sensor Bring-Up

### Objective

Obtain reliable angular-rate measurements from the IMU.

### Tasks

1. initialize I2C bus
2. configure MPU6050 registers
3. read gyroscope measurements
4. convert raw values to rad/s
5. measure sensor noise characteristics
6. implement basic low-pass filtering

### State Estimate

```text
ω_est = LPF(gyro_measurement)
```

### Telemetry Stream

```
time
raw_gyro
filtered_rate
```

### Deliverable

stable angular-rate measurement and telemetry output.

---

# Week 3 — Motor Control

### Objective

Establish reliable actuator control through the motor driver.

### Tasks

1. configure PWM timer
2. implement motor command interface

```
motor_cmd ∈ [-1,1]
```

3. convert command to PWM duty cycle
4. verify direction control
5. test acceleration and deceleration

### Tests

| Test             | Expected Behavior   |
| ---------------- | ------------------- |
| positive command | motor spins forward |
| negative command | motor spins reverse |
| zero command     | motor stops         |

### Deliverable

manual motor torque control verified.

---

# Week 4 — Closed-Loop Control

### Objective

Implement rate stabilization using feedback control.

### Control Law

```
u = -Kp * ω_est
```

Where:

* `ω_est` = estimated angular rate
* `u` = motor command

### Control Loop Timing

Loop executed at **50 Hz timer interrupt**.

Loop sequence:

```
read sensor
update estimate
compute control
apply motor command
```

### Tuning

Tune proportional gain **Kp** experimentally.

### Disturbance Test

* rotate rig manually
* release platform
* observe stabilization behavior

### Deliverable

closed-loop rate damping demonstrated.

---

# Week 5 — System Identification and Estimation

### Objective

Estimate system dynamics and refine state estimation.

### Plant Model

```
I * dω/dt = τ
```

Where:

* `I` = platform inertia
* `τ` = reaction wheel torque

### Experiments

1. open-loop torque step
2. measure resulting angular acceleration
3. estimate actuator gain

### Estimation Improvements

* gyro bias estimation
* corrected rate measurement

```
ω_corr = gyro − bias
ω_est = LPF(ω_corr)
```

### Deliverable

estimated plant parameters and improved state estimate.

---

# Week 6 — Validation and Demonstration

### Objective

Validate system behavior and document experimental results.

### Experiments

| Test                  | Purpose                         |
| --------------------- | ------------------------------- |
| stationary noise      | characterize sensor behavior    |
| open-loop step        | measure plant response          |
| disturbance rejection | evaluate controller performance |
| saturation test       | observe actuator limits         |

### Telemetry Variables

```
time
gyro_rate
rate_estimate
motor_command
```

### Deliverables

* experimental plots
* comparison with simple simulation model
* demonstration video of stabilization
* finalized documentation

---

# Expected Outcome

A functioning **single-axis reaction wheel stabilization prototype** with documented control architecture, experimental validation, and a clear engineering workflow consistent with spacecraft **GNC system development practices**.
