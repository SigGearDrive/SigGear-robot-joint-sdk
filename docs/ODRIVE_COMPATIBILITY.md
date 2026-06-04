# ODrive Compatibility

## Overview

SigGear robotic joint modules are compatible with the ODrive ecosystem.

This compatibility allows developers to rapidly evaluate and integrate SigGear products using familiar ODrive workflows.

---

# Supported Features

* Python Integration
* USB Communication
* CAN Communication
* Position Control
* Velocity Control
* Torque Control
* Error Diagnostics

---

# Python Installation

```bash
pip install --upgrade odrive
```

---

# Device Discovery

```python
import odrive

odrv0 = odrive.find_any()
```

---

# Enter Closed Loop Control

```python
odrv0.axis0.requested_state = 8
```

---

# Clear Errors

```python
odrv0.clear_errors()
```

---

# Save Configuration

```python
odrv0.save_configuration()
```

---

# Reboot Device

```python
odrv0.reboot()
```

---

# Notes

ODrive is a trademark of ODrive Robotics.

Examples shown in this document are provided for compatibility and integration purposes.

---

# Recommended Applications

* Robot Joint Development
* Humanoid Robot Research
* University Laboratories
* Rapid Prototyping
* Motion Control Evaluation
