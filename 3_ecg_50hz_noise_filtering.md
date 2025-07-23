# 🫀 50 Hz Noise Addition and Notch Filtering of ECG Signal in MATLAB

This script demonstrates how to:

- Load ECG data from an Excel file
- Simulate 50 Hz power-line interference
- Apply a notch filter to remove the noise
- Visualize the original, noisy, and filtered ECG signals

---

## 📌 MATLAB Code

```matlab
%***********************************************************************%
%**** Add and Remove 50 Hz Noise from ECG Signal using Notch Filter ****%
%***********************************************************************%

% Step 1: Define the folder and Excel file containing the ECG signal
folder = 'I:\1403\Industrial_Project\Darman_Tajhiz\Simulation QRS Detection & pan tompkins';
filename = 'ECG_Value_4_10SEC_converted.xlsx';  % ECG signal file
fullpath = fullfile(folder, filename);

% Step 2: Set full path to the Excel file (optional duplication for clarity)
outputCSV = fullpath;

% Step 3: Read the data (assumes a column named 'Signal' in Excel file)
data = readtable(outputCSV);  % Use xlsread if your MATLAB version does not support readtable

% Step 4: Define sampling frequency
Fs = 1000;  % Hz

% Step 5: Generate time vector
t = (0:height(data)-1) / Fs;

% Step 6: Extract original ECG signal
signal = data.Signal;  % Make sure your Excel column is named 'Signal'

% Step 7: Add synthetic 50 Hz sine wave noise
noiseFreq = 50;  % Hz
noiseAmplitude = 0.5 * max(abs(signal));  % Half of max signal amplitude
noise = noiseAmplitude * sin(2*pi*noiseFreq*t)';  % Column vector

% Combine signal with noise
signal_noisy = signal + noise;

% Step 8: Plot original and noisy ECG signals
figure;
subplot(3,1,1);
plot(t, signal);
title('Original ECG Signal');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(3,1,2);
plot(t, signal_noisy);
title('ECG Signal with 50 Hz Noise');
xlabel('Time (s)');
ylabel('Amplitude');

% Step 9: Design a notch filter to eliminate 50 Hz interference
wo = noiseFreq / (Fs/2);  % Normalized frequency
bw = wo / 35;             % Bandwidth for notch filter
[b, a] = iirnotch(wo, bw);  % Notch filter coefficients

% Step 10: Filter the noisy signal
signal_filtered = filter(b, a, signal_noisy);

% Step 11: Plot the filtered signal
subplot(3,1,3);
plot(t, signal_filtered);
title('Filtered ECG Signal (50 Hz Noise Removed)');
xlabel('Time (s)');
ylabel('Amplitude');
```

---

## 📈 Output

- **Subplot 1**: Original ECG signal
- **Subplot 2**: Signal with added 50 Hz interference
- **Subplot 3**: Signal after applying the notch filter

---

## ⚠️ Notes

- Make sure the Excel file has a column labeled **`Signal`**
- Adjust `Fs` if your sampling rate is different
- This approach simulates and removes typical power-line interference

---

## 🧠 Author

Created by **Alireza**  
📅 July 2025  
