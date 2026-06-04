# Error Codes

## System Errors

| Error                     | Description                   |
| ------------------------- | ----------------------------- |
| DC_BUS_UNDER_VOLTAGE      | Supply voltage too low        |
| DC_BUS_OVER_VOLTAGE       | Supply voltage too high       |
| DC_BUS_OVER_CURRENT       | Bus current too high          |
| DC_BUS_OVER_REGEN_CURRENT | Regenerative current too high |

---

# Axis Errors

| Error             | Description              |
| ----------------- | ------------------------ |
| INVALID_STATE     | Invalid drive state      |
| MOTOR_FAILED      | Motor error              |
| ENCODER_FAILED    | Encoder error            |
| CONTROLLER_FAILED | Controller error         |
| ESTOP_REQUESTED   | Emergency stop activated |
| UNKNOWN_POSITION  | Position unknown         |

---

# Motor Errors

| Error                         | Description                 |
| ----------------------------- | --------------------------- |
| PHASE_RESISTANCE_OUT_OF_RANGE | Phase resistance abnormal   |
| PHASE_INDUCTANCE_OUT_OF_RANGE | Phase inductance abnormal   |
| CURRENT_LIMIT_VIOLATION       | Current limit exceeded      |
| MOTOR_THERMISTOR_OVER_TEMP    | Motor temperature too high  |
| FET_THERMISTOR_OVER_TEMP      | Driver temperature too high |
| I_BUS_OUT_OF_RANGE            | Bus current out of range    |

---

# Controller Errors

| Error              | Description               |
| ------------------ | ------------------------- |
| OVERSPEED          | Motor overspeed           |
| INVALID_INPUT_MODE | Invalid input mode        |
| INVALID_ESTIMATE   | Invalid position estimate |
| SPINOUT_DETECTED   | Mechanical instability    |

---

# Encoder Errors

| Error                 | Description                 |
| --------------------- | --------------------------- |
| NO_RESPONSE           | Encoder not responding      |
| CPR_POLEPAIR_MISMATCH | Configuration mismatch      |
| SEC_ENC_COM_FAIL      | Encoder communication error |

---

# Recommended Troubleshooting

## Motor Not Moving

Check:

* Power Supply
* CAN Wiring
* Axis State
* Encoder Status

## Over Temperature

Check:

* Cooling
* Load Conditions
* Current Limit Settings

## Encoder Failure

Check:

* Encoder Connection
* Encoder Configuration
* Cable Integrity
