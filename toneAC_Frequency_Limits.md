# toneAC Frequency Limits #

The table below are theoretical limits. Due to overhead and your sketch probably doing something else, the maximum frequency will be lower. For the highest frequency possible when calling toneAC, specify only the frequency parameter, for example:

`toneAC(frequency);`

This will play the specified frequency till you terminate it with toneAC();

| **Arduino CPU speed** | **Minimum Frequency** | **Maximum Frequency** |
|:----------------------|:----------------------|:----------------------|
|16 Mhz                 |1 Hz                   |2.66 MHz               |
|8 Mhz                  |1 Hz                   |1.33 MHz               |
|4 Mhz                  |1 Hz                   |666.66 kHz             |
|2 Mhz                  |1 Hz                   |333.33 kHz             |
|1 Mhz                  |1 Hz                   |166.66 kHz             |