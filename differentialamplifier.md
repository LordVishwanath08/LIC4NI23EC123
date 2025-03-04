## Differential Amplifier

A differential amplifier is an electronic circuit that amplifies the difference between two input signals while rejecting any signals that are common to both inputs.

![image](https://github.com/user-attachments/assets/cd0e449c-8f0d-419c-bd24-090add6e9e81)

This Expereiment is Based on Common Mode Input voltage Differential Amplifier and this Experiement is conducted in 3 stages.Where common source terminal is connected with
Resistor(Rss), Current source, nMOSFET, For all this circuit we need to find Dc Operating point, and do Transient analysis And AC analysis, Frequency Response.

## Design Specifications.
P<=3mA <br />
Vdd=2.5V <br />
Vicm=1.3V <br />
Vocm=1.4V <br />
Vp=0.5V <br />
l=180nm and w=20u

## Design and calculations
P=Vdd*Iss <br />
Iss=3m/2.5 = 1.2mA <br />
Id1=Id2=Iss/2=0.6mA <br />

RD=VDD-Vocm/Iss=1.83kΩ <br />
Rss=Vp/Iss=0.416kΩ <br />

M1 Q-Point(0.902V,0.6mA) <br />
M2 Q-Point(0.902V,0.6mA) <br />

## DC analysis of Mosfet with resistor
In this circuit, two MOSFETs are connected to the same voltage input, forming a differential pair. A load resistor is connected to the drain terminal of each MOSFET. The source terminals share a common resistor, which is connected to the ground—this resistor is known as the **source degeneration resistor**.  

The presence of this resistor at the common source terminal influences key circuit parameters, including voltage gain, input impedance, and linearity. Specifically, it enhances linearity while also increasing impedance. Since this is a **closed-loop amplifier**, it introduces feedback for all elements connected to the common source terminal, effectively making it a **feedback amplifier**.

![pic1](https://github.com/user-attachments/assets/d93d8984-f83e-4ec2-90da-425ec63e779f)


## Transient Analysis 

The transient analysis explain the circuit response at a particular instant of time when a time-varying signal is applied at the inputs.In this experiment we can see a complete phase shift of 180 degree output to the input signal.As with respect to context of voltage gain, as the volatge gain is more leads to the smaller the bandwidth size.
At the particular time output wave changes with respect input in the amplitude.

![pic2](https://github.com/user-attachments/assets/3a272a52-e067-49c3-93e3-e855258c1efe)

Av=(1.44-1.25/1.34-1.25)=0.19/0.09=2.111


##Circuit with constant current source 
We replaced resistor by constant current source. We have two MOSFET connected to same voltage input forming differential pair.And current source is connected to the Drain terminal of MOSFET.
Source terminal is connected to the current source and another terminal is connected to ground.

DC Analysis
![image](https://github.com/user-attachments/assets/ef162e24-7116-4f20-b986-6ce25020900b)

Transient analysis

The transient analysis explain the circuit response at a particular instant of time when a time-varying signal is applied at the inputs.In this experiment we can see a complete phase shift of 180 degree output to the input signal.As with respect to context of voltage gain, as the volatge gain is more leads to the smaller the bandwidth size.
At the particular time output wave changes with respect input in the amplitude.

![image](https://github.com/user-attachments/assets/9c6f5a86-432c-4c46-a5de-6928022fbb99)



## Circuit with the mosfet
Replacing the current source with a MOSFET (M3) allows us to set the desired drain current \( I_{D3} \). To ensure proper operation, MOSFETs **M1, M2, and M3** must remain in the **saturation region**, which helps maintain the required voltage gain. In this circuit, the MOSFET is connected with its drain to the source terminal and then to the ground.

## DC Analysis 
![image](https://github.com/user-attachments/assets/fad23eb1-9f76-49b5-97fb-37f4cd478317)

## Transient Analysis 
![image](https://github.com/user-attachments/assets/fb503fdf-ad0a-467c-805d-874a33fb0d51)

##b Inference 
A differential amplifier with a constant current source or MOSFET-based current source provides better stability, gain control, and linearity compared to a resistor-based biasing method. Using MOSFETs in the saturation region ensures consistent performance, making it a preferred design choice for high-precision applications.


