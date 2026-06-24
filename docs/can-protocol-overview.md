# CAN Protocol Overview for SigGear Robot Joint Actuators

This page provides a general overview of CAN-based communication concepts for SigGear robot joint actuator integration.

The information here is intended for engineering reference only. Final CAN IDs, baud rates, command formats, feedback formats, scaling factors, and safety logic may vary by actuator model, firmware version, motor configuration, and customer-specific requirements.

## Typical CAN-Based Robot Joint Architecture

A typical SigGear robot joint actuator integration may include:

* Robot controller or embedded host
* CAN interface adapter
* SigGear robot joint actuator
* Power supply
* Emergency stop circuit
* Motion control software
* Feedback monitoring and fault handling logic

## Common Control Data

Robot joint actuator communication may include commands such as:

* Enable actuator
* Disable actuator
* Set position target
* Set velocity target
* Set torque or current target
* Set control mode
* Read joint position
* Read joint velocity
* Read torque or current feedback
* Read temperature
* Read fault status

## Example Command Concepts

Typical actuator control commands may include:

* Position command
* Velocity command
* Torque command
* Zero position command
* Stop command
* Status request
* Fault clear command

## Example Feedback Concepts

Typical actuator feedback may include:

* Actual position
* Actual velocity
* Estimated torque
* Motor current
* Bus voltage
* Temperature
* Actuator state
* Fault code

## Safety Considerations

Before testing CAN actuator control:

* Confirm the correct CAN baud rate.
* Confirm actuator ID settings.
* Verify power supply voltage and current capacity.
* Start with low torque and low speed limits.
* Use mechanical fixtures during testing.
* Monitor fault feedback continuously.
* Prepare an emergency stop method.

## Related Documentation

* [CAN Protocol Robot Joint Control](https://siggeardrive.github.io/SigGear-product-docs/Developers/can-protocol-robot-joint-control/)
* [ROS2 Robot Joint Actuator](https://siggeardrive.github.io/SigGear-product-docs/Developers/ros2-robot-joint-actuator/)
* [Robot Joint Gearbox Selection Guide](https://siggeardrive.github.io/SigGear-product-docs/Selection-Guides/robot-joint-gearbox-selection-guide/)

## Contact

For confirmed protocol documents, CAN frame definitions, actuator samples, or custom integration support, contact SigGear:

**Email:** [wangwanrong984@gmail.com](mailto:wangwanrong984@gmail.com)
