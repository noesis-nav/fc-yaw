# System Architecture

## Control Architecture

The prototype implements a simplified spacecraft ADCS control loop.

```
disturbance torque
        ↓
platform dynamics
        ↓
angular rate ω
        ↓
gyroscope sensor
        ↓
state estimation
        ↓
rate controller
        ↓
motor driver
        ↓
reaction wheel torque
```

---

# Hardware Interfaces

| Interface | Signal                | Voltage |
| --------- | --------------------- | ------- |
| I2C       | MPU6050 communication | 3.3 V   |
| PWM       | motor command         | 3.3 V   |
| GPIO      | direction control     | 3.3 V   |
| UART      | telemetry             | 3.3 V   |

---

# Control Loop Timing

The control loop executes at **50 Hz** using a microcontroller timer interrupt.

Loop sequence:

```
read sensor
update state estimate
compute control command
output PWM command
log telemetry
```

---

# State Variables

| Variable | Description           |
| -------- | --------------------- |
| ω_meas   | raw gyro measurement  |
| ω_est    | filtered angular rate |
| u        | control command       |

---

# Safety Features

* actuator saturation limits
* manual kill switch
* software safe mode
