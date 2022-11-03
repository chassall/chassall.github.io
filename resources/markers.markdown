---
layout: page
title: Markers
permalink: "/resources/markers"

---
![markers](/images/markers.jpg)

An event-related potential (ERP) is the average scalp voltage in response to an external event, such as the appearance of visual feedback. One way to construct an ERP is to mark the continuous electroencephalogram (EEG), then compute averages based on marker position. Thus, the timing of marker placement within the continuous EEG stream is critical.

Many EEG systems require that numerical markers be sent via a parallel port, which modern PCs are unlikely to include. It is possible to install a parallel port in a PC with a spare PCI-Express slot. This method will also require locating the appropriate driver for your operating system, and may require the use of special libraries for your experimental program.

The timing of several options for sending a marker via parallel cable are shown below. An experiment-presentation computer ("stim machine") running Ubuntu 17.04 was used to control each device. In particular, a test program was run in Matlab (R2015a) using the Psychophysics Toolbox ("Psychtoolbox"). On each trial of the test program, a display image switched from black to white. The output of a photoelectrode attached to the top left corner of the display (22" LCD, 75 Hz) was recorded using an auxiliary channel of a BrainVision actiCHamp EEG system. For each trial (100 trials in total) a marker was sent, either before or after the Psychtoolbox command to draw to the display.

### USB to Serial/Parallel Adapter Cable

![usbtoserial](/images/usbtoserial.jpg)

Manufacturer: Startech

Cost: Low Delay: 5.1 ms (SD = 4.2 ms)

### Stimtracker

![stimtracker](/images/stimtracker.png)

Cedrus

Cost: Medium Delay: 4.9 ms (SD = 3.9 ms)

### DATAPixx2

![datapixx2](/images/datapixx2.png)

VPixx

Delay (USB to parallel): 5.9 ms (SD = 3.9 ms) 

Delay (video sync): 2.8 ms (SD = 0.6 ms)