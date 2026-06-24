# Contributing to SigGear Robot Joint SDK

Thank you for your interest in SigGear robot joint actuator integration resources.

This repository provides reference materials, examples, and documentation for SigGear compact robot joint actuators, CAN-based actuator control, robotic drive systems, and motion control integration.

## Contribution Scope

Contributions may include:

* Example code for CAN-based robot joint actuator control
* Robot joint command and feedback examples
* Documentation improvements
* Integration notes for humanoid robots, quadruped robots, robot arms, and robotic grippers
* Testing scripts and development utilities
* ROS2 or embedded control references
* Issue reports related to documentation clarity or example usage

## Before Contributing

Before submitting a contribution, please make sure that:

* The contribution is relevant to SigGear robot joint actuator integration.
* Example code is clearly documented.
* Product-specific parameters are not presented as universal values.
* Safety-related behavior is described carefully.
* Any test data, CAN IDs, message formats, or control parameters are clearly marked as examples unless confirmed by SigGear.

## Safety Notice

Robot joint actuators and motor control systems can generate high torque, high speed, and unexpected motion.

Before testing any actuator example:

* Secure the actuator mechanically.
* Use a current-limited power supply where possible.
* Confirm the correct voltage, wiring, CAN baud rate, and device ID.
* Keep hands and tools away from moving parts.
* Prepare an emergency stop method.
* Test with low speed and low torque limits first.

## Documentation Style

Please use clear technical English.

When adding examples, include:

* Required hardware
* Required software
* Connection assumptions
* Command format
* Feedback format
* Safety notes
* Expected behavior
* Known limitations

## Contact

For product-specific protocol details, actuator samples, datasheets, CAD files, or custom robotic joint drive support, contact SigGear:

**Email:** [wangwanrong984@gmail.com](mailto:wangwanrong984@gmail.com)
