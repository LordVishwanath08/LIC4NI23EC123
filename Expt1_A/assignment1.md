<u>**Introduction** </u>

The common source (CS) configuration is a popular MOSFET arrangement
used primarily in voltage and power amplifiers. In this setup, a small
AC signal is applied to the gate, which, thanks to its high input
resistance, preserves the circuit’s predetermined DC bias point
necessary for amplification. The amplified output is then derived from
the drain. Essentially, the CS amplifier operates as a transconductance
device, meaning that a voltage input is converted into a corresponding
current output.

In this experiment, we simulated a CS amplifier without a source
resistance (Rₛ) and conducted a range of analyses using LTSpice, a
circuit simulation tool. We set the parameters for our N-channel MOSFET
using the TSMC 180 nm SPICE library file. For this particular
configuration, the circuit was designed within a power budget of 50 μW,
with a supply voltage of 1.8 V and a drain resistance (R_D) of 1 kΩ and
V_G as 0.6V

The components we require are

<img src="./media/1.png"
style="width:5.42708in;height:2.69792in" />

1.  N-channel Enhancement MOSFET (CMOSN)

2.  DC Supply Voltage - 1.8V (V<sub>DD</sub>)

3.  Resistor - 1kΩ

4.  Power Supply - 0.9V DC

**<u>Procedure</u>**

1.  We are supposed to rig up the circuit in the tool window and measure
    the DC Q-point, according to the requirements we have been given.

2.  Make sure to save the TSMC 180 nm SPICE netlist, or .lib file in the
    folder where you have saved LTSpice on your system.

3.  Open the LTSpice simulation tool, and click on the IC symbol, which
    contains the the list of components available. From the list, select
    **nmos4** which is a 4 terminal NMOS, After placing the NMOS, place
    the rest of the required components, assemble the circuit as per the
    given circuit diagram. The body terminal must be connected to the
    lowest potential, i.e., ground while the drain connected to Rd
    followed by a voltage source with a voltage of 1.8V and gate
    terminal connected to the voltage source of voltage 0.9V.

4.  Select the .t symbol on the toolbar. This lets you add a SPICE
    directive, which will allow you to specify the process technology
    and the parameters for the MOSFET. In this case, we will be using
    the **TSMC 180 nm**

5.  Next, using the .t tool, give the directive, **.lib tsmc018.lib**,
    and click ‘OK’. Then place this command anywhere in the schematic.

6.  After this, we can perform various analyses - DC, AC, transient, DC
    operating point, etc.

> <img src="./media/2.png" style="width:3.875in;height:3.22917in" />

**<u>DC Operating Point</u>**

Given that power budget = 50 𝜇W, we use P = V<sub>DD</sub>.
I<sub>D</sub>, to calculate I<sub>D</sub>, given that supply voltage
V<sub>DD</sub> = 1.8V.

50 𝜇W = (1.8) x I<sub>D</sub>, which gives us **I<sub>D</sub> = 27.778
𝜇A**.

Now that we have the value of I<sub>D</sub>, we can calculate
V<sub>D</sub>.

Applying KVL in the drain portion of the circuit - 

V<sub>D</sub> = V<sub>DD</sub> - I<sub>D</sub>R<sub>D</sub> — (1)

Substituting the values, we get - 

V<sub>D</sub> = 1. 8- (27.775𝜇A x 1kΩ) = **1.7722V**

Now, we can check whether the MOSFET is in the saturation region, and
ensure that it provides ideal amplification.

We know for saturation, V<sub>GD</sub> \< V<sub>t</sub>.

**V<sub>t</sub> = 0.3662 V** (From tsmc018.lib file)

V<sub>GD</sub> = 0.9 - 1.7722 = **-0.8722 V**

∴ Since V<sub>GD</sub> \< V<sub>t</sub>, we can say that the MOSFET is
operating in the saturation region.

∴ The operating point of this MOSFET is – (1.7722 V, 27.778 𝜇A), with
V<sub>GS</sub> = 0.9 V.

To perform this analysis, we go to the Run icon on the LTSpice toolbar,
or use the Alt + R shortcut. After that, click on the DC operating point
tab. Then click ‘OK’, and place the .op file anywhere on the schematic.

This will open a window of all the node voltages, branch currents and
resistances in your schematic

**<u>Results</u>**

<img src="./media/3.png"
style="width:3.79167in;height:2.30208in" />

From this, we can see V<sub>D</sub> = **1.77223V,** I<sub>D</sub> **=
27.77668 𝜇A**. These closely match our calculated values.

**<u>Transient Analysis</u>**

We will now conduct a transient simulation in LTSpice to observe how the
output voltage (VD) evolves over time. Since we are dealing with a
time-dependent signal, an AC excitation is required.

1.  **Setting up the AC Source:**

    - Locate the gate voltage source, VG, in your schematic.

    - Right-click on VG to open its configuration dialog.

    - Select the “Advanced” option and then choose “SINE” to specify
      that the input will be a sine wave.

2.  **Configuring the Sine Wave Parameters:**

    - **DC Offset:** Set to 0.9 V. This value ensures that the DC
      operating point remains unaffected.

    - **Amplitude:** Set to 50 mV, which keeps the signal within the
      small-signal regime (i.e., ensuring Vgs is much less than 2VOV).

    - **Frequency:** Set to 1 kHz.

3.  **Running the Transient Analysis:**

    - Open the “Configure Analysis” window by clicking the Run

    - Switch to the Transient tab and set the stop time to 5 ms.

    - Finally, insert the command .tran 5m anywhere on your schematic
      and execute the simulation.

**<u>Results</u>**

<img src="./media/4.png" style="width:5.27986in;height:4.1125in" />

From the waveform, we can see that the peak voltage of the output signal
is around 1.777 V. We can also see that the waveform is inverted
compared to the input. This indicates a 180° phase shift, which results
in a negative gain.

Since we know the amplitude of the input voltage, V<sub>in</sub>, and
approximated amplitude of the output voltage, V<sub>out</sub>, we can
calculate small signal gain.

**A<sub>v</sub> = -( V<sub>out</sub>/ V<sub>in</sub>) = -(1.772/50m) =
-33.54**

**<u>AC Analysis</u>**

 **Accessing the AC Analysis Settings:**

- Click the Run icon and select “Configure Analysis.”

- Navigate to the AC analysis tab.

 **Setting Up the Sweep Parameters:**

- **Sweep Type:** Choose “Decade” to generate a logarithmic sweep,
  ensuring the gain is represented in dB per decade.

- **Points per Decade:** Set this to 20 to obtain a detailed plot.

- **Frequency Range:** Specify a start frequency of 0.1 Hz and an end
  frequency of 1 THz, covering a broad spectrum.

 **Final Steps:**

- Place the directive .ac dec 20 0.1 1T anywhere on your schematic.

- Run the simulation to generate the Bode plot.

**<u>Results</u>**

<img src="./media/5.png" style="width:6.26806in;height:1.1699in" />

From the plot, we can see that the midband gain is around -22 dB, for an
input ac sine signal, of amplitude 50 mV. The gain is negative due to a
180° phase shift, which inverts the output compared to the input. We can
also see that the phase shift is approximately between 160° - 180°, but
closer to 180°, which explains the reason for the negative gain and the
inverted output.

Converting our gain from V/V to dB, using the formula A’<sub>V</sub> =
-10log<sub>10</sub>(A<sub>v</sub>)

A’<sub>V</sub> = -10log<sub>10</sub>(35.54) = -10(1.5507) = -15.507

∴ **A’<sub>V</sub> = -15.507**, which matches with the gain value from
the Bode plot.

We can also see that the gain begins falling at around 1 GHz, which we
can assume to be the f<sub>H</sub> value.

**<u>DC Sweep</u>**

**<u>Transfer Characteristics</u>**

 **Open the Analysis Configuration:**

- Click on the “Configure Analysis” button in LTSpice.

 **Select the DC Sweep Option:**

- Choose the DC sweep tab within the configuration window.

 **Input the Sweep Parameters:**

- **Source to Sweep:** Set this to VG (the gate voltage).

- **Sweep Type:** Choose a linear sweep.

- **Start Voltage:** 0 V.

- **Stop Voltage:** 0.9 V (the maximum input gate voltage).

- **Increment:** 0.05 V.

 **Add the Directive:**

- Place the command .dc VG 0 0.9 0.05 anywhere on your schematic.

 **Run the Simulation:**

- Click the “Run” icon to start the simulation and view the resulting
  plots.

**<u>Results</u>**

<img src="./media/6.png"
style="width:6.26806in;height:1.34602in" />

We can see the transfer characteristics of the MOSFET, i.e., the plot of
V<sub>GS</sub> versus drain current, I<sub>D</sub>.

The voltage at which the current starts flowing through the MOSFET is
around 360 mV = 0.36 V ≈ 0.3662473 V, which is the NMOS threshold
voltage (V<sub>t</sub>) from the tsmc018.lib file.

**<u>Drain Characteristics</u>**

To perform the DC sweep on V<sub>DS</sub>, and obtain drain
characteristics, we go to the “Configure Analysis” option and choose the
DC sweep tab, and input the parameters. For this analysis, set the name
of 1<sup>st</sup> source to sweep = V<sub>DD</sub>, the type of sweep =
Linear, start value = 0V, stop value = 1.8V, which is the maximum value
of the input gate voltage, increment = 0.1V.

Place the **“.dc VDD 0 1.8 0.1”** directive anywhere on the schematic,
and then click on the “Run” icon.

**<u>Results</u>**

<img src="./media/7.png"
style="width:6.26806in;height:1.25361in" />

From this plot, we can see that the MOSFET is in triode from 0 V until
somewhere between 0.4V – 0.6V. At a little more than 0.6V, the MOSFET
goes into saturation, and the drain current I<sub>D</sub>, becomes a
constant. The I<sub>D</sub> value (in saturation) is around 27 µA, which
matches approximately with our calculated value of 27.778 µA.

<img src="./media/8.png"
style="width:6.26806in;height:1.94069in" />

This plot shows us the drain characteristics at different values of
V<sub>GS</sub>, from 0V – 0.9V, in steps of 0.05V. To perform this
analysis, go to the DC sweep tab, and without changing the
1<sup>st</sup> source sweep parameters, i.e., V<sub>DS</sub> parameters,
click on the 2<sup>nd</sup> source to sweep tab, and set name of
2<sup>nd</sup> source to sweep = V<sub>G</sub>, type of sweep = Linear,
start value = 0 V, end value = 0.9 V, increment value = 0.05V. Then
click “Ok”, and then click on “Run”. This will return the plot.

**<u>Voltage Transfer Characteristic</u>**

<img src="./media/9.png"
style="width:3.16601in;height:2.77369in" />

**<u>Variation of Parameters</u>**

1.  **Variation of I<sub>D</sub> with varying values of R<sub>D</sub>
    (10Ω – 1kΩ, with increments of 50Ω) –**

> We can use LTSpice to measure values of I<sub>D</sub>, while varying
> R<sub>D</sub>, and simultaneously perform DC sweep, transient
> analysis, and AC analysis. We can do this by using the SPICE directive
> or clicking the .t icon.
>
> Next right click on the resistor R<sub>1</sub>, and change the value
> of the resistor from 1kΩ to {R}. This changes the value of the
> resistor to a parameter, which can be varied between values.
>
> Then, using the SPICE directive, type **“.step param R 10 1k 50”**,
> which tells LTSpice to vary R from 10Ω to 1kΩ, in steps of 50Ω.

<img src="./media/10.png" style="width:5.11458in;height:2.625in" />

2.  **Variation of I<sub>D</sub> with varying values of W (0.5µm –
    1.5µm, with increments of 0.5µm)-**

> We can use LTSpice to measure values of I<sub>D</sub>, while varying
> W, and simultaneously perform DC sweep, transient analysis, and AC
> analysis. We can do this by using the SPICE directive or clicking the
> .t icon.
>
> Next right click on the MOSFET M1, and change the value of W from
> 690nm to {w}. This changes the value of the width to a parameter,
> which can be varied between values.
>
> Then, using the SPICE directive, type **“.step param w 0.5u 1.5u
> 0.5u”**, which tells LTSpice to vary W from 0.5 µm to 1.5 µm in steps
> of 0.5 µm.
>
> <img src="./media/11.png"
> style="width:6.26806in;height:1.99694in" />

3.  **Variation of I<sub>D</sub> with varying values of L (50 nm – 200
    nm, with increments of 10 nm)-**

> We can use LTSpice to measure values of I<sub>D</sub>, while varying
> L, and simultaneously perform DC sweep, transient analysis, and AC
> analysis. We can do this by using the SPICE directive or clicking the
> .t icon.
>
> Next right-click on the MOSFET M1, and change the value of the length
> from 700 nm to {l}. This changes the value of the length to a
> parameter, which can be varied between values.
>
> Then, using the SPICE directive, type **“.step param l 50n 180n
> 25n”**, which tells LTSpice to vary L from 50 nm to 200 nm, in steps
> of 25 nm.
>
> <img src="./media/12.png"
> style="width:6.26806in;height:1.34536in" />

**<u>Final Results</u>**

- Drain Current, I<sub>D</sub> = 27.7668 µA

- Drain-to-source voltage, V<sub>DS</sub> = 1.7723 V

- Gain (V/V) = -35.54 V/V

- Gain (dB) = -15.507 dB

**<u>Inference</u>**

In this experiment, we explored the MOSFET’s behavior using a variety of
simulation techniques—including DC analysis, transient response, DC
sweeps, and AC analysis. Our observations confirmed that the MOSFET
operates as a voltage-controlled current source: adjusting the
gate-to-source voltage (VGS) directly influenced the output current.

During the AC analysis, we noted that the device amplified a 50 mV input
signal up to 1.77 V, which corresponds to a gain of approximately
–35.54. This large negative gain indicates a near 180° phase shift,
meaning the output signal is inverted relative to the input. In decibel
terms, the gain was around –15 dB.

We also investigated how changes in the MOSFET’s physical dimensions
(the width, W, and length, L) and the drain resistor (RD) affected the
drain current (ID). Finally, we gained hands-on experience with LTSpice,
a simulation tool that simplifies circuit analysis by incorporating
realistic process parameters through SPICE directives and library files.
