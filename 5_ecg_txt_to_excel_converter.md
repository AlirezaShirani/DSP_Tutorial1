# 📤 Convert ECG Signal from `.txt` to `.xlsx` with Time in Seconds

This MATLAB script demonstrates how to:

- Read ECG signal data from a `.txt` file with time strings (e.g., `0:01.234`)
- Convert time into seconds
- Save the cleaned and formatted signal to a `.xlsx` file

---

## 📌 MATLAB Code

```matlab
%***********************************************************************%
%******** Convert ECG Data from TXT to Excel with Time Conversion ******%
%***********************************************************************%

% Step 1: Define file paths
inputFile  = 'I:\\1403\\Industrial_Project\\Darman_Tajhiz\\Simulation QRS Detection & pan tompkins\\ECG_Value_4_10SEC.txt';
outputCSV  = 'I:\\1403\\Industrial_Project\\Darman_Tajhiz\\Simulation QRS Detection & pan tompkins\\ECG_Value_4_10SEC_converted.xlsx';

% Step 2: Read data from TXT file
fid = fopen(inputFile, 'r');
data = textscan(fid, '%s %f');  % Time as string, ECG as float
fclose(fid);

% Step 3: Parse and convert time strings to seconds
timeStrings = data{1};
ecgValues = data{2};
timeInSeconds = zeros(length(timeStrings), 1);

for i = 1:length(timeStrings)
    parts = sscanf(timeStrings{i}, '%d:%f');  % Convert 'min:sec.millisec'
    timeInSeconds(i) = parts(1) * 60 + parts(2);
end

% Step 4: Create and export a table to Excel
T = table(timeInSeconds, ecgValues, 'VariableNames', {'Time_sec', 'ECG_mV'});
writetable(T, outputCSV);

% Step 5: Display confirmation message
disp('✅ Conversion to CSV completed.');
```

---

## 📁 Input File Format

```
0:00.000   0.12
0:00.004   0.19
0:00.008   0.14
...
```

- Column 1: Time in `min:sec.millisec` format  
- Column 2: ECG signal amplitude (in mV)

---

## 📤 Output

A `.xlsx` file named:  
**`ECG_Value_4_10SEC_converted.xlsx`**  
with two columns:
- `Time_sec` (converted time in seconds)
- `ECG_mV` (signal amplitude)

---

## 🧠 Author

Created by **Alireza**  
📅 July 2025  
