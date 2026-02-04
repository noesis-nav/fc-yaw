# Space-oriented Flight Controller — Single-axis (Yaw)

## Overview
Design and build a space-oriented flight controller for single-axis (yaw) attitude determination and control,
demonstrated using a reaction wheel. Runs a deterministic closed-loop control loop on a custom PCB.

## Scope

### Objectives

O1. Hardware flight controller: design and fabricate PCB integrating MCU, inertial sensing, power regulation, and interfaces.

O2. Deterministic control: fixed-rate loop (50 Hz initial; 100 Hz later) with timing jitter logged.

O3. Yaw control demo: stabilize/command yaw using reaction wheel actuation (PWM + direction).

O4. Flight-style robustness: mode logic (init/nominal/safe) with watchdog and actuator inhibit.

O5. Portfolio evidence: diagrams, bring-up tests, plots, and repeatable test plan.

### Explicit Exclusions

E1. Multi-axis (3-axis) control

E2. Physical RCS (thrusters/pressurized hardware)

E3. Star tracker / camera-based attitude

E4. GPS orbit navigation

E5. Space-grade / radiation-hardened components


### Operating Assumptions

A1. Laboratory environment; architectural demonstration only (not flight qualification)

A2. Reaction wheel is a DC motor + flywheel

A3. One-axis mechanical rig approximates free yaw rotation

A4. Advanced actuators may exist as software stubs later

## Architecture Placeholder

Sensing → Estimation → Control → Actuator command → Mode logic → Fault handling


