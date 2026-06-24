# BASK Modulation with FDM: Digital Data Transmission

An Open-Ended Lab (OEL) project demonstrating digital data transmission pipelines through ASCII encoding, Binary Amplitude Shift Keying (BASK) modulation, and Frequency Division Multiplexing (FDM) inside a simulated noisy channel.

Developed as part of the **Data Communication** course under the Faculty of Science & Technology at **American International University - Bangladesh (AIUB)**[cite: 3, 4].

---

##  Group Members (Group 03 / Section L)

| Name | Student ID |
| --- | --- |
| **MD Shahriar Laskher** | 23-51207-1 |
| **Shahariar Khan** | 23-51222-1 |
| **Md. Saikot Hossain** | 23-51242-1 |
| **T.A Nahian** | 23-51257-1 |
| **Md. Mosharof Hossain Khan** | 23-51259-1 |

**Supervised By:** Mohammad Asaduzzaman Khan

**Semester:** Summer 2024-2025

---

##  Project Objectives & Logic

* **ASCII Conversion:** Translates student member surnames into distinct binary vectors.


* **Line Coding:** Represents raw binary data using Unipolar Non-Return-to-Zero (NRZ) line signaling ($1 = 5\text{V}$, $0 = 0\text{V}$).


* **Modulation & Multiplexing:** Applies BASK modulation over custom carrier frequencies ($f_1 = 2000\text{Hz}$ and $f_2 = 4000\text{Hz}$), merging them into a single composite channel via FDM with introduced Gaussian noise ($\text{SNR} = 10\text{dB}$).


* **Recovery Demodulation:** Implements envelope/coherent threshold detection to isolate, demultiplex, and accurately decode back into human-readable ASCII text string outputs.



---

##  Core Implementation Snippets

### Text to Binary & Binary to Text Converter

```matlab
function dn = asc2bn(txt)
    dec = double(txt);
    p2 = 2.^(0:-1:-7); 
    B = mod(floor(p2'*dec),2);
    dn = reshape(B, 1, numel(B));
end

function txt = bin2asc(dn)
    L = length(dn);
    L8 = 8 * floor(L/8);
    B = reshape(dn(1:L8), 8, L8/8);
    p2 = 2.^(0:7); 
    dec = p2 * B;
    txt = char(dec);
end

```

### Signal Processing Setup

```matlab
clc; clear all; close all;

surname1 = 'KHAN';
surname2 = 'NAHIAN';
x1 = asc2bn(surname1);
x2 = asc2bn(surname2);

% BASK Configuration
bp = 1e-3; % Bit period
A1 = 5; A2 = 0; 
f1 = 2000; f2 = 4000;

```

---


* **Noise Resistance:** The threshold decision criteria efficiently handled the structural distortions introduced by White Gaussian Noise channels at $10\text{dB}$ SNR, yielding a 100% bit validation match back into the original input matrices (`KHAN` and `NAHIAN` string configurations).
