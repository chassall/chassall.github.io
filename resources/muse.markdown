---
layout: page
title: Muse
permalink: /resources/muse
---
![muse](/images/muse.jpg)

The Muse, by Interaxon, is a portable and inexpensive EEG headset. Although it was designed as a tool for meditation training, it has been validated for research in cognitive psychology [(Krigolson et al., 2017)](https://www.frontiersin.org/articles/10.3389/fnins.2017.00109/full).

[How to Connect (2014 Muse, OSX)](/resources/connectingthemuse.pdf)

### Markers
*How to use MATLAB to send markers to a MuseLab recording.*

One method for collecting Muse data during an experiment is to read directly from the device as needed using [muse-io](http://developer.choosemuse.com/tools/museio) and [OSC](http://opensoundcontrol.org/introduction-osc) (e.g., following the presentation of a visual stimulus). This method is described in detail [here](http://www.neuroeconlab.com/muse-data-collection.html).

A second method is to send markers to a [MuseLab EEG](http://developer.choosemuse.com/tools/mac-tools/muselab) recording. This method currently has the following requirements:

* [Muse Research Tools](http://developer.choosemuse.com/) (includes MuseLab, muse-io, and muse-player)

* 2014 (MU-01) Muse

* [MATLAB](https://www.mathworks.com/products/matlab.html)

* [Instrument Control Toolbox](https://www.mathworks.com/products/instrument.html)

* [oscsend.m](https://github.com/stefanofasciani/TSM4VSTS/blob/master/MATLAB/oscsend.m)

The main advantage of this method is that it will work in macOS, Windows, and Linux. The main disadvantage is that it requires the Instrument Control Toolbox to send UDP messages (though other solutions may be possible).

First, connect the Muse by running muse-io with the following command:

    muse-io --no-dsp --preset AD --osc osc.udp://localhost:5555 --device Muse-XXXX

*-\-no-dsp -\-preset AD* turns off signal processing

*-\-osc osc.udp://localhost:5555* forwards incoming data to local port 5555 (UDP protocol, OSC message format)

*-\-device Muse-XXXX* specifies the device name (where XXXX is the name of your Muse)

Next, have MuseLab listen to port 5555 using the UDP protocol. Start/stop recordings as needed ([instructions](http://dev.choosemuse.com/tools/getting-started)).

In MATLAB, open a UDP connection to the same port:

```MATLAB
u = udp('localhost',5555); % specify the UDP address that markers will be sent to
fopen(u); % open the UDP connection
```

To send a marker, simply send it as an OSC message. Note that MuseLab will record all OSC messages that it receives, however there is an advantage to formatting the message in a Muse-friendly way. Eventually you may want to convert your Muse recording using  muse-player, for example to a MATLAB or CSV (comma-separated value) file. All OSC messages that are received by MuseLab seem to show up if you convert the .muse file to a .csv file (if that is your plan, use any header you like, e.g. /mylab/marker).

However, only messages with certain formatting seem to be included in the converted .mat file. The following works, and your markers and timestamps will show up in the .mat file under "elements".

```MATLAB
oscsend(u,'/muse/elements/marker','i',1); % Send marker 1 on UDP connection u
```

Finally, close the connection at the end of your script.

```MATLAB
fclose(u); % close the UDP connection
```
