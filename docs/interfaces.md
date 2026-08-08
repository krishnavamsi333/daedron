# Daedron — Interface Definition v0.1

## 1. MCU

Target:

- STM32G4 family
- 3.3 V logic
- Advanced motor-control timers
- FDCAN
- ADC resources suitable for synchronized current sampling
- Hardware fault inputs
- Sufficient GPIO for motor, feedback, communication, and diagnostics

The exact MCU and package shall be selected after the complete
interface budget is reviewed.

## 2. Three-Phase PWM

The inverter requires six gate-control signals.

| Signal | Function | Direction |
|---|---|---|
| PWM_UH | Phase U high-side | MCU → gate driver |
| PWM_UL | Phase U low-side | MCU → gate driver |
| PWM_VH | Phase V high-side | MCU → gate driver |
| PWM_VL | Phase V low-side | MCU → gate driver |
| PWM_WH | Phase W high-side | MCU → gate driver |
| PWM_WL | Phase W low-side | MCU → gate driver |

Requirements:

- Complementary PWM generation
- Programmable dead time
- Synchronized ADC triggering
- Hardware emergency shutdown capability

## 3. Gate-Driver Fault

The gate driver shall provide a fault signal to the MCU.

| Signal | Function |
|---|---|
| DRV_FAULT | Gate-driver fault input |

The fault path shall also be capable of directly disabling the power
stage where supported by the selected gate driver.

## 4. Phase Current Sensing

Three current measurements shall be available.

| Signal | Function | MCU Resource |
|---|---|---|
| I_U | Phase U current | ADC |
| I_V | Phase V current | ADC |
| I_W | Phase W current | ADC |

Requirements:

- Synchronized sampling with PWM
- Bidirectional current measurement
- Adequate bandwidth for FOC
- Overcurrent detection
- Calibration capability

The final ADC channels shall be assigned after the exact MCU is chosen.

## 5. DC-Bus Monitoring

The MCU shall measure the DC bus.

| Signal | Function |
|---|---|
| VBUS | DC-bus voltage |

The measurement shall use a protected resistor-divider and appropriate
filtering/conditioning.

The design shall provide hardware protection independently of the ADC
measurement where required.

## 6. Temperature Monitoring

Initial temperature inputs:

| Signal | Function |
|---|---|
| TEMP_PWR | Power-stage temperature |
| TEMP_BOARD | PCB/thermal monitoring |

Additional temperature channels may be added if supported by the
selected MCU.

## 7. Encoder

Incremental encoder interface:

| Signal | Function |
|---|---|
| ENC_A | Encoder A |
| ENC_B | Encoder B |
| ENC_Z | Encoder index |

The MCU timer encoder interface shall be preferred.

Input conditioning shall support the intended encoder voltage level.

## 8. Hall Sensors

Three Hall inputs shall be provided.

| Signal | Function |
|---|---|
| HALL_A | Hall A |
| HALL_B | Hall B |
| HALL_C | Hall C |

The inputs shall include suitable protection and level conditioning.

Hall sensors provide an alternative or complementary rotor-position
feedback method.

## 9. CAN-FD

One CAN-FD interface:

| Signal | Function |
|---|---|
| CAN_TX | MCU → CAN transceiver |
| CAN_RX | CAN transceiver → MCU |

The STM32G4 FDCAN peripheral shall be used.

Physical interface:

- CAN_H
- CAN_L
- GND

Initial architecture:

- Non-isolated
- ESD protection
- Transient protection
- Selectable 120 ohm termination

## 10. Debug Interface

SWD:

| Signal | Function |
|---|---|
| SWDIO | Debug/programming |
| SWCLK | Debug/programming |
| NRST | MCU reset |
| 3V3 | Reference |
| GND | Reference |

## 11. Status Indicators

Minimum MCU-controlled indicators:

- STATUS
- FAULT
- CAN activity

Additional indicators may be added if GPIO and PCB area permit.

## 12. User / Service Interface

The design shall reserve GPIO for future:

- Enable input
- Fault acknowledge
- Service/configuration input
- External emergency-stop interface where appropriate

These shall not consume critical motor-control resources until the
exact requirements are defined.

## 13. Power Monitoring

The MCU shall have access to:

- VBUS
- 5 V logic rail where applicable
- 3.3 V logic rail where applicable
- Temperature monitoring

Power-good/fault signals from regulators shall be considered.

## 14. Hardware Enable

The power stage shall have a dedicated hardware enable/shutdown path.

Target:
