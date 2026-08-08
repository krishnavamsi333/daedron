# Daedron — Requirements v1.0

## 1. Purpose

Daedron is a low-voltage three-phase motor controller designed for
robotic actuators, mobile robots, and embedded electromechanical
systems.

The controller shall provide closed-loop control of BLDC/PMSM motors,
including current, velocity, and position-oriented control functions.

## 2. Target Applications

- Robotic actuators
- Mobile robots
- Wheeled platforms
- Robotic mechanisms
- Mechatronic systems
- Distributed motor-control systems

## 3. Motor

Target motor type:

- 3-phase BLDC/PMSM
- Sensor-based operation
- Field-oriented control capable
- External motor connection

The controller shall support motor parameter configuration.

## 4. DC Bus

Initial target:

- Nominal bus: 48 V DC
- Operating range: 24–52 V DC
- Maximum operating voltage shall be validated against the selected
  power-stage components

The design shall provide:

- Reverse-polarity protection
- DC-bus transient protection
- DC-bus voltage monitoring
- Undervoltage detection
- Overvoltage detection
- Appropriate bulk and ceramic capacitance

## 5. Motor Current

Initial target:

- 10 A continuous phase-current capability
- Higher short-duration peak current capability
- Final peak-current value to be determined from thermal analysis

Current measurement shall support closed-loop current control.

## 6. Power Stage

The controller shall contain:

- Three-phase MOSFET inverter
- Six-switch topology
- High-side and low-side gate driving
- Bootstrap or appropriate high-side supply architecture
- Gate protection
- Dead-time control
- Phase-current measurement

The power stage shall be designed for switching losses,
conduction losses, thermal performance, and EMC.

## 7. Motor Control

The controller shall support:

- Six-step commutation where practical
- Field-oriented control architecture
- Phase-current control
- Velocity control
- Position-control capability through external feedback

The firmware architecture shall separate:

- Fast current loop
- Velocity loop
- Position loop
- Communication
- Diagnostics

## 8. Position Feedback

The controller shall support an encoder interface.

Initial target:

- Incremental quadrature encoder
- A/B signals
- Index signal
- 5 V or 3.3 V compatible interface as determined during design

Optional future support:

- Hall sensors
- Absolute encoder interface

## 9. Current Sensing

The controller shall measure motor phase current.

Target:

- Three-phase current measurement
- Current-sense amplifier or integrated sensing solution
- Sufficient bandwidth for current-control loop
- Overcurrent detection independent of firmware where practical

## 10. MCU

Target:

- STM32G4 family
- Hardware PWM/timer resources suitable for three-phase motor control
- ADC capability suitable for synchronized current sampling
- Hardware protection/fault inputs
- CAN-FD capability
- Sufficient processing performance for FOC

Exact MCU part shall be selected during architecture and interface
definition.

## 11. Communication

Primary communication:

- 1 × CAN-FD

The CAN interface shall support:

- Motor commands
- Velocity commands
- Position commands
- Telemetry
- Fault reporting
- Configuration

The physical interface shall include appropriate ESD and transient
protection.

## 12. Protection

The controller shall detect and respond to:

- Phase overcurrent
- DC-bus overvoltage
- DC-bus undervoltage
- MOSFET overtemperature
- PCB/power-stage overtemperature
- Gate-driver fault
- Encoder/feedback fault
- MCU watchdog fault

Hardware protection shall be used for fast shutdown of the power stage
where practical.

## 13. Regenerative Braking

The architecture shall account for energy returned to the DC bus
during deceleration.

The design shall provide a defined strategy for:

- DC-bus overvoltage detection
- Controlled deceleration
- External braking provision or future braking circuitry

The final regenerative-braking implementation shall be determined
during architecture.

## 14. Thermal

The design shall monitor relevant temperatures.

Target measurements:

- Power-stage/MOSFET temperature
- Gate-driver temperature where practical
- PCB thermal hotspot

The PCB shall provide adequate copper area and thermal paths for the
expected continuous current.

## 15. Power Supplies

The board shall generate the required low-voltage rails for:

- MCU
- Gate driver
- Current sensing
- Encoder interface
- CAN transceiver
- Auxiliary circuitry

The power architecture shall separate noisy power-stage circuitry
from sensitive control circuitry.

## 16. PCB

Initial target:

- 4-layer PCB preferred
- Compact robotics-oriented form factor
- High-current copper paths
- Dedicated power-stage thermal regions
- Controlled separation between power and logic
- Accessible test points

Final dimensions shall be determined after power-stage floorplanning.

## 17. Diagnostics

The controller shall provide diagnostics for:

- DC-bus voltage
- Motor current
- Temperature
- Gate-driver faults
- Encoder status
- CAN communication
- Controller state
- Active fault conditions

## 18. Safe State

The power stage shall default to a disabled state during:

- MCU reset
- MCU startup
- Watchdog timeout
- Gate-driver fault
- Critical overcurrent
- Critical overvoltage
- Loss of required control power

## 19. Manufacturing

The design shall support:

- Standard PCB fabrication
- Automated assembly where practical
- Thermal inspection
- Electrical test
- Motor-control bring-up
- Test-point access

## 20. Validation

The prototype shall be tested for:

- DC-bus operation
- Power-stage switching
- Gate-drive timing
- Current measurement
- Overcurrent shutdown
- Motor commutation
- FOC operation
- Encoder feedback
- Velocity control
- Position control
- CAN-FD communication
- Thermal performance
- Regenerative braking behavior
- Fault handling

## 21. Status

Requirements: v1.0 Draft

Architecture: Not started

Interfaces: Not started

Schematic: Not started

PCB: Not started

Prototype: Not started

Validation: Not started
