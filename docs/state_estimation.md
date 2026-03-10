# State Estimation

## Purpose

The control system requires an estimate of the platform's angular rate to compute the control command.
This document describes how the system derives a usable state estimate from raw gyroscope measurements.

The estimation layer performs three functions:

1. sensor measurement conversion
2. bias correction
3. noise filtering

The resulting state estimate is used by the controller.

---

# Measurement Source

Angular rate measurements are obtained from the **MPU6050 inertial sensor**.

Only the **gyroscope measurement** is used in the current prototype.

Measurement variable:

```
ω_meas
```

where

```
ω_meas = measured angular rate
```

---

# Measurement Model

The gyroscope measurement can be modeled as

```
ω_meas = ω_true + b + n
```

where

| Term   | Description       |
| ------ | ----------------- |
| ω_true | true angular rate |
| b      | gyro bias         |
| n      | measurement noise |

The objective of the estimation layer is to obtain a usable estimate:

```
ω_est
```

---

# Bias Handling

Gyroscope sensors typically exhibit a slowly varying bias.

A simple bias estimate is computed during stationary conditions.

```
bias = average(gyro_samples)
```

Corrected measurement:

```
ω_corr = ω_meas − bias
```

---

# Filtering

To reduce measurement noise, a first-order low-pass filter is applied.

Discrete-time filter:

```
ω_est[k] = α · ω_est[k−1] + (1 − α) · ω_corr[k]
```

where

| Parameter | Description                |
| --------- | -------------------------- |
| α         | filter coefficient         |
| ω_corr    | bias-corrected measurement |

This produces a smoother rate estimate for the controller.

---

# State Variables

| Variable | Description                    |
| -------- | ------------------------------ |
| ω_meas   | raw gyroscope measurement      |
| ω_corr   | bias corrected measurement     |
| ω_est    | filtered angular rate estimate |

---

# Use in Control Loop

The controller uses the estimated rate as input:

```
u = −Kp · ω_est
```

where

| Variable | Description       |
| -------- | ----------------- |
| u        | motor command     |
| Kp       | proportional gain |

---

# Future Improvements

Possible extensions to the estimation layer include:

* complementary filtering using accelerometer measurements
* Kalman filtering
* online bias estimation
* multi-axis attitude estimation

These upgrades would bring the estimation approach closer to spacecraft ADCS implementations.
