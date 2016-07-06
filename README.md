# CAENReader
_A set of tools to read and process binary data produced by CAEN waveform digitizers._

## Introduction

The binary format produced by CAEN digitizers (via WaveDump or similar DAQ software packages) is an efficient way of storing data. We have produced two classes, DataFile and RawTrigger, that parse the raw binary data, extract information from the event header, and return the recorded traces in numpy arrays. These can then be analyzed by the end user.

## Contents

### `DataFile`

This class is the connection to the raw binary data. 

The `getNextTrigger` method is designed to be flexible and extract all information from the event header along with unpacking the traces into numpy arrays. 

#### Zero Suppression and ZLE

CAEN provides two methods of suppressing extraneous information from being read out from the digitizers, Zero Suppression and Zero-length encoding (ZLE). 

- Zero Suppression: suppressing empty channels from being read out entirely
- Zero-length encoding: only read out "interesting" parts of the acquisition window 

These are documented in various digitizer manuals. Note, these features are not available for all models. 

### `RawTrigger`

This class is a container of the information stored in one trigger: 

- Trigger Time Tag (clock ticks from event header)
- Time of event since beginning of the file (in microseconds)
- Event Counter (from event header)
- File position
- Dictionary of the traces 

There is one method, `display`, that uses matplotlib to plot the traces. The event information is displayed in the legend.


## Usage
The most basic usage of this code is to extract a trigger from a binary file `waves.dat` and display the trigger using the `trigger.display()` method:

    dataFile = CAENReader.DataFile('waves.dat')
    trigger = dataFile.getNextTrigger()
    trigger.display()
    
This will produce a plot of every trace included in this trigger. If zero suppression is being used, empty traces will not be plotted. For traces with ZLE, the "interesting" parts of the traces are plotted in their correct position.   
