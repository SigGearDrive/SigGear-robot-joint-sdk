# SigGear CAN Protocol

## Overview

SigGear robotic joint modules use CAN communication based on standard 11-bit CAN frames.

Default baud rate:

```text
500 kbps
```

Maximum baud rate:

```text
1 Mbps
```

CAN data length:

```text
8 Bytes
```

---

# CAN ID Structure

```text
CAN_ID = (node_id << 5) + cmd_id
```

| Field      | Bits       |
| ---------- | ---------- |
| Node ID    | Bit10~Bit5 |
| Command ID | Bit4~Bit0  |

Example:

```text
node_id = 0x05
cmd_id = 0x0C

CAN_ID = (0x05 << 5) + 0x0C
```

---

# Supported Commands

| CMD ID | Function             |
| ------ | -------------------- |
| 0x001  | Heartbeat            |
| 0x002  | Emergency Stop       |
| 0x007  | Set Axis State       |
| 0x008  | MIT Control          |
| 0x009  | Get Encoder Estimate |
| 0x00B  | Set Controller Mode  |
| 0x00C  | Set Position         |
| 0x00D  | Set Velocity         |
| 0x00E  | Set Torque           |
| 0x017  | Get Bus Voltage      |
| 0x018  | Clear Errors         |
| 0x01F  | Save Configuration   |

---

# Axis State

| State | Description         |
| ----- | ------------------- |
| 1     | Idle                |
| 4     | Motor Calibration   |
| 7     | Encoder Calibration |
| 8     | Closed Loop Control |

Example:

```text
CAN ID: 0x007
Data: 08 00 00 00 00 00 00 00
```

---

# Position Control

Controller Mode:

```text
Position Control
```

Command:

```text
CMD ID: 0x00C
```

---

# Velocity Control

Controller Mode:

```text
Velocity Control
```

Command:

```text
CMD ID: 0x00D
```

---

# Torque Control

Controller Mode:

```text
Torque Control
```

Command:

```text
CMD ID: 0x00E
```

---

# Heartbeat Message

Heartbeat provides:

* Device Status
* Error Status
* Axis State
* Life Counter

Default Period:

```text
100 ms
```

---

# Encoder Feedback

Default Period:

```text
10 ms
```

Feedback includes:

* Position
* Velocity

---

# Typical Applications

* Humanoid Robots
* Quadruped Robots
* Exoskeleton Systems
* Robot Arms
* AGV & AMR
