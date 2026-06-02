# MWMOTOR SDK Quick Start Guide

## 1. Test Environment

This example has been tested on the following hardware platforms:

* **STM32G431VB** (FDCAN)
* **DJI C Board STM32F407IGH** (CAN)

The project is generated using **STM32CubeMX** and the HAL library.

### CAN Communication Configuration

* CAN baud rate: **500 Kbps**
* CAN interface:

  * FDCAN1 (STM32G431)
  * CAN1 (STM32F407)
* CAN reception is implemented through interrupt mode.
* Please ensure that the CAN TX/RX pins are correctly configured according to your hardware design.

---

## 2. Code Structure

### CANDrive.c

This file contains:

* CAN filter initialization
* CAN transmit functions
* CAN receive functions

For detailed API descriptions, please refer to **CANDrive.h**.

---

### MWMotor.c

This file contains the MW Motor Software Development Kit (SDK).

### Firmware Version Configuration

Before using the SDK, please define the firmware version number in **MWMotor.h**.

The firmware version can be obtained through the motor configuration software.

Current SDK default firmware version:

```c
#define FIRMWARE_VERSION_NUMBER 513
```

Corresponding firmware version:

```text
v0.5.13
```

---

### Motor Registration

Before using the SDK, users must create a motor access structure of type:

```c
MW_MOTOR_ACCESS_INFO
```

After CAN bus initialization, register the motor using:

```c
MWRegisterMotor()
```

The following parameters must be provided:

| Parameter | Description                                                 |
| --------- | ----------------------------------------------------------- |
| busId     | CAN bus ID                                                  |
| nodeId    | Motor node ID                                               |
| motorData | Pointer to motor feedback data structure                    |
| sender    | Motor transmit callback function (user-defined)             |
| notifier  | Motor receive notification callback function (user-defined) |

---

### Important Notes

Default SDK limits:

```text
MAX_BUS_NUM = 8
MAX_MOTOR_NUM_PER_BUS = 16
```

Therefore:

* busId must not exceed 8
* nodeId must not exceed 16

If larger networks are required, modify the following macros in the SDK:

```c
MAX_BUS_NUM

MAX_MOTOR_NUM_PER_BUS
```

---

### MWTest.c

This file contains all variables and test functions required for SDK validation.

The following functions are demonstrated:

#### 1. Configure Maximum Current

Set maximum bus current through Endpoint parameters.

#### 2. Motor Calibration

Execute motor startup calibration.

#### 3. Position Filter Control Test

When:

```c
MODE_TEST = 1
```

the motor runs in Position Filter Control Mode.

#### 4. Velocity Ramp Control Test

When:

```c
MODE_TEST = 2
```

the motor runs in Velocity Ramp Control Mode.

The parameter:

```c
MODE_TEST
```

is defined in:

```text
MWTest.h
```

---

### fdcan.c

Add the initialization code inside the user section of:

```c
MX_FDCAN1_Init()
```

This file performs:

* CAN filter configuration
* CAN receive interrupt initialization

required for SDK operation.

---

## Getting Started

1. Configure CAN hardware and baud rate (500 Kbps).
2. Initialize CAN filters and receive interrupts.
3. Create an `MW_MOTOR_ACCESS_INFO` structure.
4. Register the motor using `MWRegisterMotor()`.
5. Run the examples in `MWTest.c`.
6. Verify motor communication and feedback data.    /* FDCAN初始化 */
    CanFilter_Init();
    HAL_FDCAN_Start(&hfdcan1);
    HAL_FDCAN_ActivateNotification(&hfdcan1,FDCAN_IT_RX_FIFO0_NEW_MESSAGE,0);

The SDK is designed to support position, velocity, torque, MIT control mode, encoder feedback, and CAN-based motor communication.
"Override the HAL library interrupt callback function to receive data."
void HAL_FDCAN_RxFifo0Callback(FDCAN_HandleTypeDef *hfdcan, uint32_t RxFifo0ITs)
{
    if(hfdcan->Instance == FDCAN1)
    {
        /* 获取电机can id */
        uint32_t can_id = CAN_Receive_DataFrame(&hfdcan1, FDCAN1_buff);
        /* 电机数据接收 */
        MWReceiver(1, can_id, FDCAN1_buff);
    }
}
Call MWFunctionTest() in the user code section of the main function in main.c for testing.
