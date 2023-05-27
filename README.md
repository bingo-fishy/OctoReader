# OctoReader
OctoReader is a utility designed by Nicholas Li in MATLAB to read data through a computer’s serial port and graph and process it in real-time. It was designed using MATLAB App Designer, MATLAB version 2021b.

Example usage:
1. Start program
2. Begin recording
3. Set number of inputs to 8
4. Send 'g'
5. Use the program to monitor data
6. Send 's'
7. Export data

Input Data format:
255   255   255   uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8 uint8

255 255 25_ - Command. The final value may change to indicate different information being sent to OctoReader. Reserve [255 255 255], [255 255 254], etc. for possible commands and do NOT use for data.

uint8t (24x) - 8x 24-bit unsigned integers, sent in Little Endian format (LSB -> MSB). They are in order of graph 1 to graph 8. 

NOTE: Due to the “binning” process used to increase the processing speed, a command is not checked for every time data is read. Therefore, the serial device must repeat the command until it receives an OK sent back from OctoReader (this does not apply to inputting data, but does apply to every other command that may be used).

Filtering:
Data is processed as an array with arbitrary time values, where filtering limits are “expressed in normalized units of π rad/sample” (MATLAB documentation). A value greater than 0 and less than 1 should be chosen for the low-pass and high-pass thresholds, where 1 represents higher frequencies and 0 represents lower frequencies. The “Steepness” parameter dictates how sharp the frequency cutoff is.

NOTE: For Band-Pass filtering, the Low-Pass threshold must be greater than the High-Pass threshold value.

NOTE: The precision of the power spectrum feature increases with sample rate. Consider temporarily increasing the program’s if increased precision is needed

Known Issues:
If the serial buffer fills up, graphs will not be updated until all of the data in the buffer is read. This can happen if the program is stopped for some reason, or if data is being sent too fast to process. If the serial buffer fills up for a long period of time, it may be easiest to end the program by disconnecting the serial device or force quitting.

Update Log:
4/26/23 - Added power spectrum and minor UX improvements.
5/27/23 - Bug fixes, improved power spectrum and power spectrum view, included filters in graph exports, added legend to graph exports

