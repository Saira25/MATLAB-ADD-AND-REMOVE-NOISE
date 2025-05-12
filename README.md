# MATLAB-ADD-AND-REMOVE-NOISE
#This project focuses on improving audio quality by investigating noise addition and reduction techniques in audio signals. Initially, we will add controlled noise to a clean audio signal to create a noisy environment. Then, we will design and apply a bandpass filter to effectively remove the introduced noise. 
clc; 
clear; 
close all; 
% Load original audio file 
file_path_original = 'C:\Users\hp\Downloads\RPReplay_Final1717854821.mp3'; 
[audio, fs] = audioread(file_path_original); 
% Play original audio 
sound(audio, fs); 
pause(4); % Pause for 4 seconds to let the audio play 
% Time vector 
t = (0:length(audio)-1)/fs; 
% Plot original audio 
figure; 
subplot(3,2,1); 
plot(t, audio, 'b'); 
xlabel('Time (s)'); 
ylabel('Amplitude'); 
title('Original Audio Signal');  
% Add noise to the audio 
noisy_audio = awgn(audio, 5, 'measured'); % SNR = 5 
sound(noisy_audio, fs); 
pause(4); % Pause for 4 seconds to let the noisy audio play 
% Plot noisy audio 
subplot(3,2,3); 
plot(t, noisy_audio, 'r'); 
xlabel('Time (s)'); 
ylabel('Amplitude'); 
title('Noisy Audio Signal'); 
% Bandpass filter design 
order = 4; 
min_freq = 100; 
max_freq = 4000; 
[num, denum] = butter(order, [min_freq max_freq]/(fs/2), 'bandpass'); 
% Apply bandpass filter to noisy audio 
filtered_audio = filter(num, denum, noisy_audio); 
sound(filtered_audio, fs); 
pause(4); % Pause for 4 seconds to let the filtered audio play 
% Plot filtered audio 
subplot(3,2,5); 
plot(t, filtered_audio, 'g'); 
xlabel('Time (s)'); 
ylabel('Amplitude'); 
title('Filtered Audio Signal'); 
% Frequency spectrum calculations 
fft_audio = abs(fft(audio)); 
fft_noisy = abs(fft(noisy_audio)); 
fft_filtered = abs(fft(filtered_audio)); 
nos = length(t); 
f = (0:fs/nos:fs-(fs/nos)); 
% Plot the frequency spectra 
subplot(3,2,2); 
plot(f, fft_audio, 'b'); 
xlabel('Frequency (Hz)'); 
ylabel('Amplitude'); 
title('Spectrum of Original Audio'); 
subplot(3,2,4); 
plot(f, fft_noisy, 'r'); 
xlabel('Frequency (Hz)'); 
ylabel('Amplitude'); 
title('Spectrum of Noisy Audio'); 
subplot(3,2,6); 
plot(f, fft_filtered, 'g'); 
xlabel('Frequency (Hz)'); 
ylabel('Amplitude'); 
title('Spectrum of Filtered Audio');
