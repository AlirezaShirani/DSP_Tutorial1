# 🎥 Extract Frames from an MP4 Video Using MATLAB

This script allows you to:

- Select an `.mp4` video file using a dialog box
- Read the video using `VideoReader`
- Save each video frame as an image (`.jpg`) in a new folder
- Automatically add the video’s folder to the MATLAB path

---

## 📌 MATLAB Code

```matlab
%***********************************************************************%
%********** Select, Read, and Save Frames from an .mp4 Video **********%
%***********************************************************************%

clc;
clear;
close all;

% Step 1: Open file selection dialog to choose the .mp4 video
[filename, filepath] = uigetfile({'*.mp4'}, 'Select an MP4 Video File');
if isequal(filename, 0)
    disp('User canceled file selection.');
    return;
end

% Step 2: Add selected file's folder to MATLAB path (optional, for re-use)
addpath(filepath);

% Step 3: Create VideoReader object
fullVideoPath = fullfile(filepath, filename);
vidObj = VideoReader(fullVideoPath);

% Step 4: Create output folder for extracted frames (in same location)
[~, nameOnly, ~] = fileparts(filename);
outputFolder = fullfile(filepath, [nameOnly '_frames']);
if ~exist(outputFolder, 'dir')
    mkdir(outputFolder);
end

% Step 5: Extract and save each frame as an image
frameCount = 0;
while hasFrame(vidObj)
    frame = readFrame(vidObj);         % Read one frame
    frameCount = frameCount + 1;
    
    % Create filename like frame_001.jpg
    imageName = sprintf('frame_%03d.jpg', frameCount);
    fullImagePath = fullfile(outputFolder, imageName);
    
    % Save the frame
    imwrite(frame, fullImagePath);
end

% Step 6: Display result
fprintf('✅ %d frames saved to:\n%s\n', frameCount, outputFolder);

%***********************************************************************%
```

---

## 📁 Output

- A new folder named `your_video_filename_frames` is created in the same directory.
- Inside this folder, you'll find frames saved as:
  - `frame_001.jpg`
  - `frame_002.jpg`
  - ...

---

## ✅ Notes

- This script supports any `.mp4` video file.
- Works well even for high-resolution videos.
- You can modify the script to:
  - Save only every Nth frame
  - Convert frames to grayscale
  - Rebuild the video later from the frames

---

## 🧠 Author

Created by **Alireza**  
📅 July 2025  
