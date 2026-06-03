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
| Field   | Bits           |
| ------- | -------------- |
| node_id | Bit 10 ~ Bit 5 |
| cmd_id  | Bit 4 ~ Bit 0  |
node_id = 0x05
cmd_id  = 0x0C

CAN_ID = (0x05 << 5) + 0x0C = 0xAC
Control Modes

SigGear robotic joint modules support:

Position Control
Velocity Control
Torque Control
Motion Control / MIT Control
Basic State Control

Enter closed-loop control:
odrv0.axis0.requested_state = 8
Enter idle state:
odrv0.axis0.requested_state = 1
Common Commands
| Command                      | Description              |
| ---------------------------- | ------------------------ |
| `dump_errors(odrv0)`         | Print all error messages |
| `odrv0.clear_errors()`       | Clear all errors         |
| `odrv0.save_configuration()` | Save configuration       |
| `odrv0.reboot()`             | Reboot the drive         |
| `odrv0.vbus_voltage`         | Read bus voltage         |
| `odrv0.ibus`                 | Read bus current         |
Repository Structure
SigGear-robot-joint-sdk/
├── README.md
├── docs/
│   ├── CAN_PROTOCOL.md
│   ├── PYTHON_SDK.md
│   ├── ARDUINO_SDK.md
│   ├── ODRIVE_COMPATIBILITY.md
│   ├── MIT_CONTROL.md
│   └── ERROR_CODES.md
├── examples/
│   ├── python/
│   ├── arduino/
│   └── can/
└── tools/
Contact

Website: https://www.siggear.com
Email: wwang109@163.com

---

## 文件：`docs/CAN_PROTOCOL.md`

直接复制：

```markdown
# SigGear CAN Protocol

## Overview

SigGear robotic joint modules use a CAN protocol based on standard 11-bit CAN frames with 8-byte data payloads.

The default CAN baud rate is 500 kbps. The maximum supported CAN baud rate is 1 Mbps.

## CAN Frame Format

```text
CAN_ID = (node_id << 5) + cmd_id
| Field   | Description                         |
| ------- | ----------------------------------- |
| node_id | Unique motor node ID on the CAN bus |
| cmd_id  | Command ID                          |
| data    | 8-byte payload                      |
Byte Order

All integer and floating-point values are encoded in little-endian format.

Floating-point values use IEEE 754 float32 encoding.
Command List
| CMD ID | Name                    | Direction    | Parameters                          |
| ------ | ----------------------- | ------------ | ----------------------------------- |
| 0x001  | Heartbeat               | Motor → Host | Axis_Error, Axis_State, Flags, Life |
| 0x002  | Estop                   | Host → Motor | None                                |
| 0x003  | Get_Error               | Motor → Host | Error_Type                          |
| 0x004  | RxSdo                   | Host → Motor | opcode, Endpoint_ID, Value          |
| 0x005  | TxSdo                   | Motor → Host | opcode, Endpoint_ID, Value          |
| 0x006  | Set_Axis_Node_ID        | Host → Motor | Axis_Node_ID                        |
| 0x007  | Set_Axis_State          | Host → Motor | Axis_Requested_State                |
| 0x008  | Mit_Control             | Host → Motor | MIT control frame                   |
| 0x009  | Get_Encoder_Estimates   | Motor → Host | Pos_Estimate, Vel_Estimate          |
| 0x00A  | Get_Encoder_Count       | Motor → Host | Shadow_Count, Count_In_Cpr          |
| 0x00B  | Set_Controller_Mode     | Host → Motor | Control_Mode, Input_Mode            |
| 0x00C  | Set_Input_Pos           | Host → Motor | Input_Pos, Vel_FF, Torque_FF        |
| 0x00D  | Set_Input_Vel           | Host → Motor | Input_Vel, Torque_FF                |
| 0x00E  | Set_Input_Torque        | Host → Motor | Input_Torque                        |
| 0x00F  | Set_Limits              | Host → Motor | Velocity_Limit, Current_Limit       |
| 0x010  | Start_Anticogging       | Host → Motor | None                                |
| 0x011  | Set_Traj_Vel_Limit      | Host → Motor | Traj_Vel_Limit                      |
| 0x012  | Set_Traj_Accel_Limits   | Host → Motor | Traj_Accel_Limit, Traj_Decel_Limit  |
| 0x013  | Set_Traj_Inertia        | Host → Motor | Traj_Inertia                        |
| 0x014  | Get_Iq                  | Motor → Host | Iq_Setpoint, Iq_Measured            |
| 0x016  | Reboot                  | Host → Motor | None                                |
| 0x017  | Get_Bus_Voltage_Current | Motor → Host | Bus_Voltage, Bus_Current            |
| 0x018  | Clear_Errors            | Host → Motor | None                                |
| 0x019  | Set_Linear_Count        | Host → Motor | Linear_Count                        |
| 0x01A  | Set_Pos_Gain            | Host → Motor | Pos_Gain                            |
| 0x01B  | Set_Vel_Gains           | Host → Motor | Vel_Gain, Vel_Integrator_Gain       |
| 0x01C  | Get_Torques             | Motor → Host | Torque_Setpoint, Torque             |
| 0x01D  | Get_Powers              | Motor → Host | Electrical_Power, Mechanical_Power  |
| 0x01E  | Disable_Can             | Host → Motor | None                                |
| 0x01F  | Save_Configuration      | Host → Motor | None                                |
Set Axis State

CMD ID:
0x007
Payload:
| Byte | Type   | Description          |
| ---- | ------ | -------------------- |
| 0-3  | uint32 | Axis_Requested_State |
Common states:
| Value | Description                |
| ----- | -------------------------- |
| 1     | Idle                       |
| 4     | Motor calibration          |
| 7     | Encoder offset calibration |
| 8     | Closed-loop control        |
Example: enter closed-loop control.
CAN ID: 0x007
Data:   08 00 00 00 00 00 00 00
Set Controller Mode

CMD ID:
0x00B
Payload:
| Byte | Type   | Description  |
| ---- | ------ | ------------ |
| 0-3  | uint32 | Control_Mode |
| 4-7  | uint32 | Input_Mode   |
Control modes:
| Value | Mode             |
| ----- | ---------------- |
| 0     | Voltage control  |
| 1     | Torque control   |
| 2     | Velocity control |
| 3     | Position control |
Input modes:
| Value | Mode                   |
| ----- | ---------------------- |
| 0     | Inactive               |
| 1     | Direct control         |
| 2     | Velocity ramp          |
| 3     | Position filter        |
| 5     | Trapezoidal trajectory |
| 6     | Torque ramp            |
| 9     | Motion control / MIT   |
Velocity Control Example

Set controller mode to velocity control with velocity ramp:
CAN ID: 0x00B
Data:   02 00 00 00 02 00 00 00
Enter closed-loop control:
CAN ID: 0x007
Data:   08 00 00 00 00 00 00 00
Set target velocity to 10 rev/s:
CAN ID: 0x00D
Data:   00 00 20 41 00 00 00 00
Position Control Example

Set controller mode to position control with position filter:
CAN ID: 0x00B
Data:   03 00 00 00 03 00 00 00
Enter closed-loop control:
CAN ID: 0x007
Data:   08 00 00 00 00 00 00 00
Set target position to 2.2 turns:
CAN ID: 0x00C
Data:   CD CC 0C 40 00 00 00 00
Periodic Messages

Periodic messages can be configured through:
odrv0.axis0.config.can.heartbeat_rate_ms
odrv0.axis0.config.can.encoder_rate_ms
odrv0.axis0.config.can.bus_vi_rate_ms
Default enabled messages:
odrv0.axis0.config.can.heartbeat_rate_ms = 0
odrv0.axis0.config.can.encoder_rate_ms = 0

---

## 文件：`docs/MIT_CONTROL.md`

直接复制：

```markdown
# MIT Motion Control

SigGear robotic joint modules support MIT-style motion control over CAN.

This mode combines position, velocity and torque feedforward control and is suitable for dynamic robotic joints such as humanoid knees, hips, shoulders and quadruped legs.

## Control Equation

```text
torque_target = kp * position_error + kd * velocity_error + torque_ff
| Parameter      | Description                         |
| -------------- | ----------------------------------- |
| kp             | Position gain                       |
| kd             | Damping gain                        |
| torque_ff      | Feedforward torque                  |
| position_error | Target position - measured position |
| velocity_error | Target velocity - measured velocity |
Important Note

For USB control, position, velocity and torque values refer to the rotor side.

For CAN MIT control, position, velocity and torque values refer to the output shaft side.

This keeps the protocol compatible with MIT-style robotic actuator control.

CAN Command

CMD ID:
0x008
Direction:
Host → Motor
Host to Motor Frame
| Field    | Bits   | Unit    |
| -------- | ------ | ------- |
| Position | 16-bit | rad     |
| Velocity | 12-bit | rad/s   |
| KP       | 12-bit | gain    |
| KD       | 12-bit | damping |
| Torque   | 12-bit | Nm      |
Scaling

Position:
pos_int = (pos_double + 12.5) * 65535 / 25
Velocity:
vel_int = (vel_double + 65) * 4095 / 130
KP:
kp_int = kp_double * 4095 / 500
KD:
kd_int = kd_double * 4095 / 5
Torque:
t_int = (t_double + 50) * 4095 / 100
Motor to Host Feedback
| Field    | Bits   | Unit  |
| -------- | ------ | ----- |
| Node ID  | 8-bit  | -     |
| Position | 16-bit | rad   |
| Velocity | 12-bit | rad/s |
| Torque   | 12-bit | Nm    |
Feedback conversion:
pos_double = pos_int * 25 / 65535 - 12.5
vel_double = vel_int * 130 / 4095 - 65
t_double   = t_int * 100 / 4095 - 50
Typical Applications
Humanoid robot knee joints
Humanoid robot hip joints
Quadruped robot leg joints
Exoskeleton joints
Dynamic robotic arms

---

## 文件：`docs/PYTHON_SDK.md`

直接复制：

```markdown
# Python SDK

SigGear robotic joint modules are compatible with the ODrive Python toolchain.

## Installation

```bash
pip install --upgrade odrive
pip install numpy matplotlib
Connect to Device
import odrive

odrv0 = odrive.find_any()
Clear Errors
import odrive

odrive.utils.dump_errors(odrv0)
odrv0.clear_errors()
Enter Closed-loop Control
odrv0.axis0.requested_state = 8
Enter Idle State
odrv0.axis0.requested_state = 1
Motor Calibration
import odrive
import time

odrv0 = odrive.find_any()

odrive.utils.dump_errors(odrv0)
odrv0.clear_errors()

odrv0.axis0.requested_state = odrive.utils.AxisState.MOTOR_CALIBRATION
time.sleep(5)

while odrv0.axis0.current_state != 1:
    time.sleep(0.5)

odrive.utils.dump_errors(odrv0)

odrv0.axis0.requested_state = odrive.utils.AxisState.ENCODER_OFFSET_CALIBRATION
time.sleep(6)

while odrv0.axis0.current_state != 1:
    time.sleep(0.5)

odrive.utils.dump_errors(odrv0)

odrv0.axis0.motor.config.pre_calibrated = 1
odrv0.axis0.encoder.config.pre_calibrated = 1
odrv0.save_configuration()
Velocity Control
import odrive
import time

odrv0 = odrive.find_any()

odrv0.axis0.controller.config.control_mode = odrive.utils.ControlMode.VELOCITY_CONTROL
odrv0.axis0.controller.config.input_mode = odrive.utils.InputMode.VEL_RAMP
odrv0.axis0.controller.config.vel_ramp_rate = 50

odrv0.axis0.requested_state = odrive.utils.AxisState.CLOSED_LOOP_CONTROL

odrv0.axis0.controller.input_vel = 15

odrive.utils.dump_errors(odrv0)

time.sleep(5)

odrv0.axis0.controller.input_vel = 0
Position Control
import odrive

odrv0 = odrive.find_any()

odrv0.axis0.controller.config.control_mode = odrive.utils.ControlMode.POSITION_CONTROL
odrv0.axis0.controller.config.input_mode = odrive.utils.InputMode.POS_FILTER

odrv0.axis0.requested_state = odrive.utils.AxisState.CLOSED_LOOP_CONTROL

odrv0.axis0.controller.input_pos = 10
Data Collection
import odrive
import numpy as np

odrv0 = odrive.find_any()

cap = odrive.utils.BulkCapture(
    lambda: [
        odrv0.axis0.motor.current_control.Iq_measured,
        odrv0.axis0.encoder.pos_estimate
    ],
    data_rate=500,
    duration=2.5
)

odrv0.axis0.controller.config.control_mode = odrive.utils.ControlMode.POSITION_CONTROL
odrv0.axis0.controller.config.input_mode = odrive.utils.InputMode.POS_FILTER

odrv0.axis0.requested_state = odrive.utils.AxisState.CLOSED_LOOP_CONTROL
odrv0.axis0.controller.input_pos = 10

np.savetxt("test.csv", cap.data, delimiter=",")
Save Configuration
odrv0.save_configuration()
Restore Configuration
odrivetool restore-config "config_backup.json"

---

## 文件：`docs/ERROR_CODES.md`

直接复制：

```markdown
# Error Codes

## System Errors

| Error Code | Name | Description |
|---|---|---|
| 0x00000002 | DC_BUS_UNDER_VOLTAGE | Power supply voltage too low |
| 0x00000004 | DC_BUS_OVER_VOLTAGE | Power supply voltage too high |
| 0x00000008 | DC_BUS_OVER_REGEN_CURRENT | Reverse charging current too high |
| 0x00000010 | DC_BUS_OVER_CURRENT | Forward discharge current too high |

## Axis Errors

| Error Code | Name | Description |
|---|---|---|
| 0x00000001 | INVALID_STATE | Drive status error |
| 0x00000040 | MOTOR_FAILED | Motor abnormal |
| 0x00000100 | ENCODER_FAILED | Encoder abnormal |
| 0x00000200 | CONTROLLER_FAILED | Controller abnormal |
| 0x00001000 | MIN_ENDSTOP_PRESSED | Minimum limit switch triggered |
| 0x00002000 | MAX_ENDSTOP_PRESSED | Maximum limit switch triggered |
| 0x00004000 | ESTOP_REQUESTED | Emergency stop requested |
| 0x00020000 | HOMING_WITHOUT_ENDSTOP | Homing without limit switch |
| 0x00080000 | UNKNOWN_POSITION | Unknown position |

## Motor Errors

| Error Code | Name | Description |
|---|---|---|
| 0x00000001 | PHASE_RESISTANCE_OUT_OF_RANGE | Phase resistance out of normal range |
| 0x00000002 | PHASE_INDUCTANCE_OUT_OF_RANGE | Phase inductance out of normal range |
| 0x00000010 | CONTROL_DEADLINE_MISSED | FOC frequency too high |
| 0x00000080 | MODULATION_MAGNITUDE | SVM modulation abnormal |
| 0x00000400 | CURRENT_SENSE_SATURATION | Phase current saturation |
| 0x00001000 | CURRENT_LIMIT_VIOLATION | Excessive motor current |
| 0x00020000 | MOTOR_THERMISTOR_OVER_TEMP | Motor temperature too high |
| 0x00040000 | FET_THERMISTOR_OVER_TEMP | Drive temperature too high |
| 0x00400000 | I_BUS_OUT_OF_RANGE | Bus current out of range |
| 0x00800000 | BRAKE_RESISTOR_DISARMED | Brake resistor abnormal |
| 0x800000000 | UNBALANCED_PHASES | Three-phase imbalance |

## Controller Errors

| Error Code | Name | Description |
|---|---|---|
| 0x00000001 | OVERSPEED | Excessive speed |
| 0x00000002 | INVALID_INPUT_MODE | Invalid input mode |
| 0x00000004 | UNSTABLE_GAIN | PLL gain unstable |
| 0x00000020 | INVALID_ESTIMATE | Position or speed unstable |
| - | SPINOUT_DETECTED | Mechanical and electrical power mismatch |

## Encoder Errors

| Error Code | Name | Description |
|---|---|---|
| 0x00000001 | UNSTABLE_GAIN | Encoder bandwidth too high |
| 0x00000002 | CPR_POLEPAIR_MISMATCH | CPR and pole pairs mismatch |
| 0x00000004 | NO_RESPONSE | Encoder not responding |
| 0x00000400 | SEC_ENC_COM_FAIL | Second encoder communication error |
