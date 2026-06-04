# MIT Motion Control

## Overview

SigGear robotic joint modules support MIT-style motion control over CAN Bus.

MIT control combines:

* Position Control
* Velocity Control
* Torque Feedforward

This control mode is widely used in:

* Humanoid Robots
* Quadruped Robots
* Exoskeleton Systems
* Dynamic Robotic Arms

---

# Control Equation

```text
Torque Target

= Kp × Position Error
+ Kd × Velocity Error
+ Torque Feedforward
```

---

# Parameters

| Parameter | Description        |
| --------- | ------------------ |
| Position  | Target Position    |
| Velocity  | Target Velocity    |
| Kp        | Position Gain      |
| Kd        | Velocity Gain      |
| Torque FF | Feedforward Torque |

---

# MIT CAN Command

Command ID:

```text
0x008
```

Direction:

```text
Host → Joint Module
```

---

# Data Frame

| Parameter | Bits |
| --------- | ---- |
| Position  | 16   |
| Velocity  | 12   |
| Kp        | 12   |
| Kd        | 12   |
| Torque    | 12   |

---

# Typical Usage

MIT control is recommended for:

* Humanoid Knees
* Humanoid Hips
* Robot Shoulders
* Quadruped Legs

---

# Advantages

* Smooth Motion
* High Responsiveness
* Low Latency
* Dynamic Force Control

---

# Supported Products

* SG6010C
* SG8021
* CPM80-25
* CPM100-25
