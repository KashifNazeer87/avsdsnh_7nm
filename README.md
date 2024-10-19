This repository contains information regarding characterization of a bootstrap switch implementation of sample and hold while utilizing 7nm finFET switches. An emphasis has been made on functionality.

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
|Acquisiton Time              |    27 deg C         |      | 1.49    |      | ns |
|Aperture time              |  27 deg C           |      | 0.00237   |      |ns |
|Settling Time              |  27 deg C           |      | 0.02          |      | ns   |         
|Droop              |  27 deg C           | 0.01     | 0.03     |  0.09    | mV |


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

# Characterization

![sampleandhold](https://github.com/user-attachments/assets/fe18f869-0d1b-4f1c-bed4-04aa3bfc2f0b)

# Explanation of parameters 

The figure below depict the various timing related and voltage droop replated parameters. These are acquired by visual inspection of the transient characteristic of the circuit.

![parameter related to time and droop for snh](https://github.com/user-attachments/assets/0d868e85-30cd-454e-ae57-8e4152ae93ba)

**1. Acquisition Time:**   
Acquisition time refers to the time required for a Sample and Hold (S&H) circuit to sample and acquire an accurate representation of the input signal. More specifically, it's the period during which the input signal is connected to the sampling capacitor, allowing the voltage across the capacitor to settle to within a certain accuracy of the input signal's voltage.

The acquisition time is governed by the RC time constant of the circuit:
𝜏=𝑅𝑂𝑁 × 𝐶𝐻

The capacitor charges up exponentially, reaching approximately 63% of the final value in one time constant 
𝜏
τ, 86% in two time constants, and about 99% in five time constants.
To achieve high accuracy (e.g., settling to within 0.01% of the final value), multiple time constants are needed, leading to a longer acquisition time.

**2. Aperture Time:** 
Aperture time in a Sample and Hold (S&H) circuit is the time window during which the circuit transitions from sampling the input signal to holding a fixed value. It represents the uncertainty in the exact instant when the S&H circuit actually stops tracking the input signal and begins holding the sampled value.
In simpler terms, aperture time defines how precisely the S&H circuit captures the input signal at the intended sampling moment. It is particularly important in high-speed and high-frequency applications, as it affects the accuracy of the sampled signal.


**3. Settling Time:** 
Settling time in a Sample and Hold (S&H) circuit refers to the time required for the output of the circuit to stabilize or "settle" to the final value of the input signal after switching from the sample mode to the hold mode. During this time, the S&H circuit's output needs to reach the desired voltage (typically within a specified error tolerance) after experiencing the transients caused by switching.
The time constant T is given by:
τ= Ron x Ch
Where 
Ron - switching on resistance
Ch - Hold capacitance

The output voltage of capacitor follows an exponential decay after switching:
V(t)=Vfinal (1−e^(t/τ))
​
In one time constant (𝜏), the output settles to about 63% of the final value. Typically, five time constants (5τ) are needed for the output to settle to within 99% of the final value.

**4. Droop**
Voltage droop in a Sample and Hold (S&H) circuit refers to the gradual decrease in the voltage stored on the holding capacitor during the hold phase. This droop occurs because of various leakage mechanisms that slowly discharge the capacitor, causing the output voltage to deviate from the initially sampled value over time.

*Analytically* 

Vhold(t) = Vinitial(t) x e^(-t/RC)

Where,

R           =  The equivalent resistance due to leakage paths and load impedance.

C           = The capacitance of the holding capacitor.

Vhold(t)    =  is the voltage on the capacitor at time t.

Vinitial(t) = The initial voltage stored on the capacitor.
 
 
**5. Input Offset Voltage:**
In a Sample and Hold (S&H) circuit, input offset voltage refers to the small voltage difference that may appear at the input due to imperfections in the switches, buffer amplifiers, or other active components (such as operational amplifiers) used in the circuit. This offset voltage results in a slight error in the sampled signal, causing the stored voltage on the holding capacitor to deviate from the actual input signal voltage.

From visual inspection at zero input the output at 0 input is noted.

Alternatively

*Analytical approach*
We are assuming unity gain for the buffer.
Vos = Vout/ Av

Where Vos is the offset voltage

Av is Gain of the buffer.

Vout is the output voltage.


**6. Input bias current**
Input bias current in a Sample and Hold (S&H) circuit refers to the small amount of current that flows into the input terminals of active components (such as buffer amplifiers or op-amps) used in the circuit. This current is typically associated with MOSFET gates or bipolar transistor bases in the input stage of amplifiers and can impact the accuracy of the sampled voltage by introducing small errors over time.

In an ideal amplifier or switch, no current should flow into the input terminals. However, in real-world components (e.g., op-amps or MOSFET gates), there is a small input bias current due to imperfections in the transistors used in the input stage.

Input bias current is often measured across a temperature range because it is highly temperature-dependent, meaning that its magnitude can change significantly with variations in temperature. Understanding how input bias current behaves over a range of temperatures is crucial, particularly for precision circuits like Sample and Hold (S&H) circuits, because temperature fluctuations can introduce errors that affect the performance and accuracy of the circuit.

- For operational temperature:

  We print the value of input current for a DC sweep from 0 to 0.7 mV.
  Syntax
   print i(vector of input voltage that contains current)

  This gives us the typical value of current.
  
- For maximum and minimum values
- 
 We perform a temperature sweep from 0 deg C to 110 deg C 

 This sweep gives us the minimum and maximum values of input bias current.

 ![offset temp](https://github.com/user-attachments/assets/74913764-3921-4578-bb47-1c1169a93021)

 **7. Input Impedance:**

 Input impedance of a Sample and Hold (S&H) circuit refers to the impedance seen by the signal source when connected to the input of the S&H circuit. It plays a crucial role in determining how the signal source interacts with the circuit and affects the accuracy of the sampled signal.

 *Analytical approach*

 Zin = Vin/Iin

 where 

 Zin= input impedance
 Vin = input voltage
 Iin= input current

 **8. Gain Error**

 Gain error in a Sample and Hold (S&H) circuit refers to the deviation between the actual gain of the circuit and the ideal gain, which affects the accuracy of the sampled output signal relative to the input. In an ideal S&H circuit, the output should exactly replicate the input signal during the hold phase, with a gain of 1 (unity gain). However, various non-idealities can cause the actual gain to differ from this ideal value, leading to gain error.

*Analytically*

Gain Error can be found by applying the following formula:

Gain Error = ((Vout/Vin) - 1 ) x 100%


# Scope for improvement 

1. Improve Transistor Sizing: Optimize the sizing of the sampling and holding transistors to reduce leakage and ensure proper switching.

2. Reduce Parasitic Capacitance: Parasitic effects may also be contributing to the rapid voltage decay. Ensure the layout is optimized for minimal parasitics.

3. Use alias filter to get rid of alias error.


# References:

1. https://www.digikey.com/en/articles/analog-fundamentals-sample-and-hold-circuits-work-adc-accuracy


# Acknowledgement

- Kunal Ghosh, Co-Founder of VLSI System Design (VSD) Corp. Pvt. Ltd.

- Dr. Skandha Deepsita, Physical Design Consultant.












