# 🫀 ECG Signal Processing from `.txt` File with Timestamps

This script demonstrates how to:

- Load an ECG signal from a `.txt` file that includes timestamps
- Parse timestamps (e.g., `0:01.230`) into seconds
- Plot the signal versus time

---

## 📌 MATLAB Code

```matlab
%*************************************************************************%
%********* Load and Plot ECG Signal from TXT File with Time Format *******%
%*************************************************************************%

% Step 1: Define full path to the ECG .txt file
% Note: Use double backslashes (\\) in the file path
filename = 'I:\\1403\\Industrial_Project\\Darman_Tajhiz\\Simulation QRS Detection & pan tompkins\\ECG_Value_4_10SEC.txt';

% Step 2: Open and read the file
fid = fopen(filename, 'r');
data = textscan(fid, '%s %f');  % Reads: 1st column = time (string), 2nd = ECG value (float)
fclose(fid);

% Step 3: Separate the two columns
timeStrings = data{1};  % Time column as strings (e.g., '0:01.230')
ecgValues   = data{2};  % ECG values as floating point numbers

% Step 4: Convert time strings into seconds
timeInSeconds = zeros(length(timeStrings), 1);  % Preallocate
for i = 1:length(timeStrings)
    parts = sscanf(timeStrings{i}, '%d:%f');  % Split 'min:sec.millisec'
    timeInSeconds(i) = parts(1) * 60 + parts(2);  % Convert to seconds
end

% Step 5: Plot the ECG signal
figure;
plot(timeInSeconds, ecgValues);
xlabel('Time (seconds)');
ylabel('ECG Value');
title('ECG Signal from File');
grid on;
```

---

## 🧾 Expected Input File Format

```
0:00.000   0.1
0:00.004   0.3
0:00.008   0.5
...
```

- First column = time in `min:sec.millisec` format
- Second column = ECG value

---

## 📈 Output

- A plot of ECG signal versus actual time in seconds

---

## 🧠 Author

Created by **Alireza**  
📅 July 2025  
