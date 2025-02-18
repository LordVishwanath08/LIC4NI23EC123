**[Task -- 2]{.underline}**

We are supposed to replace the R_D with the pmos4 and do the all the
analysis, DC, AC, Transient

**[Procedure]{.underline}**

1.  We are supposed to rig up the circuit in the tool window and measure
    the DC Q-point, according to the requirements we have been given.

2.  Make sure to save the TSMC 180 nm SPICE netlist, or .lib file in the
    folder where you have saved LTSpice on your system.

3.  Open the LTSpice simulation tool, and click on the IC symbol, which
    contains the the list of components available. From the list, select
    **nmos4 and pmos4** which is a 4 terminal NMOS and PMOS, After
    placing the NMOS and PMOS, place the rest of the required
    components, assemble the circuit as per the given circuit diagram.

4.  Select the .t symbol on the toolbar. This lets you add a SPICE
    directive, which will allow you to specify the process technology
    and the parameters for the MOSFET. In this case, we will be using
    the **TSMC 180 nm**

5.  Next, using the .t tool, give the directive, **.lib tsmc018.lib**,
    and click 'OK'. Then place this command anywhere in the schematic.

6.  After this, we can perform various analyses - DC, AC, transient, DC
    operating point, etc.

**[DC Operating Point]{.underline}**

Given that power budget = 50 𝜇W, we use P = V~DD~. I~D~, to calculate
I~D~, given that supply voltage V~DD~ = 1.8V.

50 𝜇W = (1.8) x I~D~, which gives us **I~D~ = 27.778 𝜇A**.

To perform this analysis, we go to the Run icon on the LTSpice toolbar,
or use the Alt + R shortcut. After that, click on the DC operating point
tab. Then click 'OK', and place the .op file anywhere on the schematic.

This will open a window of all the node voltages, branch currents and
resistances in your schematic

**[Results]{.underline}**

![](media/1.jpg){width="6.268055555555556in"
height="3.652083333333333in"}

**[Transient Analysis]{.underline}**

We will now conduct a transient simulation in LTSpice to observe how the
output voltage (VD) evolves over time. Since we are dealing with a
time-dependent signal, an AC excitation is required.

1.  **Setting up the AC Source:**

    - Locate the gate voltage source, VG, in your schematic.

    - Right-click on VG to open its configuration dialog.

    - Select the "Advanced" option and then choose "SINE" to specify
      that the input will be a sine wave.

2.  **Configuring the Sine Wave Parameters:**

    - **DC Offset:** Set to 0.9 V. This value ensures that the DC
      operating point remains unaffected.

    - **Amplitude:** Set to 50 mV, which keeps the signal within the
      small-signal regime (i.e., ensuring Vgs is much less than 2VOV).

    - **Frequency:** Set to 1 kHz.

3.  **Running the Transient Analysis:**

    - Open the "Configure Analysis" window by clicking the Run

    - Switch to the Transient tab and set the stop time to 5 ms.

    - Finally, insert the command .tran 5m anywhere on your schematic
      and execute the simulation.

**[Results]{.underline}**

![](media/2.jpg){width="6.268055555555556in"
height="1.3132108486439196in"}

We can see that the waveform is inverted compared to the input. This
indicates a 180° phase shift, which results in a negative gain.

Since we know the amplitude of the input voltage, V~in~, and
approximated amplitude of the output voltage, V~out~, we can calculate
small signal gain.

**A~v~ = -( V~out~/ V~in~) = -(1.52/50m) = -30.4**

**[AC Analysis]{.underline}**

 **Accessing the AC Analysis Settings:**

- Click the Run icon and select "Configure Analysis."

- Navigate to the AC analysis tab.

 **Setting Up the Sweep Parameters:**

- **Sweep Type:** Choose "Decade" to generate a logarithmic sweep,
  ensuring the gain is represented in dB per decade.

- **Points per Decade:** Set this to 20 to obtain a detailed plot.

- **Frequency Range:** Specify a start frequency of 0.1 Hz and an end
  frequency of 1 THz, covering a broad spectrum.

 **Final Steps:**

- Place the directive .ac dec 20 0.1 1T anywhere on your schematic.

- Run the simulation to generate the Bode plot.

**[Results]{.underline}**

![](media/3.jpg){width="6.268055555555556in"
height="1.3654451006124235in"}

From the plot, we can see that the midband gain is around -18.5 dB, for
an input ac sine signal, of amplitude 50 mV. The gain is negative due to
a 180° phase shift, which inverts the output compared to the input. We
can also see that the phase shift is approximately between 160° - 180°,
but closer to 180°, which explains the reason for the negative gain and
the inverted output.

Converting our gain from V/V to dB, using the formula A'~V~ =
-10log~10~(A~v~)

A'~V~ = -20log~10~(30.4) = -20(1.4828) = -29.656

∴ **A'~V~ = -29.656**, which matches with the gain value from the Bode
plot.

We can also see that the gain begins falling at around 1 GHz, which we
can assume to be the f~H~ value.

**[DC Sweep]{.underline}**

**[Transfer Characteristics]{.underline}**

 **Open the Analysis Configuration:**

- Click on the "Configure Analysis" button in LTSpice.

 **Select the DC Sweep Option:**

- Choose the DC sweep tab within the configuration window.

 **Input the Sweep Parameters:**

- **Source to Sweep:** Set this to VG (the gate voltage).

- **Sweep Type:** Choose a linear sweep.

- **Start Voltage:** 0 V.

- **Stop Voltage:** 0.9 V (the maximum input gate voltage).

- **Increment:** 0.05 V.

 **Add the Directive:**

- Place the command .dc V1 0 0.9 0.05 anywhere on your schematic.

 **Run the Simulation:**

- Click the "Run" icon to start the simulation and view the resulting
  plots.

**[Results]{.underline}**

![](media/4.jpg){width="6.268055555555556in"
height="1.176599956255468in"}

We can see the transfer characteristics of the MOSFET, i.e., the plot of
V~GS~ versus drain current, I~D~.

The voltage at which the current starts flowing through the MOSFET is
around 360 mV = 0.36 V ≈ 0.3662473 V, which is the NMOS threshold
voltage (V~t~) from the tsmc018.lib file.

**[Drain Characteristics]{.underline}**

To perform the DC sweep on V~DS~, and obtain drain characteristics, we
go to the "Configure Analysis" option and choose the DC sweep tab, and
input the parameters. For this analysis, set the name of 1^st^ source to
sweep = V~DD~, the type of sweep = Linear, start value = 0V, stop value
= 1.8V, which is the maximum value of the input gate voltage, increment
= 0.1V.

Place the **".dc VDD 0 1.8 0.1"** directive anywhere on the schematic,
and then click on the "Run" icon.

**[Results]{.underline}**

![](media/5.jpg){width="6.268055555555556in"
height="1.340667104111986in"}

This plot shows us the drain characteristics at different values of
V~GS~, from 0V -- 0.9V, in steps of 0.05V. To perform this analysis, go
to the DC sweep tab, and without changing the 1^st^ source sweep
parameters, i.e., V~DS~ parameters, click on the 2^nd^ source to sweep
tab, and set name of 2^nd^ source to sweep = V~G~, type of sweep =
Linear, start value = 0 V, end value = 0.9 V, increment value = 0.05V.
Then click "Ok", and then click on "Run". This will return the plot.

**[Inference]{.underline}**

Through this experiment, we analyzed the behavior of a MOSFET using
different techniques, including DC analysis, transient analysis, DC
sweep, and AC analysis. Our observations confirm that the MOSFET
operates as a voltage-controlled current device, as variations in the
gate-to-source voltage (VGS) directly influence the output current.

Additionally, we examined how the drain current (ID) is affected by the
MOSFET's width (W) and length (L) parameters.

Lastly, we learned how to use the LTSpice simulation tool, which
simplifies circuit simulation and testing while incorporating
fabrication-specific process parameters through SPICE directives and
library files.
