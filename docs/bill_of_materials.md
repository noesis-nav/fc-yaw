# FC-YAW Hardware Bill of Materials (BOM)

This document lists the hardware components used in the **FC-YAW single-axis reaction wheel control system** prototype.

Version: Week-2 hardware configuration
Project: FC-YAW
Repository: https://github.com/noesis-nav/fc-yaw

---

# 1. Core Electronics

| Item         | Component            | Specification    | Quantity | Notes                       |
| ------------ | -------------------- | ---------------- | -------- | --------------------------- |
| MCU          | STM32 NUCLEO-F446RE  | ARM Cortex-M4    | 1        | Main control board          |
| Sensor       | MPU6050 (GY-521)     | 6-axis IMU       | 2        | One spare                   |
| Motor Driver | BTS7960 H-Bridge     | 43A module       | 1        | Drives reaction wheel motor |
| Motor        | 550 Brushed DC Motor | 6-24V, ~8000 RPM | 1        | Reaction wheel actuator     |

---

# 2. Power System

| Item           | Component     | Specification | Quantity | Notes                |
| -------------- | ------------- | ------------- | -------- | -------------------- |
| Power Supply   | DC Adapter    | 12V 2A        | 1        | Motor supply         |
| Logic Supply   | USB           | 5V            | 1        | Powers Nucleo        |
| Buck Converter | MP1584 Module | 3A adjustable | 1        | Optional future rail |

---

# 3. Passive Components

| Component  | Value    | Type             | Quantity | Notes             |
| ---------- | -------- | ---------------- | -------- | ----------------- |
| Capacitors | 100nF    | Ceramic (THT)    | 10+      | Decoupling        |
| Capacitors | 470µF    | Electrolytic 25V | 2        | Power filtering   |
| Capacitors | 1000µF   | Electrolytic 25V | 2        | Bulk motor supply |
| Diodes     | Schottky | SS34 class       | 2        | Protection        |
| Resistors  | Assorted | 220Ω / 1k / 10k  | Assorted | LEDs / pullups    |

---

# 4. Mechanical Components

| Item          | Specification             | Quantity | Notes               |
| ------------- | ------------------------- | -------- | ------------------- |
| Shaft Coupler | 3mm → 8mm flexible        | 1        | Motor to flywheel   |
| Flywheel      | Steel washer stack / disc | 1        | Reaction wheel mass |
| Motor Mount   | 550 motor bracket         | 1        | Rigid mounting      |
| Fasteners     | M8 bolt + washers + nuts  | Assorted | Flywheel stack      |

---

# 5. Wiring and Prototyping

| Item            | Specification   | Quantity | Notes                  |
| --------------- | --------------- | -------- | ---------------------- |
| Breadboard      | 830-point       | 1        | Prototype wiring       |
| Jumper wires    | M-M / M-F       | Assorted | Breadboard connections |
| Power wire      | 20 AWG silicone | 40 m     | Motor supply           |
| Terminal blocks | Screw type      | Assorted | Power connections      |

---

# 6. Tools and Test Equipment

| Item          | Specification          | Quantity | Notes                  |
| ------------- | ---------------------- | -------- | ---------------------- |
| Multimeter    | Digital                | 1        | Electrical diagnostics |
| Soldering Kit | Temperature controlled | 1        | Assembly               |

---

# 7. Future Hardware (Not Yet Installed)

These components may be added in later phases.

| Component      | Purpose                      |
| -------------- | ---------------------------- |
| Encoder        | Wheel speed measurement      |
| Current sensor | Motor current monitoring     |
| Dedicated PCB  | Replace breadboard prototype |

---

# 8. Notes

* Motor and logic power domains are separated.
* Bulk capacitors must be placed near the **BTS7960 VM input**.
* Reaction wheel inertia can be adjusted by adding/removing washers.

---

# Revision History

| Version | Date    | Description         |
| ------- | ------- | ------------------- |
| v1      | Initial | Week-2 hardware BOM |
