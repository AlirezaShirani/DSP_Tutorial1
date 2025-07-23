# 🎙️ Load, Plot, and Save a Speech Signal in MATLAB

This MATLAB script demonstrates how to:

- Load a `.wav` audio file
- Convert stereo to mono (if needed)
- Play and plot the waveform
- Save the signal and sampling rate for later use in `.mat` or `.txt` formats

---

## 📌 MATLAB Code

```matlab
%***********************************************************************%
%****************** Load, Plot, and Save a Speech Signal ***************%
%***********************************************************************%

% Step 1: Specify the full path of the audio (.wav) file
filename = 'C:\Users\Alireza-MSI-Old\Downloads\harvard.wav';

% Step 2: Read the audio file using audioread
% y  = the audio signal (samples)
% fs = the sampling frequency (Hz)
[y, fs] = audioread(filename);

% Step 3: Play the audio (optional)
sound(y, fs);

% Step 4: Convert stereo to mono (if needed)
% If the audio has two channels (stereo), average them to create a mono signal
if size(y,2) == 2
    y = mean(y, 2);
end

% Step 5: Plot the waveform of the audio signal
figure;
plot(y, 'k');              % Plot waveform in black
xlabel('Sample Index');    % x-axis: time (in samples)
ylabel('Amplitude');       % y-axis: amplitude of the signal
title('Waveform of Speech Signal');
grid on;

% Step 6: Save the signal and sampling rate for future use
% Recommended format: .mat (compact and keeps variables with names)
save('speech_data.mat', 'y', 'fs');

% Step 7 (Optional): Save the raw signal as ASCII text file
% Note: This saves only the signal (not fs) and may result in larger files
save('speech_data.txt', 'y', '-ascii');

% Notes:
% - Use "load('speech_data.mat')" to reload both y and fs later.
% - Use "y = load('speech_data.txt')" if you only saved y in ASCII format.
% - This script can be used as a base for speech signal processing (e.g., filtering, segmentation, feature extraction).

%***********************************************************************%
```

---

## 📁 Output

- A `.mat` file: `speech_data.mat` (contains both `y` and `fs`)
- A `.txt` file: `speech_data.txt` (ASCII text, signal only)
- A waveform plot
- Optional playback of the loaded signal

---

## 🧠 Author

Created by **Alireza**  
📅 July 2025  
