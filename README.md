# PCT EET320 Utilities
Two Python utilities for EET320/EET321 at the Pennsylvania College of Technology.</br>
</br>
This repository is designed for use in the electronics labs in the BWD building at Penn College.</br>
It is not intended as a general-purpose device discovery tool.
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
  It is able to automatically identitify and assign the USB addresses to allow easier transition between lab workstations.</br>
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
  The variables must be first declared as globals in a user-made function or method so a local variable with the same name is not instantiated. </br>



  ## eng_note(Value, short)
  This function converts a number into scientific notation representation.</br>

  ### Inputs:
  - `Value` - The numerical value to convert into engineering notation representation.
    - Can be type `float`, `int` or `string`
    - If string, it must only contain numeric characters and a decimal point
  - `short` - Boolean variable to determine whether to return 'short' or 'long' engineering notation representation
    - `True` will make the output string contain a maximum of 5 digits
    - `False` will make the output string contain a maximum of 6 digits after the decimal, and up to 3 digits before the decimal.  This is the default.
</details>
