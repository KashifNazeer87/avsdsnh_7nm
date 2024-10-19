This repository contains information regarding characterization of a bootstrap switch implementation of sample and hold while utilizing 7nm finFET switches.

# Introduction 
A Sample and Hold (S&H) circuit is an electronic circuit that captures (or "samples") the value of an analog signal at a specific point in time and holds that value for a certain period, allowing it to be processed or converted later. It is an essential component in many analog-to-digital conversion systems (ADCs), where continuous-time analog signals need to be converted into discrete-time signals for further digital processing.
Implementing a Sample and Hold (S&H) circuit in 7nm technology, particularly in advanced designs using FinFET (or similar) transistors, introduces several design challenges and opportunities. In nanoscale technology nodes like 7nm, the small feature sizes offer high speed and low power benefits, but also come with challenges like increased leakage, reduced voltage headroom, and parasitic effects.



# Sample and Hold Circuit- Key parameters
This table summarizes the key parameters and operating conditions of the designed Bootstrapped sample and hold circuit. The key parameters point towards the performance of a sample and hold switch.  


| Paramater    | Condition  | Min  | Typ | Max  | Unit |
|--------------|------------|------|-----|------|------|
|Input offset Voltage              |       27 deg C     |      | 0.35    |      |mV |
|Input Bias Current             |    0-110 deg C         |  -14.9    | -18.8    | -33.5     |pA |
|Input Impedance              |     27 deg C        |      |  186.1   |    |Mohm | 
|Gain Error              |     27 deg C        |      | 1.8 E-6    |      | % |
|Feedthrough reduction ratio              |    27 deg C         |      |  10   |      | dB|
|Output impedance              |     27 deg C        |      |  1.05   | 58.4     | Mohm |
|HOLD Step              |      27 deg C       |      | 0.05     |      |ns |
|Supply current              |      27 deg C       | 0.0135     |     |  3.18E-5    |mA |
|Logic and Logic reference current              |    27 deg C         |   2.79   |     |  3.09    |nA |
|Acquisiton Time              |    27 deg C         |      |     |      | |
|Aperture time              |  27 deg C           |      | 1.49    |      |ns |
|Droop              |  27 deg C           | 0.2     | 0.217     |  0.237    | mV |


# Bootstrap sample and hold circuit overview:

A bootstrapped Sample and Hold (S&H) circuit is an enhanced version of the traditional sample and hold circuit that uses bootstrap techniques to improve the performance of the switch, particularly in terms of maintaining a high and stable switch-on voltage. This allows the circuit to minimize charge injection, improve linearity, and maintain signal integrity, even when operating at low supply voltages, such as those common in advanced technologies like 7nm FinFET.

![bootstrapping circuit for sample and hold](https://github.com/user-attachments/assets/b6cd614c-8821-4b99-ac0c-c68629fc2007)

# Bootstrap sample and hold circuit key components:

# Transistors (FinFETs):

The circuit uses multiple nmos and pmos FinFET transistors for switching purposes.
Transistors are configured as switches for sampling the input signal, bootstrapping, and for holding the sampled voltage on the capacitor.
Capacitors (C1, C2, C3, etc.):

# Capacitors 

Capacitors are used to store the voltage during the sample-and-hold operation.
C1, C2, and C3 (20pF and 2pF) serve as hold capacitors, keeping the sampled voltage stable during the "hold" phase.


# Clock Signals
Two clock signals (CLK and CLK_BAR) are present, where CLK seems to be the main clock signal, and CLK_BAR is its complement.
These clocks control when the circuit samples the input and when it enters the hold phase. CLK would typically enable the sampling phase, while CLK_BAR would enable the hold phase.
Input Signals:

# Input Signal
The input signal (VIN) is connected to transistors and is sampled at the appropriate clock phase.
There are pulse voltage sources (V1, V2, V3, etc.), which represent the analog input signals being sampled.
Output Signal (Vout):

# Output Signal
The signal is held at a node and routed to the output terminal Vout.
The final sampled voltage would appear here, and droop/leakage behavior might be monitored at this node.

# Plot showing input being sampled and held at output along with clock signal

![sampleandhold](https://github.com/user-attachments/assets/fe18f869-0d1b-4f1c-bed4-04aa3bfc2f0b)






# Scope for improvement 

1. Improve Transistor Sizing: Optimize the sizing of the sampling and holding transistors to reduce leakage and ensure proper switching.

2. Reduce Parasitic Capacitance: Parasitic effects may also be contributing to the rapid voltage decay. Ensure the layout is optimized for minimal parasitics.

3. Use alias filter to get rid of alias error.












