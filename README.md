# avsdsnh_7nm

This repository contains information regarding characterization of a bootstrap switch implementation of sample and hold while utilizing 7nm finFET switches.


![bootstrapping circuit for sample and hold](https://github.com/user-attachments/assets/b6cd614c-8821-4b99-ac0c-c68629fc2007)

Main Components:
Transistors (FinFETs):

The circuit uses multiple nmos and pmos FinFET transistors for switching purposes.
Transistors are configured as switches for sampling the input signal, bootstrapping, and for holding the sampled voltage on the capacitor.
Capacitors (C1, C2, C3, etc.):

Capacitors are used to store the voltage during the sample-and-hold operation.
C1, C2, and C3 (20pF and 2pF) serve as hold capacitors, keeping the sampled voltage stable during the "hold" phase.
Clock Signals (CLK, CLK_BAR, etc.):

Two clock signals (CLK and CLK_BAR) are present, where CLK seems to be the main clock signal, and CLK_BAR is its complement.
These clocks control when the circuit samples the input and when it enters the hold phase. CLK would typically enable the sampling phase, while CLK_BAR would enable the hold phase.
Input Signals:

The input signal (IN) is connected to transistors and is sampled at the appropriate clock phase.
There are pulse voltage sources (V1, V2, V3, etc.), which represent the analog input signals being sampled.
Output Signal (Vout):

The signal is held at a node and routed to the output terminal Vout.
The final sampled voltage would appear here, and droop/leakage behavior might be monitored at this node.

# Plot showing input being sampled and held at output along with clock signal

![sampleandhold](https://github.com/user-attachments/assets/9afef062-7d8f-44b3-b5cc-639df24016a2)

# Scope for improvement 

1. Improve Transistor Sizing: Optimize the sizing of the sampling and holding transistors to reduce leakage and ensure proper switching.

2. Reduce Parasitic Capacitance: Parasitic effects may also be contributing to the rapid voltage decay. Ensure the layout is optimized for minimal parasitics.


# Datasheet


| Paramater | Condition | Min | Typ | Max |

