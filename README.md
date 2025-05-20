# BJT Master-Slave D-Type Flip-Flop

This repository contains the circuit diagram for a Master-Slave D-Type Flip-Flop implemented entirely using discrete NPN Bipolar Junction Transistors (BJTs) and passive components. This design demonstrates the fundamental building blocks of digital logic circuits.

![MasterSlaveFlipFlop](https://github.com/user-attachments/assets/63a6d97b-a22f-47de-b1bb-3a13a3dbbbe4)


![20250520_193316](https://github.com/user-attachments/assets/2dc6a999-c751-4306-b16c-fb21dd1bce16)


## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Circuit Description](#circuit-description)
  - [Master Latch](#master-latch)
  - [Slave Latch](#slave-latch)
  - [Clocking](#clocking)
- [Components List](#components-list)
- [Power Supply](#power-supply)
- [Inputs and Outputs](#inputs-and-outputs)
- [Operation](#operation)
- [Potential Applications](#potential-applications)
- [Limitations](#limitations)
- [Contributing](#contributing)
- [License](#license)

## Introduction

A D-type flip-flop is a fundamental digital memory element that stores one bit of information. It has a data input (D) and a clock input (CLK). On the active edge of the clock signal, the value at the D input is transferred to the Q output.

The master-slave configuration uses two latches: a "master" latch and a "slave" latch.
- The master latch is enabled by one clock level (e.g., CLK high).
- The slave latch is enabled by the opposite clock level (e.g., CLK low, typically via an inverted clock signal).

This arrangement ensures that the output Q only changes on a specific clock edge (e.g., the falling edge if the master is positive level-triggered and the slave is negative level-triggered via an inverter), preventing race conditions and ensuring stable operation.

## Features

-   **Edge-Triggered:** The output Q updates based on the D input only on a specific clock signal transition.
-   **Discrete Component Design:** Implemented using NPN BJTs, resistors, and a capacitor.
-   **Master-Slave Architecture:** Provides robust data latching.
-   **Q and Q' (implied) Outputs:** Provides the main output (Q, with LED indicator) and an implied complementary output.
-   **Manual Inputs:** Designed for manual operation via switches for Data (D) and Clock (CLK).

## Circuit Description

The circuit consists of two main latch sections (master and slave), each built from BJT-based logic gates (effectively NAND gates cross-coupled to form SR latches, adapted for D-type operation).

### Master Latch
The first section of the circuit (left/middle part) forms the master latch. It takes the D input and the direct clock signal. When the clock signal allows (e.g., CLK is high), the master latch tracks the D input.

### Slave Latch
The second section (middle/right part) forms the slave latch. Its data input comes from the output of the master latch. Its clock input is an inverted version of the main clock signal (the single BJT inverter connected to the clock line serves this purpose). When its clock input is active (e.g., main CLK is low, inverted clock is high), the slave latch takes the data from the master latch and presents it to the Q output.

### Clocking
-   The clock input (CLK) is manually controlled by a switch.
-   A 100nF capacitor and 10kΩ resistor at the clock input likely provide some debouncing or edge shaping.
-   A BJT inverter stage inverts the clock signal for the slave latch. This means:
    -   If the master latch is active on CLK HIGH, the slave latch is active on CLK LOW.
    -   The overall D flip-flop will typically be **falling-edge triggered** if the master is enabled when CLK is high. (Or rising edge if the master is enabled when CLK is low, depending on the exact BJT NOR gate implementation details).

## Components List

-   **Transistors (NPN BJTs):** 18 (e.g., 2N3904, BC547, or similar general-purpose NPN)
-   **Resistors:**
    -   1kΩ: 28
    -   10kΩ: 1 (at clock input)
    -   300Ω: 2 (for output indicators/current limiting)
-   **Capacitors:**
    -   100nF: 1 (at clock input)
-   **LEDs:**
    -   1 Red LED (for NOT Q output indication)
    -   1 Green LED (for  Q output indication)
-   **Switches:**
    -   1 Push Button  (for CLK inputs)
    -   1 SPST Switch  (for D inputs)
-   **Power Supply:** +5V DC

## Power Supply

-   **Voltage:** +5V DC
-   **Ground:** Common ground reference.

## Inputs and Outputs

-   **Inputs:**
    -   **D (Data):** Manually set to HIGH (+5V via 1kΩ resistor) or LOW (GND) using a switch.
    -   **CLK (Clock):** Manually toggled HIGH (+5V) or LOW (GND reference via 10kΩ resistor and capacitor) using a switch.
-   **Outputs:**
    -   **Q:** The primary output of the flip-flop. Indicated by an LED.
    -   **Q' (Complementary Output):** The node connected to the other 300Ω resistor provides the complementary output (though not explicitly labeled Q').

## Operation

1.  **Set Data (D) Input:** Use the D input switch to set the desired data bit (HIGH or LOW).
2.  **Apply Clock Pulse:**
    *   Initially, the clock might be LOW.
    *   Transition the CLK input switch from LOW to HIGH, then back to LOW (a full pulse).
3.  **Observe Output (Q):**
    *   The Q output (and the LED) will update to reflect the D input state *at the active clock edge*.
    *   For this configuration, if the master is active high and slave active low (due to inverter), the Q output will change on the **falling edge** of the CLK signal.
    *   Specifically:
        *   When CLK is HIGH: The master latch "sees" the D input. The slave latch holds the previous state.
        *   When CLK transitions from HIGH to LOW: The master latch holds its value. The slave latch now "sees" the master's output and transfers it to Q.

## Potential Applications

While discrete BJT flip-flops are rarely used in modern complex systems (ICs are preferred), understanding their operation is crucial for:
-   Educational purposes in digital electronics.
-   Hobbyist projects.
-   Understanding the internal workings of integrated circuit flip-flops.
-   Building simple sequencers, counters, or registers with discrete components.

## Limitations

-   **Speed:** Discrete BJT implementations are much slower than integrated circuits.
-   **Size:** Physically larger than IC equivalents.
-   **Power Consumption:** Potentially higher than CMOS ICs.
-   **Manual Clocking:** The current setup is for manual clocking; for higher frequencies, a proper clock generator would be needed.
-   **No Asynchronous Set/Reset:** This design does not include asynchronous preset or clear inputs.

## Contributing

Contributions, suggestions, and improvements are welcome! Please feel free to fork the repository, make changes, and submit a pull request. You can also open an issue if you find any bugs or have ideas for enhancements.

