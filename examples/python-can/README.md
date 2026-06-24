# Python CAN Examples

This folder is reserved for Python-based CAN communication examples for SigGear robot joint actuator testing and integration.

These examples are intended to help engineers understand basic actuator communication flow, command testing, feedback monitoring, and development workflow.

## Planned Example Topics

This folder may include examples for:

* CAN interface initialization
* Actuator enable and disable command
* Position command example
* Velocity command example
* Torque command example
* Joint feedback reading
* Fault status monitoring
* Basic actuator test loop
* Multi-actuator CAN network reference

## Typical Development Environment

A typical Python CAN test environment may include:

* Python 3
* CAN interface adapter
* CAN driver
* SigGear robot joint actuator
* Power supply
* Emergency stop method
* Mechanical test fixture

## Safety Notice

Before running any actuator test script:

* Confirm wiring and CAN bus connection.
* Confirm actuator ID and CAN baud rate.
* Secure the actuator before motion testing.
* Start with low speed and low torque limits.
* Keep clear of moving parts.
* Prepare an emergency stop method.

## Related Documentation

* [CAN Protocol Robot Joint Control](https://siggeardrive.github.io/SigGear-product-docs/Developers/can-protocol-robot-joint-control/)
* [ROS2 Robot Joint Actuator](https://siggeardrive.github.io/SigGear-product-docs/Developers/ros2-robot-joint-actuator/)

## Contact

For confirmed SDK examples, CAN protocol details, actuator samples, or custom integration support, contact SigGear:

**Email:** [wangwanrong984@gmail.com](mailto:wangwanrong984@gmail.com)
