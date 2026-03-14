# Autonomous Obstacle-Avoidance Robot

**Bachelor's Final Year Project**
BCA — St. Aloysius College (Autonomous), Mangaluru
Nathan Ivor Sequeira · Jan – May 2024

---

## What This Is

An autonomous robot built on an Arduino Uno that detects obstacles in real time and reroutes without human input. No remote control, no pre-loaded maps — just sensor readings and a decision algorithm running on the microcontroller itself.

The project started as a line-following robot. About three weeks in, we scrapped that approach: the IR sensors were too unreliable on the test surface (dead zones, ambient light interference, inconsistent readings). We redesigned around ultrasonic sensing instead. More work, but a more tractable problem with the hardware we actually had.

---

## Hardware

| Component | Role |
|---|---|
| Arduino Uno R3 SMD | Main microcontroller |
| HC-SR04 Ultrasonic Sensor | Obstacle detection |
| Servo Motor | Sensor sweep (left/right scan) |
| L298N Motor Driver | Motor control |
| DC Motors (x2) | Locomotion |
| Battery Holder + Rocker Switch | Power supply and on/off control |

---

## How It Works

1. The servo sweeps the HC-SR04 sensor in an arc ahead of the robot, taking continuous distance readings.
2. When the measured distance drops below a set threshold, the directional decision algorithm runs.
3. It compares left and right clearance values and routes the robot toward the less obstructed side.
4. If both sides are blocked, the robot reverses briefly before re-scanning.

The full loop — sense, decide, move — runs entirely on the Arduino in Embedded C.

---

## Software

- **Language:** Embedded C (Arduino framework)
- **Core logic:** Threshold-based obstacle detection + clearance comparison algorithm
- **Motor control:** PWM signals via L298N driver routines
- **Sensor sweep:** Servo angle control with `Servo.h` library

---

## What We Learned

Hardware debugging is different from software debugging. Sensor noise, motor timing inconsistencies, and voltage drops under load only show up when the robot is actually moving — not in code review. Most of our debugging time went into the physical system, not the algorithm.

The pivot from line-following to obstacle avoidance also clarified something: switching data models (binary IR signal → continuous ultrasonic distance) required rethinking the decision logic from scratch. That redesign was where most of the actual engineering happened.

---

## Project Structure

```
UnderGrad_Arduino_code/
├── finalobstacle.ino     # Final working code — autonomous obstacle avoidance
├── [other .ino files]    # Test sketches used during development and hardware testing
└── README.md
```

The other `.ino` files in the repo are test sketches written during development — motor calibration, sensor range checks, servo sweep tests, and similar. `finalobstacle.ino` is the complete, final version of the robot's code.

---

## Project Team

Nathan Ivor Sequeira, Ohsneen D'Costa, Hirkur Biru
*Code and repository maintained by Nathan Ivor Sequeira*

---

## Academic Context

Submitted as the official Final Year Project for the Bachelor of Computer Applications degree at St. Aloysius College (Autonomous), Mangaluru, India.
