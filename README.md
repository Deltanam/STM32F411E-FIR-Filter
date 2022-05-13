# STM3232F4-FIR-Filter

This code was created for the STM32F411E DISCO board. The goal was to create a FIR digital low-pass filter that could filter out a contaminated signal. This contaminated signal would be downloaded directly onto the board at address 0x8020000.

There are multiple different ProcessSample#() functions available in the code. Changing to another ProcessSample() function requires modifying the code directly.
ProcessSample() is the original implementation of the FIR filter, with the convolution being executed once every loop.
ProcessSampleNew() executes loop unrolling by a factor of 10 while implementing the same logic as ProcessSample().
ProcessSample2() uses the MAC command SMLABB to simultaneously add and accumulate tap/input values for each execution of the loop.
ProcessSample3() uses the SIMD intrinsic SMLAD to simultaneously add and accumulate 2 tap/input values each loop execution.
ProcessSample4() utilizes a circular buffer, completely removing the need to shift input values and removing the second loop in the first several ProcessSample#() functions.
