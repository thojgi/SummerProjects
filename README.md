# SummerProjects
# Embedded Systems & Hardware Prototyping: 2-Week Arduino Sprint

A collection of embedded engineering systems developed during an intensive two-week hardware sprint following Summer 2026 academic coursework. This repository chronicles the practical implementation of input/output interfaces, analog sensor data scaling, and signal debugging to bridge foundational physics with practical electrical and computer engineering.

## 🛠️ Technical Skillset & Toolchain
*   **Microcontroller Platform:** Arduino Uno (ATmega328P Core)
*   **Languages & Environments:** Embedded C/C++ / Arduino IDE
*   **Hardware Components:** Solderless breadboards, 16x2 Liquid Crystal Displays (LCDs), HD44780 drivers, TMP36/Thermistors, Photoresistors (LDRs), RGB LEDs, Tilt switches, Linear potentiometers, discrete resistor networks
*   **Core Concepts Proven:** Analog-to-Digital Conversion (ADC), Pulse-Width Modulation (PWM), serial communication, voltage dividers, hardware/software debouncing, sensor calibration loops

---

## 🚀 Technical Project Showroom

### 1. Embedded Digital Stopwatch & Precision Timer
*   **System Architecture:** Developed a standalone digital timer utilizing an LCD panel driven by parallel bit lines. Incorporated a physical tilt/input sensor to alter state-machine tracking dynamically.
*   **Hardware & Interface Layer:** Interfaced a 16x2 Liquid Crystal Display using standard 4-bit data mode pins (`D4-D7`) alongside `Register Select (RS)` and `Enable (E)` control lines. Tuned contrast dynamics using a 10kΩ linear potentiometer acting as a variable voltage divider on the LCD `V0` pin.
*   **Engineering Challenge & Fix:** 
    *   *The Problem:* The LCD displayed corrupted characters and intermittent sync drops when input switches changed states rapidly due to contact bounce and voltage fluctuations.
    *   *The Fix:* Rewrote the execution loop to implement asynchronous software debouncing using time-elapsed tracking (`millis()`) rather than blocking delay loops, completely stabilizing the display data bus.

### 2. Multi-Channel Photometric RGB Color Mixer
*   **System Architecture:** Engineered a closed-loop optical mixing circuit that samples ambient light spectra across multiple zones and remaps the values into a synchronized, color-calibrated light output.
*   **Hardware & Interface Layer:** Constructed three independent ambient light sensing channels using photoresistors (LDRs) wired into continuous voltage divider configurations. Sampled the varying analog voltages via the ATmega328P's built-in Successive Approximation ADC (`A0-A2`), remapped the 10-bit integer array ($0-1023$) into an 8-bit scale ($0-255$), and actively drove a common-cathode RGB LED via hardware Pulse-Width Modulation (PWM) channels.
*   **Engineering Challenge & Fix:**
    *   *The Problem:* Fluorescent room lighting caused severe flickering in the RGB output due to minute analog voltage oscillations on the ADC input pins.
    *   *The Fix:* Implemented a software-based low-pass moving average smoothing filter in the sampling loop, blending the current reading with the previous 5 samples to dampen transient high-frequency noise.

### 3. Thermal Monitoring Interface (Chill-O-Meter)
*   **System Architecture:** Built a calibrated digital thermometer that evaluates ambient temperature variations and handles local threshold sorting via an array of indicator LEDs.
*   **Hardware & Interface Layer:** Sampled continuous voltage drops from an analog temperature sensor. Scaled the raw ADC voltage steps into precision Millivolts, mapped them to Celsius using the standard component baseline ($(\text{Voltage} - 0.5) \times 100$), and managed multi-stage threshold logic to trigger specific output pins.
*   **Engineering Challenge & Fix:**
    *   *The Problem:* The boundaries between threshold tiers caused rapid, rhythmic flickering of the state LEDs when the temperature sat exactly between integer steps.
    *   *The Fix:* Programmed mathematical hysteresis into the conditional comparison statements, requiring the temperature to clear a designated dead-band threshold before altering the output state.

### 4. Interactive Control Panel & State Interface
*   **System Architecture:** Designed a classic physical interface panel that uses a master toggled input switch to swap between normal operating configurations and safe/critical state indicators.
*   **Hardware & Interface Layer:** Configured a pull-down resistor circuit on a tactile momentary digital input switch. Monitored pin states asynchronously to switch a tri-LED notification cluster from idle green to blinking warning configurations.

---

## 📈 Integration with Academic Curriculum
These functional builds directly validate the concurrent coursework in my Electrical and Computer Engineering sophomore sequence:
*   **Principles of Electrical Engineering:** Practical application of Ohm's Law and Kirchhoff's Laws verified via voltage divider circuits and resistor matching.
*   **Digital Logic Design:** Practical observation of state machine structures, binary data paths, logic gate behavior, and truth-table confirmation.
*   **Discrete Math:** Structuring clean, optimized conditional branch logic and algorithmic state structures within code blocks.
