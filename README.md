#Frequency Division Multiplexing
#Aim:
To study and implement Frequency Division Multiplexing (FDM) and Demultiplexing using SCILAB by combining six different message signals into a single composite signal for transmission and then recovering each message signal at the receiver through demodulation and filtering.
Apparatus Required:
Computer system with SCILAB software installed.
#Theory:
Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a unique carrier frequency. Each message is modulated with its respective carrier so that their frequency bands do not overlap. These modulated signals are then combined to form a single multiplexed signal for transmission. At the receiver end, the signal is demultiplexed by using the same carrier frequencies for demodulation, followed by low-pass filtering to recover the original baseband signals. FDM is widely used in radio broadcasting, cable television, and satellite communication systems where efficient bandwidth utilization is essential.
#Algorithm:
1.Start the program and initialize the sampling frequency fs and time vector t. 2.Generate six message signals of different frequencies (150 Hz to 900 Hz) using sine functions. 3.Assign six distinct carrier frequencies (3 kHz to 13 kHz) to each message signal to avoid overlap. 4.Modulate each message signal by multiplying it with its corresponding carrier (Amplitude Modulation). 5.Add all modulated signals to obtain the combined FDM signal representing multiple channels. 6.Plot all six message signals and the multiplexed signal for observation. 7.Demodulate each signal by multiplying the FDM signal with its corresponding carrier frequency. 8.Apply a low-pass filter to extract the original baseband signals (recovering the messages). 9.Plot the demodulated signals to verify successful recovery. 10.End the program after confirming proper multiplexing and demultiplexing operation.

#Code:
```
clc;
clear;
close;

fs = 25000;              
t = 0:1/fs:0.04;         

// Message and carrier frequencies
fm = [80, 160, 240, 320, 400, 480]; 
fc = [2500, 3500, 4500, 5500, 6500, 7500];

// Amplitude of messages changed to 2.3 (same for all)
amp = 2.3 * ones(1,6);

// Small phase offsets for each carrier
phi = [0, %pi/18, %pi/16, %pi/14, %pi/12, %pi/10];

// Generate message signals
m = zeros(6, length(t));
for i = 1:6
    m(i, :) = amp(i) * sin(2*%pi*fm(i)*t);
end

// FDM multiplexing
fdm = zeros(1, length(t));
for i = 1:6
    c = cos(2*%pi*fc(i)*t + phi(i));
    s = m(i, :) .* c;
    fdm = fdm + s;
end

// Plot individual message signals
scf(1); clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, m(i, :));
    xtitle("Message Signal M" + string(i));
end

// Plot FDM composite signal
scf(2); clf;
plot(t, fdm);
xtitle("FDM Composite Signal");

// Demodulation and low-pass filtering
demod = zeros(6, length(t));
N = 120;                         // Moving average LPF length
h = ones(1, N) / N;

for i = 1:6
    c = cos(2*%pi*fc(i)*t + phi(i));
    x = fdm .* c;
    y = conv(x, h, "same");
    demod(i, :) = y;
end

// Plot recovered (demodulated) signals
scf(3); clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, demod(i, :));
    xtitle("Demodulated Signal D" + string(i));
end

disp("FDM and Demultiplexing completed with updated amplitude 2.3!");

```

#Tabulation:

![WhatsApp Image 2025-12-05 at 11 57 24_39ef1354](https://github.com/user-attachments/assets/9d4e95c0-7835-40e0-935d-d796393c18a9)

#Result:
The Frequency Division Multiplexing (FDM) and Demultiplexing of six different message signals were successfully implemented using SCILAB.All six message signals were modulated with distinct carrier frequencies and combined to form a single multiplexed signal. Upon demodulation and low-pass filtering, each original message signal was accurately recovered, verifying the correct working of the FDM and demultiplexing pro
