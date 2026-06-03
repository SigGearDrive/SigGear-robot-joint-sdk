# SigGear Robot Joint SDK

Official SDK and communication documentation for SigGear robotic joint modules.

This repository provides integration resources for SigGear robotic joint modules, including:

- SG6010C planetary robotic joint module
- SG8021 planetary robotic joint module
- CPM80-25 cycloidal robotic joint module
- CPM100-25 cycloidal robotic joint module

The SDK supports CAN communication, ODrive-compatible commands, MIT-style motion control, Python integration, Arduino integration and ROS2 integration.

## Supported Communication Interfaces

- CAN Bus
- USB Type-C
- ODrive-compatible interface
- MIT-style motion control over CAN
- Python SDK
- Arduino SDK
- ROS2 SDK

## Default CAN Parameters

| Parameter | Value |
|---|---|
| CAN frame type | Standard frame |
| CAN ID | 11-bit |
| CAN data length | 8 bytes |
| Default baud rate | 500 kbps |
| Maximum CAN baud rate | 1 Mbps |
| Default node ID | 0 |
| Node ID range | 0–63 |

## CAN ID Format

The 11-bit CAN ID is composed of:

```text
CAN_ID = (node_id << 5) + cmd_id
