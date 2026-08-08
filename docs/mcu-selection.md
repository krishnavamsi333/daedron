# Daedron — MCU Selection v1.0

## Selected MCU

- Manufacturer: STMicroelectronics
- Family: STM32G4
- Part: STM32G474RE
- Package: LQFP-64
- Core: Arm Cortex-M4F
- Maximum CPU frequency: 170 MHz

## Reason for Selection

The STM32G474RE provides substantial headroom for Daedron's
three-phase motor-control application.

Required capabilities include:

- Advanced motor-control PWM
- Complementary PWM outputs
- Programmable dead time
- Hardware emergency shutdown
- Fast ADC resources
- FDCAN
- Encoder-capable timers
- DMA
- Sufficient Flash and SRAM
- Floating-point support

Additional useful capabilities include:

- CORDIC accelerator
- FMAC accelerator
- Multiple comparators
- Integrated operational amplifiers
- Multiple ADC peripherals
- Multiple FDCAN controllers

## Motor-Control Requirements

The MCU shall provide resources for:

- 6 complementary inverter PWM signals
- PWM-synchronized ADC sampling
- Hardware power-stage fault shutdown
- 3 phase-current measurements
- DC-bus voltage measurement
- Temperature measurements
- Incremental encoder
- Hall sensors
- CAN-FD
- SWD debugging

## Design Margin

The MCU shall not be designed to use every available peripheral or
GPIO.

Unused resources shall be retained for:

- Diagnostics
- Future firmware features
- Additional sensors
- Service interfaces
- Hardware revisions

## Clock

An accurate external clock source shall be evaluated for the CAN-FD
interface and overall timing requirements.

## Status

MCU family: Frozen

Exact MCU: STM32G474RE

Package: LQFP-64

Selection: Frozen v1.0

Pin assignment: Not started
