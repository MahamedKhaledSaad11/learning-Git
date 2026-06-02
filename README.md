# Wireless Communications: Formula & Reference Guide

This document compiles and explains all the rules, formulas, and equations from the wireless communication lectures (Slide 1 to Slide 9). For each entry, we detail the mathematical expression, the physical meaning of all parameters, and concrete engineering guidelines on when to apply them.

---

## Table of Contents
1. [Signal Representation, Gain, Attenuation, & Decibels (Slide 1)](#1-signal-representation-gain-attenuation--decibels-slide-1)
2. [Fading & Noise Characteristics (Slide 2)](#2-fading--noise-characteristics-slide-2)
3. [Large-Scale Path Loss & Propagation Models (Slides 3 & 4)](#3-large-scale-path-loss--propagation-models-slides-3--4)
4. [Multipath Channels & Delay Spread Parameters (Slides 5 & 6)](#4-multipath-channels--delay-spread-parameters-slides-5--6)
5. [Wireless Link Performance & Deep Fade Analysis (Slide 7)](#5-wireless-link-performance--deep-fade-analysis-slide-7)
6. [Space Diversity & Maximal Ratio Combining (Slide 8)](#6-space-diversity--maximal-ratio-combining-slide-8)
7. [Multiple Access & Multi-Carrier Systems (Slide 9)](#7-multiple-access--multi-carrier-systems-slide-9)

---

## 1. Signal Representation, Gain, Attenuation, & Decibels (Slide 1)

### 1.1. Voltage Gain and Attenuation
$$A_v = \frac{V_{\text{out}}}{V_{\text{in}}}$$
*   **Parameters:**
    *   $A_v$: Voltage amplification factor (dimensionless ratio).
    *   $V_{\text{out}}$: Output voltage across the load (Volts, $\text{V}$).
    *   $V_{\text{in}}$: Input voltage to the circuit (Volts, $\text{V}$).
*   **When to Use:**
    *   Use to characterize the voltage transfer ratio of active circuits (amplifiers) or passive circuits (filters, attenuators).
    *   If $A_v > 1$, the circuit exhibits **gain** (amplification).
    *   If $A_v < 1$, the circuit exhibits **attenuation** (loss).

---

### 1.2. Power Gain and Attenuation
$$A_p = \frac{P_{\text{out}}}{P_{\text{in}}} = \frac{P_2}{P_1}$$
*   **Parameters:**
    *   $A_p$: Power ratio (dimensionless).
    *   $P_{\text{out}}$ (or $P_2$): Signal power at the output/destination point (Watts, $\text{W}$).
    *   $P_{\text{in}}$ (or $P_1$): Signal power at the input/source point (Watts, $\text{W}$).
*   **When to Use:**
    *   Use in link analysis to evaluate how much signal power changes as it propagates through cables, amplifiers, or open space.

---

### 1.3. Power Gain in Decibels
$$A_p\text{ (dB)} = 10 \log_{10}\left(\frac{P_{\text{out}}}{P_{\text{in}}}\right)$$
*   **Parameters:**
    *   $A_p\text{ (dB)}$: Power gain expressed in decibels ($\text{dB}$).
    *   $P_{\text{out}}, P_{\text{in}}$: Output and input powers, respectively ($\text{W}$ or $\text{mW}$, must use identical units).
*   **When to Use:**
    *   Use to express power changes in logarithmic units, converting multiplication/division operations into simple additions/subtractions.
    *   A **positive** $\text{dB}$ value represents gain ($P_{\text{out}} > P_{\text{in}}$).
    *   A **negative** $\text{dB}$ value represents attenuation or loss ($P_{\text{out}} < P_{\text{in}}$).

---

### 1.4. Cascaded Gain (Stage Addition)
$$A_{\text{overall}}\text{ (dB)} = A_1\text{ (dB)} + A_2\text{ (dB)} + A_3\text{ (dB)} + \dots$$
*   **Parameters:**
    *   $A_{\text{overall}}\text{ (dB)}$: Cumulative power gain of the entire system.
    *   $A_i\text{ (dB)}$: Gain (positive) or loss (negative) of individual cascaded components (e.g., cables, amplifiers, antennas).
*   **When to Use:**
    *   Use when multiple communication blocks are connected in series (transmitter $\to$ cable $\to$ channel $\to$ receiver). It is much simpler than multiplying linear ratios.

---

### 1.5. Absolute Power in dBm
$$P_{\text{dBm}} = 10 \log_{10}\left(\frac{P_{\text{absolute}}}{1\text{ mW}}\right)$$
*   **Parameters:**
    *   $P_{\text{dBm}}$: Absolute power level relative to 1 milliwatt ($\text{dBm}$).
    *   $P_{\text{absolute}}$: Power value in Watts ($\text{W}$) or milliwatts ($\text{mW}$).
*   **When to Use:**
    *   Use when expressing the absolute strength of a transmitter output, receiver sensitivity, or noise floor.
    *   > [!IMPORTANT]
      > Use $\text{dB}$ for relative ratios (gains/losses) and $\text{dBm}$ for absolute power values. Never add $\text{dBm} + \text{dBm}$.

---

### 1.6. Link Attenuation from Absolute Power
$$\text{Attenuation (dB)} = P_{\text{Rx, dBm}} - P_{\text{Tx, dBm}}$$
*   **Parameters:**
    *   $P_{\text{Tx, dBm}}$: Transmit power ($\text{dBm}$).
    *   $P_{\text{Rx, dBm}}$: Received power ($\text{dBm}$).
*   **When to Use:**
    *   Use to calculate the total path loss or gain of a communication channel by subtracting the transmitter power from the receiver power. The result is always in $\text{dB}$.

---

### 1.7. Cable Loss Calculation
$$\text{Loss}_{\text{total}}\text{ (dB)} = \text{Loss rate}\text{ (dB/km)} \times \text{Distance}\text{ (km)}$$
*   **Parameters:**
    *   $\text{Loss rate}$: Attenuation coefficient of the transmission line, usually given in negative $\text{dB/km}$.
    *   $\text{Distance}$: Total length of the cable.
*   **When to Use:**
    *   Use to find the attenuation introduced by cables of a specific length before feeding signals to antennas.

---

## 2. Fading & Noise Characteristics (Slide 2)

### 2.1. Thermal Noise Power (Johnson-Nyquist Noise)
$$N = k T B$$
*   **Parameters:**
    *   $N$: Thermal noise power (Watts, $\text{W}$).
    *   $k$: Boltzmann's constant ($1.38 \times 10^{-23}\text{ Joules/Kelvin, J/K}$).
    *   $T$: Absolute temperature in Kelvin ($\text{K}$), where $T_{\text{Kelvin}} = T_{^{\circ}\text{C}} + 273$. (Standard room temperature $17^{\circ}\text{C} = 290\text{ K}$).
    *   $B$: Bandwidth over which the noise is measured (Hertz, $\text{Hz}$).
*   **When to Use:**
    *   Use to find the absolute physical limit of noise in any receiver channel. It defines the minimum detectable signal power (receiver sensitivity limit).
    *   To express in $\text{dBm}$:
        $$N_{\text{dBm}} = 10 \log_{10}\left(\frac{k T B}{10^{-3}}\right) = -174\text{ dBm/Hz} + 10 \log_{10}(B)$$

---

### 2.2. Wiener-Khinchine Theorem
$$S_x(f) = \int_{-\infty}^{\infty} R_x(\tau) e^{-j 2 \pi f \tau} d\tau$$
*   **Parameters:**
    *   $S_x(f)$: Power Spectral Density (PSD) of the random signal $x(t)$ ($\text{Watts/Hz}$).
    *   $R_x(\tau) = \mathbb{E}[x(t)x(t+\tau)]$: Autocorrelation function of the process at time lag $\tau$.
    *   $f$: Frequency ($\text{Hz}$).
*   **When to Use:**
    *   Use to analyze the frequency distribution of a noise or signal process by computing the Fourier Transform of its time-domain autocorrelation function.

---

### 2.3. White Noise Power Spectral Density
$$S_w(f) = \frac{N_0}{2}$$
*   **Parameters:**
    *   $S_w(f)$: Two-sided Power Spectral Density ($\text{Watts/Hz}$).
    *   $N_0$: One-sided noise power spectral density, equivalent to $kT$ for thermal noise.
*   **When to Use:**
    *   Use as an idealized model for wideband thermal noise where power is distributed uniformly across all frequencies from $-\infty$ to $+\infty$.

---

### 2.4. Signal-to-Noise Ratio (SNR)
$$\text{SNR} = \frac{P_{\text{signal}}}{P_{\text{noise}}} \quad\implies\quad \text{SNR}_{\text{dB}} = 10 \log_{10}\left(\frac{P_{\text{signal}}}{P_{\text{noise}}}\right)$$
*   **Parameters:**
    *   $P_{\text{signal}}$: Desired signal power ($\text{Watts}$ or $\text{dBm}$).
    *   $P_{\text{noise}}$: Noise power ($\text{Watts}$ or $\text{dBm}$).
*   **When to Use:**
    *   Use at the receiver input (before detection/demodulation) to quantify signal quality. It determines the ultimate capacity and bit error rate of the channel.

---

## 3. Large-Scale Path Loss & Propagation Models (Slides 3 & 4)

### 3.1. Friis Free Space Propagation Model
$$P_r(d) = P_t G_t G_r \left(\frac{\lambda}{4 \pi d}\right)^2 = P_t G_t G_r \left(\frac{c}{4 \pi d f}\right)^2$$
*   **Parameters:**
    *   $P_r(d)$: Received power at distance $d$ (Watts, $\text{W}$).
    *   $P_t$: Transmit power (Watts, $\text{W}$).
    *   $G_t, G_r$: Transmit and receive antenna power gains (dimensionless ratios).
    *   $\lambda = c/f$: Wavelength of the carrier frequency (meters, $\text{m}$).
    *   $c$: Speed of light ($3 \times 10^8\text{ m/s}$).
    *   $f$: Carrier frequency (Hertz, $\text{Hz}$).
    *   $d$: Separation distance between antennas (meters, $\text{m}$).
*   **When to Use:**
    *   Use to predict received power when there is a clear, unobstructed Line-of-Sight (LOS) path between transmitter and receiver (e.g., satellite links, terrestrial microwave towers).
    *   **Constraint:** Only valid in the far-field region of the antennas: $d \gg d_f = 2D^2/\lambda$ (where $D$ is the largest antenna dimension).

---

### 3.2. Free Space Path Loss (FSPL) in Decibels
$$\text{FSPL(dB)} = 32.4 + 20 \log_{10}(f_{\text{ MHz}}) + 20 \log_{10}(d_{\text{ km}})$$
*   **Parameters:**
    *   $f_{\text{ MHz}}$: Carrier frequency in Megahertz ($\text{MHz}$).
    *   $d_{\text{ km}}$: Link distance in kilometers ($\text{km}$).
*   **When to Use:**
    *   Standard formula for calculating line-of-sight signal loss in decibels.
    *   To get received power:
        $$P_{r,\text{ dBm}} = P_{t,\text{ dBm}} + G_{t,\text{ dBi}} + G_{r,\text{ dBi}} - \text{FSPL}_{\text{dB}}$$

---

### 3.3. Two-Ray Ground Reflection Model (Flat Earth Model)
$$P_r(d) = P_t G_t G_r \frac{h_t^2 h_r^2}{d^4}$$
$$\text{Path Loss (dB)} = 40 \log_{10}(d) - 20 \log_{10}(h_t) - 20 \log_{10}(h_r)$$
*   **Parameters:**
    *   $h_t$: Height of the transmit antenna above the ground (meters, $\text{m}$).
    *   $h_r$: Height of the receive antenna above the ground (meters, $\text{m}$).
    *   $d$: T-R separation distance (meters, $\text{m}$).
*   **When to Use:**
    *   Use for mobile communication links over several kilometers where antennas are on tall towers and a ground-reflected path interferes with the direct path.
    *   > [!TIP]
      > Note that the received power drops off as $d^{-4}$ (40 dB/decade) rather than $d^{-2}$ (20 dB/decade), and is independent of wavelength (frequency) at long distances.

---

### 3.4. Log-Distance Path Loss Model (Non-Line-of-Sight)
$$P_r(d) = P_r(d_0) \left(\frac{d_0}{d}\right)^n \quad\implies\quad \text{PL}(d)\text{ (dB)} = \text{PL}(d_0)\text{ (dB)} + 10 n \log_{10}\left(\frac{d}{d_0}\right)$$
*   **Parameters:**
    *   $d_0$: Close-in reference distance in the far-field (typically $1\text{ km}$ or $100\text{ m}$ for outdoor, $1\text{ m}$ for indoor).
    *   $d$: Actual transmitter-receiver distance ($d \ge d_0$).
    *   $n$: Path loss exponent indicating the rate at which path loss increases with distance.
*   **When to Use:**
    *   Use to estimate average path loss in shadowed/obstructed environments (e.g., indoor walls, urban streets) where Friis' model does not apply.
    *   **Common values of $n$:**
        *   Free space: $n = 2$
        *   Urban cellular: $n = 2.7\text{ to }3.5$
        *   Shadowed urban cellular: $n = 3.0\text{ to }5.0$
        *   In-building (obstructed): $n = 4.0\text{ to }6.0$

---

### 3.5. Okumura Model
$$L_{50}\text{ (dB)} = \text{FSPL} + A_{mu}(f, d) - G(h_t) - G(h_r) - G_{\text{AREA}}$$
*   **Parameters:**
    *   $L_{50}$: Median propagation path loss ($\text{dB}$).
    *   $A_{mu}(f, d)$: Median attenuation relative to free space (read from curves).
    *   $G(h_t) = 20 \log_{10}\left(\frac{h_t}{200}\right)$ for $30\text{ m} < h_t < 1000\text{ m}$ (BS antenna height gain).
    *   $G(h_r) = 20 \log_{10}\left(\frac{h_r}{3}\right)$ for $h_r \le 3\text{ m}$ (MS antenna height gain).
    *   $G(h_r) = 10 \log_{10}\left(\frac{h_r}{3}\right)$ for $3\text{ m} < h_r < 10\text{ m}$ (MS antenna height gain).
    *   $G_{\text{AREA}}$: Environment gain correction (read from curves).
*   **When to Use:**
    *   Empirical path loss model valid for $f_c = 150-1920\text{ MHz}$, $h_t = 30-1000\text{ m}$, $h_r = 1-10\text{ m}$, and $d = 1-100\text{ km}$. Use to predict average signal levels in urban/suburban environments using measurement charts.

---

### 3.6. Okumura-Hata Model (Standard Hata Model)
$$L_{50,\text{ urban}}\text{ (dB)} = 69.55 + 26.16 \log_{10}(f_c) - 13.82 \log_{10}(h_t) - a(h_r) + [44.9 - 6.55 \log_{10}(h_t)] \log_{10}(d)$$
*   **Parameters:**
    *   $f_c$: Carrier frequency in $\text{MHz}$ ($150 - 1500\text{ MHz}$).
    *   $h_t$: Base station antenna height in meters ($30 - 200\text{ m}$).
    *   $h_r$: Mobile antenna height in meters ($1 - 10\text{ m}$).
    *   $d$: Separation distance in kilometers ($1 - 20\text{ km}$).
    *   $a(h_r)$: Mobile antenna height correction factor:
        *   **Medium-to-Small Cities:**
            $$a(h_r) = (1.1 \log_{10}(f_c) - 0.7)h_r - (1.56 \log_{10}(f_c) - 0.8)\text{ dB}$$
        *   **Large Cities ($f_c < 1500\text{ MHz}$):**
            $$a(h_r) = 8.29 (\log_{10}(1.54 h_r))^2 - 1.1\text{ dB}$$
        *   **Large Cities ($f_c \ge 1500\text{ MHz}$):**
            $$a(h_r) = 3.2 (\log_{10}(11.75 h_r))^2 - 4.97\text{ dB}$$
*   **When to Use:**
    *   Use to programmatically calculate path loss in regular macro-cellular systems without reading graphical curves.
    *   **Suburban and Open Area Corrections:**
        $$L_{\text{suburban}}\text{ (dB)} = L_{\text{urban}} - 2 \left[\log_{10}\left(\frac{f_c}{28}\right)\right]^2 - 5.4$$
        $$L_{\text{open}}\text{ (dB)} = L_{\text{urban}} - 4.78 [\log_{10}(f_c)]^2 + 18.33 \log_{10}(f_c) - 40.94$$

---

### 3.7. COST 231 Hata Model (Higher Frequencies Extension)
$$L_{\text{COST}}(dB) = 46.3 + 33.9 \log_{10}(f_c) - 13.82 \log_{10}(h_t) - a(h_r) + [44.9 - 6.55 \log_{10}(h_t)] \log_{10}(d) + C$$
*   **Parameters:**
    *   $f_c$: Carrier frequency in $\text{MHz}$ ($1500 - 2000\text{ MHz}$).
    *   $C$: Environment factor:
        *   $C = 0\text{ dB}$ for medium cities and suburban areas.
        *   $C = 3\text{ dB}$ for metropolitan centers/large cities.
    *   $a(h_r)$: Mobile antenna height correction (same as standard Hata).
*   **When to Use:**
    *   Use to estimate path loss for cellular systems operating in the $1.8\text{ GHz}$ or $1.9\text{ GHz}$ bands (like GSM1800, PCS, early 3G).

---

### 3.8. Doppler Shift ($f_d$)
$$f_d = \frac{v}{\lambda} \cos(\theta) = \frac{v f_c}{c} \cos(\theta)$$
*   **Parameters:**
    *   $f_d$: Frequency shift (Hertz, $\text{Hz}$).
    *   $v$: Mobile speed (meters/second, $\text{m/s}$). To convert from $\text{km/h}$ to $\text{m/s}$, divide by $3.6$.
    *   $\lambda = c/f_c$: Carrier wavelength (meters, $\text{m}$).
    *   $f_c$: Carrier frequency ($\text{Hz}$).
    *   $\theta$: Angle of arrival of the incoming wave relative to the direction of vehicle motion.
*   **When to Use:**
    *   Use to find the frequency change of received signals due to receiver mobility.
    *   If the mobile moves **towards** the wave source ($\theta = 0^{\circ}$), $f_d$ is positive ($f_{\text{received}} = f_c + f_{d,\text{max}}$).
    *   If the mobile moves **away** from the wave source ($\theta = 180^{\circ}$), $f_d$ is negative ($f_{\text{received}} = f_c - f_{d,\text{max}}$).
    *   If the mobile moves **perpendicular** ($\theta = 90^{\circ}$), $f_d = 0$.

---

## 4. Multipath Channels & Delay Spread Parameters (Slides 5 & 6)

### 4.1. Baseband Channel Impulse Response (Time-Varying)
$$h(t, \tau) = \sum_{i=0}^{N-1} a_i(t) e^{-j \phi_i(t)} \delta(\tau - \tau_i(t))$$
*   **Parameters:**
    *   $t$: Time when the channel is probed (represents time variation due to motion).
    *   $\tau$: Excess delay parameter.
    *   $a_i(t)$: Real amplitude (attenuation) of the $i$-th path.
    *   $\tau_i(t)$: Propagation delay of the $i$-th path.
    *   $\phi_i(t) = 2 \pi f_c \tau_i(t) + \phi_{i0}$: Phase shift of the $i$-th path.
*   **When to Use:**
    *   Use as the mathematical baseline for simulating multipath channels. The received signal is computed as:
        $$y(t) = x(t) * h(t,\tau) + n(t)$$

---

### 4.2. Received Power of Wideband vs. Narrowband Signals
*   **Wideband Signal ($T_b < \text{max delay spread}$ or $B_{\text{signal}} > B_c$):**
    $$P_{\text{wideband}} \approx \sum_{i=0}^{N-1} |a_i|^2$$
    *   *Usage:* Individual multipath components are resolvable. Since their powers sum up directly, received power fluctuates very little over small areas.
*   **Narrowband Signal ($T_b > \text{max delay spread}$ or $B_{\text{signal}} < B_c$):**
    $$P_{\text{narrowband}} = \left| \sum_{i=0}^{N-1} a_i e^{-j \phi_i} \right|^2$$
    *   *Usage:* Multipath components cannot be resolved and add vectorially. Small changes in position (fractions of a wavelength) cause large variations in phase, leading to deep destructive fading (up to $30-40\text{ dB}$).

---

### 4.3. Mean Excess Delay ($\bar{\tau}$)
$$\bar{\tau} = \frac{\sum_k P(\tau_k) \tau_k}{\sum_k P(\tau_k)}$$
*   **Parameters:**
    *   $\tau_k$: Excess delay of the $k$-th bin relative to the first arriving signal ($\tau_0 = 0$).
    *   $P(\tau_k)$: Power of the signal component at delay $\tau_k$.
*   **When to Use:**
    *   Characterizes the average arrival time of multipath components, weighted by their received power.

---

### 4.4. RMS Delay Spread ($\sigma_{\tau}$)
$$\sigma_{\tau} = \sqrt{\overline{\tau^2} - (\overline{\tau})^2} \quad\text{where}\quad \overline{\tau^2} = \frac{\sum_k P(\tau_k) \tau_k^2}{\sum_k P(\tau_k)}$$
*   **Parameters:**
    *   $\overline{\tau^2}$: Second moment of the power delay profile.
    *   $\overline{\tau}$: Mean excess delay.
*   **When to Use:**
    *   Measures the temporal dispersion of the channel. It is the primary parameter used to determine if a channel causes ISI.
    *   Typical values: Microseconds ($\mu\text{s}$) for outdoors, nanoseconds ($\text{ns}$) for indoors.

---

### 4.5. Coherence Bandwidth ($B_c$)
*   **Strict Definition (correlation $> 0.9$):**
    $$B_c \approx \frac{1}{50 \sigma_{\tau}}$$
*   **Relaxed Definition (correlation $> 0.5$):**
    $$B_c \approx \frac{1}{5 \sigma_{\tau}}$$
*   **When to Use:**
    *   Defines the frequency range where the channel gain is relatively constant.
    *   If signal bandwidth $B_s < B_c$, the channel is **Flat Fading** (no ISI, simple receiver).
    *   If signal bandwidth $B_s > B_c$, the channel is **Frequency-Selective Fading** (causes ISI, requires equalization or OFDM).

---

### 4.6. Doppler Spread ($B_D$)
$$B_D = f_m = \frac{v}{\lambda}$$
*   **When to Use:**
    *   Measures the range of spectral broadening of a single-tone carrier due to mobility.

---

### 4.7. Coherence Time ($T_c$)
*   **Strict Definition (correlation $> 0.5$):**
    $$T_c \approx \frac{9}{16 \pi f_m} = \frac{0.179}{f_m}$$
*   **Digital Communication Rule of Thumb:**
    $$T_c \approx \frac{3}{4 \pi f_m} = \frac{0.239}{f_m} \quad\text{or}\quad T_c \approx \frac{0.423}{f_m}$$
*   **When to Use:**
    *   Defines the time interval over which channel coefficients remain highly correlated.
    *   If symbol duration $T_s < T_c$, the channel is **Slow Fading** (channel is constant over a symbol).
    *   If symbol duration $T_s > T_c$, the channel is **Fast Fading** (channel changes during a symbol, causing distortion).

---

## 5. Wireless Link Performance & Deep Fade Analysis (Slide 7)

### 5.1. AWGN (Wireline) Bit Error Rate (BPSK/QPSK)
$$\text{BER}_{\text{AWGN}} = Q\left(\sqrt{2 \text{ SNR}}\right)$$
*   **Parameters:**
    *   $\text{SNR} = \frac{P}{\sigma_n^2}$: Power ratio of signal to noise.
    *   $Q(x) = \frac{1}{\sqrt{2\pi}} \int_x^{\infty} e^{-u^2/2} du$: Gaussian tail probability.
*   **When to Use:**
    *   Gives the theoretical baseline performance of BPSK in a stable channel (like fiber or coax) without fading. BER decreases exponentially as SNR increases.

---

### 5.2. Average BER in Rayleigh Fading (BPSK)
$$\text{BER}_{\text{Rayleigh}} = \frac{1}{2} \left(1 - \sqrt{\frac{\text{SNR}_0}{2 + \text{SNR}_0}}\right) \approx \frac{1}{4 \text{SNR}_0} \quad (\text{for high SNR})$$
*   **Parameters:**
    *   $\text{SNR}_0$: Average received SNR ($\mathbb{E}[a^2] \cdot P / \sigma_n^2$).
*   **When to Use:**
    *   Predicts performance of a single-antenna BPSK system in flat Rayleigh fading.
    *   > [!WARNING]
      > Fading changes the BER behavior from exponential to linear ($1/\text{SNR}$), meaning that to achieve low BER (e.g. $10^{-5}$), a massive "fade margin" of $30-40\text{ dB}$ is required.

---

### 5.3. Deep Fade Condition & Probability
*   **Deep Fade Condition:**
    $$P_{\text{Rx}} < \sigma_n^2 \quad\implies\quad a^2 P < \sigma_n^2 \quad\implies\quad a < \frac{1}{\sqrt{\text{SNR}}}$$
*   **Probability of Deep Fade (at High SNR):**
    $$P_{\text{fade}} = \text{Pr}\left(a^2 < \frac{1}{\text{SNR}}\right) = 1 - e^{-1/\text{SNR}} \approx \frac{1}{\text{SNR}}$$
*   **When to Use:**
    *   Explains why flat fading has such bad BER performance: at high SNR, the average BER is dominated by the probability of the channel falling into a deep fade.
    *   To improve link quality, we must use diversity to reduce the probability of deep fades.

---

## 6. Space Diversity & Maximal Ratio Combining (Slide 8)

### 6.1. Linear Combined Vector (Beamforming)
$$y_{\text{comb}} = \mathbf{w}^H \mathbf{y} = \sum_{i=1}^L w_i^* y_i$$
*   **Parameters:**
    *   $\mathbf{y} = [y_1, y_2, \dots, y_L]^T$: Received signals at the $L$ antennas.
    *   $\mathbf{w} = [w_1, w_2, \dots, w_L]^T$: Combining weight vector.
    *   $w_i^*$: Complex conjugate of $w_i$.
*   **When to Use:**
    *   Use when analyzing linear combining receivers in Single-Input Multiple-Output (SIMO) systems.

---

### 6.2. Maximal Ratio Combining (MRC) Optimum SNR
$$\mathbf{w}_{\text{opt}} = \mathbf{h} \quad\implies\quad \text{SNR}_{\text{MRC}} = \frac{P}{\sigma_n^2} \sum_{i=1}^L |h_i|^2 = \text{SNR}_0 \sum_{i=1}^L |h_i|^2$$
*   **Parameters:**
    *   $h_i$: Complex fading coefficient of the $i$-th receive antenna.
    *   $\text{SNR}_0$: Average branch SNR without fading.
    *   $L$: Number of receive antennas.
*   **When to Use:**
    *   MRC is the optimal linear combining technique that maximizes the output SNR by rotating the phases and scaling the amplitudes of each branch proportionally to its signal strength.

---

### 6.3. Probability Density Function of MRC Channel Gain ($g$)
$$f_G(g) = \frac{g^{L-1} e^{-g}}{(L-1)!} \quad (\text{for } g = \sum_{i=1}^L |h_i|^2)$$
*   **When to Use:**
    *   Use when performing analytical integration to find average capacity or average BER of an $L$-branch MRC system. It is a Chi-square distribution with $2L$ degrees of freedom.

---

### 6.4. Average BER with L-Branch MRC (Rayleigh Fading)
$$\text{BER}_L = \left(\frac{1-\mu}{2}\right)^L \sum_{k=0}^{L-1} \binom{L-1+k}{k} \left(\frac{1+\mu}{2}\right)^k \quad\text{where}\quad \mu = \sqrt{\frac{\text{SNR}_0}{2 + \text{SNR}_0}}$$
$$\text{BER}_L \approx \binom{2L-1}{L} \left(\frac{1}{4 \text{SNR}_0}\right)^L \quad (\text{at high SNR})$$
*   **When to Use:**
    *   Predicts BPSK performance when using $L$ receive antennas with MRC combining.
    *   > [!TIP]
      > The BER decreases as $1/\text{SNR}_0^L$. This dramatically increases the slope of the BER-vs-SNR curve, meaning diversity effectively eliminates deep fade events. The diversity order is $L$.

---

### 6.5. Minimum Antenna Spacing for Space Diversity
$$d_{\text{min}} \ge 0.5 \lambda = \frac{0.5 c}{f_c}$$
*   **Parameters:**
    *   $\lambda$: Carrier wavelength.
    *   $f_c$: Carrier frequency.
*   **When to Use:**
    *   Design rule to ensure that fading across different antenna elements is statistically independent (uncorrelated).
    *   **Rule of Thumb:**
        *   *Mobile Station (MS):* Spacing must be $\ge 0.5 \lambda$ (easy to fit at high frequencies like $2.3\text{ GHz} \to 6.5\text{ cm}$).
        *   *Base Station (BS):* Spacing must be several tens of wavelengths (e.g. $10\lambda$ to $30\lambda$) due to narrow angular spread at elevated heights.

---

## 7. Multiple Access & Multi-Carrier Systems (Slide 9)

### 7.1. OFDM Subcarrier Orthogonality Spacing
$$\Delta f = \frac{1}{T}$$
*   **Parameters:**
    *   $\Delta f$: Subcarrier spacing ($\text{Hz}$).
    *   $T$: Useful symbol duration ($\text{seconds}$).
*   **When to Use:**
    *   Calculates the minimum frequency-domain subcarrier spacing to prevent Inter-Carrier Interference (ICI) in OFDM. For example, in LTE, $T = 66.7\ \mu\text{s} \implies \Delta f = 15\text{ kHz}$.

---

### 7.2. OFDM Modulation and Demodulation (IFFT/FFT)
*   **IFFT (Modulation):**
    $$x[n] = \sum_{k=0}^{N-1} X_k e^{j \frac{2 \pi k n}{N}}$$
*   **FFT (Demodulation):**
    $$X_k = \frac{1}{N} \sum_{n=0}^{N-1} x[n] e^{-j \frac{2 \pi k n}{N}}$$
*   **Parameters:**
    *   $X_k$: Data symbol (e.g. QPSK, QAM) on the $k$-th subcarrier.
    *   $x[n]$: Time-domain samples of the composite signal.
    *   $N$: Number of subcarriers (FFT size).
*   **When to Use:**
    *   Practical implementation of OFDM. IFFT generates the orthogonal subcarriers at the transmitter, and FFT separates them at the receiver, replacing banks of analog oscillators.

---

### 7.3. NOMA Downlink Superimposed Transmitted Signal
$$x = \sum_{i=1}^K \sqrt{P_i} x_i$$
*   **Parameters:**
    *   $x_i$: Normalized message signal of user $i$ ($\mathbb{E}[|x_i|^2] = 1$).
    *   $P_i$: Power allocated to user $i$.
    *   $K$: Total number of users sharing the same time-frequency resource.
*   **When to Use:**
    *   Use in power-domain Non-Orthogonal Multiple Access (NOMA) downlink to construct the combined signal transmitted by the base station.

---

### 7.4. NOMA Successive Interference Cancellation (SIC) Rule
*   **Downlink Power Allocation Rule:**
    *   Allocate **more power** to weak users (poor channel) and **less power** to strong users (good channel):
        $$|h_{\text{weak}}|^2 < |h_{\text{strong}}|^2 \implies P_{\text{weak}} > P_{\text{strong}}$$
*   **SIC Detection Order Rule:**
    *   The receiver decodes signals in descending order of signal strength (strongest user first).
    *   A strong user decodes the weak user's signal first (treating its own signal as noise, which is small due to lower power allocation), subtracts it from the received signal, and then decodes its own signal interference-free.
    *   A weak user decodes its own signal directly, treating the strong user's signal as noise (which is small compared to its own large allocated power).

---

### 7.5. NOMA Achievable Downlink Rates
$$R_i = \log_2\left(1 + \frac{P_i |h_i|^2}{\sum_{j > i} P_j |h_i|^2 + \sigma_i^2}\right)$$
*   **Parameters:**
    *   Users are sorted in ascending order of channel quality:
        $$\frac{|h_1|^2}{\sigma_1^2} \le \frac{|h_2|^2}{\sigma_2^2} \le \dots \le \frac{|h_K|^2}{\sigma_K^2}$$
    *   Power is allocated as: $P_1 > P_2 > \dots > P_K$.
    *   User $i$ can cancel all users $j < i$ (weaker users with higher power) using SIC.
    *   Signals of users $j > i$ (stronger users with lower power) remain as interference.
    *   $\sigma_i^2$: Noise variance at receiver $i$.
*   **When to Use:**
    *   Calculates the theoretical downlink throughput of user $i$ in a power-domain NOMA system, showing the spectral efficiency gain over orthogonal allocation (OFDMA).
