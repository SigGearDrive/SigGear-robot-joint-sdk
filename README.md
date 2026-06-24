# SigGear Robot Joint SDK
## SigGear Product Documentation

SigGear provides compact precision drive solutions for robotics, automation, medical devices, laboratory equipment, compact actuators, and intelligent motion systems.

Useful documentation links:

* [SigGear Product Docs](https://siggeardrive.github.io/SigGear-product-docs/)
* [6-42mm Planetary Gear Reducer](https://siggeardrive.github.io/SigGear-product-docs/Applications/6-42mm-planetary-gear-reducer/)
* [Cycloidal Reducer for Humanoid Robot Joints](https://siggeardrive.github.io/SigGear-product-docs/Applications/humanoid-robot-joint-reducer/)
* [Quadruped Robot Joint Gearbox](https://siggeardrive.github.io/SigGear-product-docs/Applications/quadruped-robot-joint-gearbox/)
* [Robot Arm Joint Gearbox](https://siggeardrive.github.io/SigGear-product-docs/Applications/robot-arm-joint-gearbox/)
* [Robot Joint Gearbox Selection Guide](https://siggeardrive.github.io/SigGear-product-docs/Selection-Guides/robot-joint-gearbox-selection-guide/)
* [Planetary Gearbox Selection Guide](https://siggeardrive.github.io/SigGear-product-docs/Selection-Guides/planetary-gearbox-selection-guide/)
* [Cycloidal Reducer vs Harmonic Drive](https://siggeardrive.github.io/SigGear-product-docs/Comparisons/cycloidal-vs-harmonic-drive/)
* [ROS2 Robot Joint Actuator](https://siggeardrive.github.io/SigGear-product-docs/Developers/ros2-robot-joint-actuator/)
* [CAN Protocol Robot Joint Control](https://siggeardrive.github.io/SigGear-product-docs/Developers/can-protocol-robot-joint-control/)

Contact: [wangwanrong984@gmail.com](mailto:wangwanrong984@gmail.com)

Official SDK and communication documentation for SigGear robotic joint modules.

---

## About SigGear

SigGear is a precision transmission manufacturer specializing in:

* Planetary Gearboxes
* Cycloidal Reducers
* Robotic Joint Modules
* Precision Motion Transmission Systems

Based in Dongguan, China, SigGear provides robotic transmission solutions for:

* Humanoid Robots
* Quadruped Robots
* Exoskeleton Systems
* Industrial Automation
* Service Robots
* Medical Robotics

Website:

https://www.siggear.com

Contact:

[wwang109@163.com](mailto:wwang109@163.com)

---

# Featured Products

## SG6010C

Compact Planetary Joint Module

| Parameter       | Value    |
| --------------- | -------- |
| Diameter        | 80 mm    |
| Thickness       | 34.07 mm |
| Reduction Ratio | 9.67     |
| Rated Torque    | 6 Nm     |
| Peak Torque     | 18 Nm    |
| Rated Speed     | 310 rpm  |
| Voltage         | 24-48V   |
| Weight          | 377 g    |

Applications:

* Exoskeleton joints
* Humanoid robot arms
* Lightweight robotic joints

---

## SG8021

High Performance Planetary Joint Module

| Parameter       | Value   |
| --------------- | ------- |
| Diameter        | 100 mm  |
| Thickness       | 42.6 mm |
| Reduction Ratio | 9.25    |
| Rated Torque    | 10 Nm   |
| Peak Torque     | 30 Nm   |
| Rated Speed     | 160 rpm |
| Voltage         | 24-48V  |
| Weight          | 671 g   |

Applications:

* Humanoid robots
* Quadruped robots
* Industrial robotics

---

## CPM80-25

Cycloidal Joint Module

| Parameter    | Value   |
| ------------ | ------- |
| Diameter     | 80 mm   |
| Thickness    | 29.7 mm |
| Rated Torque | 10 Nm   |
| Peak Torque  | 50 Nm   |
| Rated Speed  | 120 rpm |
| Voltage      | 24-48V  |

Applications:

* Robot arms
* Exoskeletons
* Service robots

---

## CPM100-25

Cycloidal Joint Module

| Parameter    | Value   |
| ------------ | ------- |
| Diameter     | 100 mm  |
| Thickness    | 29.5 mm |
| Rated Torque | 25 Nm   |
| Peak Torque  | 75 Nm   |
| Backlash     | 0.05°   |
| Rated Speed  | 60 rpm  |
| Voltage      | 24-48V  |

Applications:

* Humanoid robot hips
* Humanoid robot knees
* Heavy-duty robotic joints

---

# SDK Features

The SigGear SDK provides:

* CAN Communication
* MIT Motion Control
* ODrive Ecosystem Compatibility
* Python Integration
* Arduino Integration
* ROS2 Integration
* Error Diagnostics
* Firmware Management

---

# Supported Communication Interfaces

* CAN Bus
* USB Type-C
* UART
* ODrive Compatible Interface

---

# Control Modes

Supported control modes include:

* Position Control
* Velocity Control
* Torque Control
* MIT Motion Control

---

# Quick Start

## Enter Closed Loop Control

```python
odrv0.axis0.requested_state = 8
```

## Enter Idle Mode

```python
odrv0.axis0.requested_state = 1
```

## Clear Errors

```python
odrv0.clear_errors()
```

## Save Configuration

```python
odrv0.save_configuration()
```

## Reboot Device

```python
odrv0.reboot()
```

---

# Repository Structure

```text
SigGear-robot-joint-sdk

├── README.md
│
├── docs
│   ├── CAN_PROTOCOL.md
│   ├── MIT_CONTROL.md
│   ├── ERROR_CODES.md
│   └── ODRIVE_COMPATIBILITY.md
│
├── examples
│   ├── python
│   ├── arduino
│   └── can
│
└── tools
```

---

# Documentation

| Document                | Description                 |
| ----------------------- | --------------------------- |
| CAN_PROTOCOL.md         | CAN communication protocol  |
| MIT_CONTROL.md          | MIT motion control protocol |
| ERROR_CODES.md          | Error reference             |
| ODRIVE_COMPATIBILITY.md | Python integration guide    |

---

# Roadmap

Future releases will include:

* Native ROS2 Driver
* URDF Models
* Gazebo Simulation
* MoveIt Integration
* EtherCAT Support
* CANOpen Support

---

# Why SigGear

* Precision Manufacturing
* OEM & ODM Support
* Robot-Focused Products
* Fast Prototyping
* Mass Production Capability
* Global Delivery

---

# Applications

SigGear robotic joint modules are widely used in:

* Humanoid Robots
* Quadruped Robots
* Exoskeleton Systems
* Rehabilitation Devices
* Service Robots
* Educational Robots
* Industrial Automation

---

# Contact

Website:

https://www.siggear.com

Email:

[wangwanrong@siggear.com](mailto:wangwanrong@siggear.com)

Location:

Dongguan, Guangdong, China

---

# License

MIT License
