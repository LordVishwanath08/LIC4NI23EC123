# Task – 2 
We are supposed to replace the R_D with the pmos4 and do the all the analysis, DC, AC, Transient
Procedure
1.	We are supposed to rig up the circuit in the tool window and measure the DC Q-point, according to the requirements we have been given.
2.	Make sure to save the TSMC 180 nm SPICE netlist, or .lib file in the folder where you have saved LTSpice on your system.
3.	Open the LTSpice simulation tool, and click on the IC symbol, which contains the the list of components available. From the list, select nmos4 and pmos4 which is a 4 terminal NMOS and PMOS, After placing the NMOS and PMOS, place the rest of the required components, assemble the circuit as per the given circuit diagram. 
4.	Select the .t  symbol on the toolbar. This lets you add a SPICE directive, which will allow you to specify the process technology and the parameters for the MOSFET. In this case, we will be using the TSMC 180 nm 
5.	Next, using the .t tool, give the directive, .lib tsmc018.lib, and click ‘OK’. Then place this command anywhere in the schematic.
6.	After this, we can perform various analyses - DC, AC, transient, DC operating point, etc. 


### DC Operating Point

Given that power budget = 50 𝜇W, we use P = VDD. ID, to calculate ID, given that supply voltage VDD = 1.8V.
50 𝜇W = (1.8) x ID, which gives us ID = 27.778 𝜇A.
To perform this analysis, we go to the Run icon on the LTSpice toolbar, or use the Alt + R shortcut. After that, click on the DC operating point tab. Then click ‘OK’, and place the .op file anywhere on the schematic.
This will open a window of all the node voltages, branch currents and resistances in your schematic

### Results 
![image](https://github.com/user-attachments/assets/4d7d0c86-4d81-4928-b84f-e3d1e02020d2)

 
### Transient Analysis
We will now conduct a transient simulation in LTSpice to observe how the output voltage (VD) evolves over time. Since we are dealing with a time-dependent signal, an AC excitation is required.
1.	Setting up the AC Source:
o	Locate the gate voltage source, VG, in your schematic.
o	Right-click on VG to open its configuration dialog.
o	Select the “Advanced” option and then choose “SINE” to specify that the input will be a sine wave.
2.	Configuring the Sine Wave Parameters:
o	DC Offset: Set to 0.9 V. This value ensures that the DC operating point remains unaffected.
o	Amplitude: Set to 50 mV, which keeps the signal within the small-signal regime (i.e., ensuring Vgs is much less than 2VOV).
o	Frequency: Set to 1 kHz.
3.	Running the Transient Analysis:
o	Open the “Configure Analysis” window by clicking the Run 
o	Switch to the Transient tab and set the stop time to 5 ms.
o	Finally, insert the command .tran 5m anywhere on your schematic and execute the simulation.


### Results
 ![image](https://github.com/user-attachments/assets/737003b9-8552-4d28-adef-81298c0906c1)

We can see that the waveform is inverted compared to the input. This indicates a 180° phase shift, which results in a negative gain.
Since we know the amplitude of the input voltage, Vin, and approximated amplitude of the output voltage, Vout, we can calculate small signal gain.
Av = -( Vout/ Vin) = -(1.52/50m) = -30.4

## AC Analysis
•  Accessing the AC Analysis Settings:
•	Click the Run icon and select “Configure Analysis.”
•	Navigate to the AC analysis tab.
•  Setting Up the Sweep Parameters:
•	Sweep Type: Choose “Decade” to generate a logarithmic sweep, ensuring the gain is represented in dB per decade.
•	Points per Decade: Set this to 20 to obtain a detailed plot.
•	Frequency Range: Specify a start frequency of 0.1 Hz and an end frequency of 1 THz, covering a broad spectrum.
•  Final Steps:
•	Place the directive .ac dec 20 0.1 1T anywhere on your schematic.
•	Run the simulation to generate the Bode plot.

### Results
![image](https://github.com/user-attachments/assets/f5197ed5-7e23-4cc1-9213-7e3c1dbac170)

  
From the plot, we can see that the midband gain is around -18.5 dB, for an input ac sine signal, of amplitude 50 mV. The gain is negative due to a 180° phase shift, which inverts the output compared to the input. We can also see that the phase shift is approximately between 160° - 180°, but closer to 180°, which explains the reason for the negative gain and the inverted output.
Converting our gain from V/V to dB, using the formula A’V = -10log10(Av)
A’V = -20log10(30.4) = -20(1.4828) = -29.656
∴ A’V = -29.656, which matches with the gain value from the Bode plot.
We can also see that the gain begins falling at around 1 GHz, which we can assume to be the fH value. 
DC Sweep 
Transfer Characteristics
•  Open the Analysis Configuration:
•	Click on the “Configure Analysis” button in LTSpice.
•  Select the DC Sweep Option:
•	Choose the DC sweep tab within the configuration window.
•  Input the Sweep Parameters:
•	Source to Sweep: Set this to VG (the gate voltage).
•	Sweep Type: Choose a linear sweep.
•	Start Voltage: 0 V.
•	Stop Voltage: 0.9 V (the maximum input gate voltage).
•	Increment: 0.05 V.
•  Add the Directive:
•	Place the command .dc V1 0 0.9 0.05 anywhere on your schematic.
•  Run the Simulation:
•	Click the “Run” icon to start the simulation and view the resulting plots.

### Results
![image](https://github.com/user-attachments/assets/1f590f89-f7ce-4d09-a0a8-a1ef9f848881)

 
We can see the transfer characteristics of the MOSFET, i.e., the plot of VGS versus drain current, ID.
The voltage at which the current starts flowing through the MOSFET is around 360 mV = 0.36 V ≈ 0.3662473 V, which is the NMOS threshold voltage (Vt) from the tsmc018.lib file.
Drain Characteristics 
To perform the DC sweep on VDS, and obtain drain characteristics, we go to the “Configure Analysis” option and choose the DC sweep tab, and input the parameters. For this analysis, set the name of 1st source to sweep = VDD, the type of sweep = Linear, start value = 0V, stop value = 1.8V, which is the maximum value of the input gate voltage, increment = 0.1V.
Place the “.dc VDD 0 1.8 0.1” directive anywhere on the schematic, and then click on the “Run” icon.

### Results
 ![image](https://github.com/user-attachments/assets/a8c45417-afeb-443d-982d-fe22baf7af17)

This plot shows us the drain characteristics at different values of VGS, from 0V – 0.9V, in steps of 0.05V. To perform this analysis, go to the DC sweep tab, and without changing the 1st source sweep parameters, i.e., VDS parameters, click on the 2nd source to sweep tab, and set name of 2nd source to sweep = VG, type of sweep = Linear, start value = 0 V, end value = 0.9 V, increment value = 0.05V. Then click “Ok”, and then click on “Run”. This will return the plot.

### Inference
Through this experiment, we analyzed the behavior of a MOSFET using different techniques, including DC analysis, transient analysis, DC sweep, and AC analysis. Our observations confirm that the MOSFET operates as a voltage-controlled current device, as variations in the gate-to-source voltage (VGS) directly influence the output current.
Additionally, we examined how the drain current (ID) is affected by the MOSFET’s width (W) and length (L) parameters. 
Lastly, we learned how to use the LTSpice simulation tool, which simplifies circuit simulation and testing while incorporating fabrication-specific process parameters through SPICE directives and library files.




