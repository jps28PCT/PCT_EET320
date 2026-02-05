# PCT EET320 Utilities
Two Python utilities for EET320/EET321 at the Pennsylvania College of Technology.</br>
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
  </br>
  `addr_assign()` is passed no values and returns nothing.</br>
  However, it creates global variables to be used by user-defined functions and methods.</br>
  The variables are:
  |VARIABLE|PURPOSE|
  |:---:|:--|
  |`oscope`|Oscilloscope|
  |`supply`|DC Power Supply|
  |`fungen`|Function / Arbitrary Waveform Generator|
  |`dmm`|Benchtop Multimeter|
  
</details>
