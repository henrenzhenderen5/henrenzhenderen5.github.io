---
title: "Superheterodyne Spectrum Analyzer"
collection: portfolio
permalink: /portfolio/superheterodyne-spectrum-analyzer/
excerpt: "An award-winning spectrum-analyzer project built around a superheterodyne receiver architecture.<br/><img src='/images/portfolio/spectrum-analyzer-cover.jpg' alt='Superheterodyne Spectrum Analyzer'>"
date: 2025-06-01
---

## Overview

**Superheterodyne Spectrum Analyzer** is an electronic-instrument project developed by a three-person team for the 2025 Fudan University Electronic Design Competition. It implements a compact spectrum-analysis workflow around a classical superheterodyne receiver: an RF input is mixed with a swept local oscillator, filtered at a fixed intermediate frequency, converted to a voltage representing signal power, and displayed as a frequency-power trace.

The project received **First Prize** and ranked **first in its competition category**.

![Superheterodyne Spectrum Analyzer](/images/portfolio/spectrum-analyzer-cover.jpg)

## My Contribution

As a core team member, I contributed to the system design, circuit integration, measurement, and iterative debugging of the prototype. The work involved coordinating the RF signal chain with embedded control and display, then validating the analyzer against generated signals at different frequencies and power levels.

## Signal Chain

1. **RF input and low-noise amplification** - The input signal is amplified by cascaded SPF5189Z low-noise amplifier stages to improve sensitivity before mixing.
2. **Swept local oscillator** - An ADF4351 PLL frequency synthesizer generates the local-oscillator signal. The STM32 configures the synthesizer through GPIO-based serial control while sweeping across the selected frequency range.
3. **Mixing and IF selection** - An AD831 double-balanced mixer combines the RF and local-oscillator signals. A 10.7 MHz crystal filter selects the desired intermediate-frequency component and rejects unwanted mixing products.
4. **Power detection and digitization** - An AD8307 RMS/logarithmic detector converts the IF signal power into a DC voltage. The STM32 samples this voltage through its ADC.
5. **Spectrum display** - The controller maps the sampled power to each swept frequency and renders the frequency-power trace on an LCD. The interface also provides controls for signal-source level, center frequency, sweep settings, span, frequency marker, and peak indication.

## Key Design Details

- **Local oscillator:** ADF4351 PLL synthesizer, specified in the report for operation from 35 MHz to 4.4 GHz; a ninth-order Butterworth low-pass filter suppresses harmonic content from the synthesizer output.
- **RF front end:** Two cascaded SPF5189Z amplifier stages were selected for low-level input signals, with an overall measured voltage gain of approximately 50.
- **Mixer and IF:** AD831 mixer with a fixed **10.7 MHz** intermediate-frequency crystal filter.
- **Level control:** A PE4302 digital attenuator provides programmable attenuation; the report demonstrates a 12 dB setting through six GPIO control lines.
- **Detector and control:** AD8307 power detector, STM32 ADC acquisition, and LCD visualization.

## Measurement Range and Calibration

Under the competition test conditions, the analyzer measured continuous-wave signals from **80 MHz to 100 MHz** with a **100 kHz sweep step**. The validated input range was **10 uV to 10 mV RMS**, corresponding to approximately **-87 dBm to -27 dBm**.

The team calibrated ADC readings against input power over this range. The report gives the fitted conversion:

```text
Power (dBm) = 0.04043 x ADC_code - 148.78
```

In the reported test set, more than 70% of samples had a power-measurement error below 0.5 dB; more than 80% were below 1 dB. Frequency identification was reported as exact for more than 98% of samples under the stated test conditions.

## Key Highlights

- Designed and built as a three-person electronic-design competition project.
- Implements a complete RF-to-display measurement chain: amplification, PLL sweep, mixing, IF filtering, RMS/logarithmic detection, ADC acquisition, and LCD visualization.
- Supports adjustable attenuation, frequency sweep, span, frequency markers, and peak display through the LCD interface.
- Awarded First Prize, with first place in the problem category, at the 2025 Fudan University Electronic Design Competition.

## Tools

ADF4351, AD831, SPF5189Z, AD8307, PE4302, STM32, 10.7 MHz crystal filter, LCD, PCB design tools, signal generator, oscilloscope, and soldering equipment.

## Media

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 8px;">
  <iframe src="https://player.bilibili.com/player.html?bvid=BV1Eju56cEPi&page=1&high_quality=1&danmaku=0" 
          scrolling="no" 
          border="0" 
          frameborder="no" 
          framespacing="0" 
          allowfullscreen="true" 
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

## Validation

The prototype was tested by sweeping known single-tone inputs and comparing the displayed peak frequency and power level with the signal-generator settings. The results confirmed that the selected superheterodyne architecture could provide a functional, low-cost spectrum view within the specified 80-100 MHz test band.
