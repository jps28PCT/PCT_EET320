# PCT EET320 Utilities
Two Python utilities for EET320/EET321 at the Pennsylvania College of Technology.</br>
</br>
This repository is designed for use in the electronics labs in the BWD building at Penn College.</br>
It is not intended as a general-purpose device discovery tool.</br>
</br>
To use, download PCT_EET320.py to the same folder where the lab Python code is stored.</br>
At the top of the file with the other imports, include the following:
```Python
import PCT_EET320 as pct
```
This allows either function to be called with the prefix `pct.`

<details>
  <summary>Functions</summary>

  ## addr_assign()
  This function imports PyVISA and automatically opens a connection to every piece of benchtop equipment it can find.</br>
  It is able to automatically identify and assign the USB addresses to allow easier transition between lab workstations.</br>
  If PyVISA is not installed, this function will ask the user to allow PyVISA to be installed, and then it will be imported.</br>
  </br>
  `addr_assign()` is passed no values and returns nothing.</br>
  However, it creates global variables to be used by user-defined functions and methods.</br>
  These variables are used to communicate with the benchtop test equipment used in lab.</br>
  The variables are:
  |VARIABLE|PURPOSE|
  |:---:|:--|
  |`oscope`|Oscilloscope|
  |`supply`|DC Power Supply|
  |`fungen`|Function / Arbitrary Waveform Generator|
  |`dmm`|Benchtop Multimeter|
  </br>
  To use one of these variables in a function, first use the `global` keyword and declare the variables you are going to use.</br>
  Then, use the variable to make the write or query.</br>
  The variables must be first declared as globals in a user-made function or method so a local variable with the same name is not instantiated. </br>
  </br>
  
  ### Example:
```Python
import PCT_EET320 as pct
pct.addr_assign()

global supply  #declares that the global variable 'supply' is used
global dmm     #declares that the global variable 'dmm' is used

# Other code here

supply.write("CH1:VOLTage 5")             #Sets the DC power supply to 5V on channel 1
measurement = dmm.query("MEAS:VOLT:DC?")  #Measures the voltage with the multimeter and places the value in 'measurement'

```
  This shows how the addr_assign() function could be used in a linear script.
  </br>
  </br>

  ## eng_note(inputValue, numSigFigs)
  This function converts a number into engineering notation representation.</br>
  This function is intended to format data for readability on the terminal.  It will not be formatted correctly for use in a CSV file or Excel spreadsheet.</br>

  ### Inputs:
  - `inputValue` - The numerical value to convert into engineering notation representation.
    - Can be type `float`, `int` or `string`
    - If string, it must only contain numeric characters and a decimal point
  - `numSigFigs` - The number of significant figures the string will be formatted with.
    - If left blank, the string will contain the maximum number of available digits.
   
  ### Returns:
  - A string containing the formatted number and engineering notation prefix.
    - If `inputValue` is within the range of prefixes, the string will be `numSigFigs + 3` characters wide and right-justified.  If `numSigFigs` is not specified, then the string may be longer or shorter.
    - If `inputValue` is too large or too small for the range of prefixes, then the string will default to scientific notation.  The string will contain the appropriate amount of significant figures, but the length of the string will be dependent on the size of the scientific engineering exponent.

  ### Range of prefixes:
  | Symbol | Prefix | Power | | Symbol | Prefix | Power |
  | :---: | :--- | :---: | --- | :---: | :--- | :---: |
  | '`Y`' | yotta- | 10<sup>24</sup> | | '`y`' | yocto- | 10<sup>-24</sup> |
  | '`Z`' | zetta- | 10<sup>21</sup> | | '`z`' | zepto- | 10<sup>-21</sup> |
  | '`E`' | exa- | 10<sup>18</sup> | | '`a`' | atto- | 10<sup>-18</sup> |
  | '`P`' | peta- | 10<sup>15</sup> | | '`f`' | femto- | 10<sup>-15</sup> |
  | '`T`' | tera- | 10<sup>12</sup> | | '`p`' | pico- | 10<sup>-12</sup> |
  | '`G`' | giga- | 10<sup>9</sup> | | '`n`' | nano- | 10<sup>-9</sup> |
  | '`M`' | mega- | 10<sup>6</sup> | | '`u`' | micro- | 10<sup>-6</sup> |
  | '`k`' | kilo- | 10<sup>3</sup>  | | '`m`' | milli- | 10<sup>-3</sup> |
  </br>

  ### Example:
```Python
import PCT_EET320 as pct

num1 = pct.eng_note(3.1415926, 5)  # No prefix
print("num1 = " + num1)

num2 = pct.eng_note(27182818, 3)  # Prefix for positive exponent
print("num2 = " + num2)

num3 = pct.eng_note(0.0001618033988, 6)  # Prefix for negative exponent
print("num3 = " + num3)

num4 = pct.eng_note(-0.00060221415, 6)  # Negative number, same sig figs
print("num4 = " + num4)

num5 = pct.eng_note(1414213562373095048801688724209, 5)  # Out of prefix range
print("num5 = " + num5)

num6 = pct.eng_note(0.707106781187)  # No sig figs specified
print("num6 = " + num6)


```
Output:
```ASCII
num1 =  3.1416
num2 =  27.2M
num3 =  161.803u
num4 = -602.214u
num5 =  1.4142e+30 
num6 = 707.106781187m
```
This demonstrates how the output of eng_note() changes based on input parameters.


</details>
