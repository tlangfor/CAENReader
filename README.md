# CAENReader
_A set of tools to read and process binary data produced by CAEN waveform digitizers._

## Introduction

The binary format produced by CAEN digitizers (via WaveDump or similar DAQ software packages) is an efficient way of storing data. We have produced two classes, DataFile and RawTrigger, that parse the raw binary data, extract information from the event header, and return the recorded traces in numpy arrays. These can then be analyzed by the end user.

## Contents

### Class: DataFile

This class is the connection to the raw binary data. The main method is getNextTrigger, which parses one trigger from the data file and returns a RawTrigger object. 

### Class: RawTrigger

This class is a container of the information stored in one trigger: 

- Trigger Time Tag
- Time of event since beginning of the file (in microseconds)
- Event Counter
- File position
- Dictionary of the traces 

There is one method, display, that uses matplotlib to plot the traces. The event information is displayed in the legend.
