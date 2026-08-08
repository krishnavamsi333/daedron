# Daedron — System Architecture v0.1

## 1. Purpose

Daedron is a 48 V-class three-phase BLDC/PMSM motor controller for
robotic and electromechanical applications.

The architecture separates the high-power motor domain from the
low-voltage control and communication circuitry.

## 2. Top-Level Architecture

```text
                         DAEDRON
┌──────────────────────────────────────────────────────────┐
│                                                          │
│                    DC BUS 24–52 V                        │
│                         │                                │
│              ┌──────────▼──────────┐                    │
│              │ Input Protection &  │                    │
│              │ DC Bus Monitoring   │                    │
│              └──────────┬──────────┘                    │
│                         │                                │
│              ┌──────────▼──────────┐                    │
│              │  Bulk DC Bus        │                    │
│              │  Capacitance        │                    │
│              └──────────┬──────────┘                    │
│                         │                                │
│              ┌──────────▼──────────┐                    │
│              │ 3-Phase MOSFET      │                    │
│              │ Inverter             │                    │
│              └─────┬────┬────┬────┘                    │
│                    │    │    │                           │
│                   U     V    W                           │
│                    │    │    │                           │
│                    └────┼────┘                           │
│                         ▼                                │
│                    BLDC/PMSM                             │
│                                                          │
│   ┌──────────────────────────────────────────────────┐   │
│   │                 CURRENT SENSING                   │   │
│   │              Phase U / V / W                      │   │
│   └──────────────────────┬───────────────────────────┘   │
│                          │                               │
│   ┌──────────────────────▼───────────────────────────┐   │
│   │                    STM32G4                        │   │
│   │                                                  │   │
│   │  FOC │ PWM │ ADC │ Timers │ Fault handling      │   │
│   └──────────┬───────────────────────┬───────────────┘   │
│              │                       │                   │
│        ┌─────▼─────┐           ┌─────▼─────┐             │
│        │ Encoder / │           │  CAN-FD   │             │
│        │ Hall      │           │ Interface │             │
│        └───────────┘           └───────────┘             │
│                                                          │
└──────────────────────────────────────────────────────────┘
