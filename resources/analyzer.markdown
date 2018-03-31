---
layout: page
title: Analyzer
permalink: /resources/analyzer
---
![analyzer](/images/analyzer.png)

### Export
*How to export data from BrainVision Analyzer.*

There are many ways to export EEG data from BrainVision Analyzer. Here's how the Krigolson Lab does it.

First, select the Matlab transformation from the Transformations tab. You will then be asked to specify Matlab code that you wish to run - in our case, code that saves the EEG data structure (see below).

![export1](/images/export1.png)

On the next options screen, specify that you wish to export markers, and that you wish to export the data in EEGLab format.

![export2](/images/export2.png)

Finally, export data for all channels.

![export3](/images/export3.png)

### Remarkering
*How to remarker BrainVision marker files.*

BrainVision EEG recordings result in three files: a data file (.eeg), a header file (.hdr), and a marker file (.vmrk). Occasionally, it may be necessary to remarker the data by modifying the marker file. For example, we may want to remove or change a stimulus marker if an invalid response was made.

The following MATLAB code should get you started in modifying a BrainVision marker file.

```MATLAB
% Open the old marker file
filename = 'oldFile.vmrk';
fileId = fopen(filename);

% Open a new marker file for writing
newFilename = 'newFile.vmrk';
newFileId = fopen(newFilename,'w');

% Get a line from the old file
thisLine = fgets(fileId);

% Loop through each line of the old file
while ischar(thisLine)

    % If this line includes a marker, e.g. 'S  1' through 'S255'
    if ~isempty(regexp(thisLine, 'S  [1-9]|S [1-9][0-9]|S[1-2][0-9][0-9]', 'once'))

        [matchStart, matchEnd] = regexp(thisLine, 'S  [1-9]|S [1-9][0-9]|S[1-2][0-9][0-9]'); % Get start/end characters

        thisMarkerString = thisLine(matchStart + 1:matchEnd); % Get this marker's string
        thisMarker = str2double(thisMarkerString); % Convert to a number for modification

        newMarker = thisMarker; % Modify marker as needed

        newMarkerString = sprintf('S%3d',newMarker); % Make a string for new marker
        thisLine(matchStart:matchEnd) = newMarkerString; % Modify line from original marker file
    end

    % Write to new file
    fwrite(newFileId,thisLine);

    % Get next line
    thisLine = fgets(fileId);
end

% Close old and new marker files
fclose(fileId);
fclose(newFileId);
```
