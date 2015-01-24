# Power Supply - LM317 Adjustable Regulator

Demonstrates the LM317 voltage regulator, using and Arduino to measure the voltage supply and plot the results with [Processing](https://www.processing.org).

## Notes

The LM317 can be used to provide an adjustable voltage or current supply.

The circuit described here is a adjustable voltage supply. When used in this mode, the voltage depends on the values of R1 and R2:

    Vout = 1.25 * ( 1 + R2/R1 )

Check the [datasheet](http://www.futurlec.com/Linear/LM317T.shtml) to verify the formula for your specific chip.
In a circuit, R2 could be fixed to provide a fixed voltage, or it can be a variable resistor to allow manipulation of the voltage.
R2 could also be replaced by a sensor to convert sensor resistance to voltage.

### Baseline Test

Using known resistances, the measured value Vout is pretty close to spec for the chip I am using:

| R1   | R2    | Vout | Derivation
| -----|-------|-------|---------------
| 220R | 1k    |  6.93 | theoretical
| 222R | 998R  |  6.87 | theoretical, with actual resistances as measure with DMM
| 222R | 998R  |  6.86 | actual (DMM)
| 222R | 998R  |  6.85 | actual (Arduino)

### Using a Pot

The circuit described in the build replaces the 1k R2 used in the reference circuit
with a smaller 220R R2 and 50k R3 potentiometer, which allows a
Vout ranging from 2.49V to the maximum supply possible (about 1.25V less than the input supply).


Here's a sample trace with the pot being adjusted:

![processing trace](./assets/processing_trace.png?raw=true)

### Construction

The Arduino only acts as a measurement device in this circuit.
Analog pin is used to read Vout via a voltage divider (Rd1/Rd2). The voltage divider is to ensure that the Arduino never sees more than half the battery voltage (4.5V) on the analog pin.

[PlotNValues (a simple Processing sketch)](../../processing/PlotNValues) reads the data from the serial port and plots the input and output value over time, with some coloration effects thrown in for good measure. In other words, we're using Arduino and Processing as a basic oscilloscope! And it kind of works, mainly because the frequency is so low.

![The Breadboard](./assets/Power317_bb.jpg?raw=true)

![The Schematic](./assets/Power317_schematic.jpg?raw=true)

Here's the breadboard with the variable R2, note a little more spread out than my original Fritzing diagram:
![The Build](./assets/Power317_build_var.jpg?raw=true)

Here's the reference measurement with fixed/known R1 and R2 values:
![The Build](./assets/Power317_build_ref.jpg?raw=true)

## Credits and References
* [LM317 datasheet](http://www.futurlec.com/Linear/LM317T.shtml)
* [LM317 Voltage Calculator](http://www.reuk.co.uk/LM317-Voltage-Calculator.htm)
* [Download Processing](https://www.processing.org/download/)