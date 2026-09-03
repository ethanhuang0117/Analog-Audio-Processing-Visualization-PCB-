# Analog Audio Processing & Visualization PCB

A custom analog audio spectrum analyzer PCB that processes microphone audio across 8 frequency bands and displays signal intensity using 4-level LED indicators.

![Completed PCB](images/completed_pcb.jpg)

## Overview

The system captures audio through an electret microphone, amplifies the signal, separates it into 8 frequency bands using active filters, and displays the signal intensity through LED indicators.

**System Block Diagram:**

![System Block Diagram](images/block_diagram.png)

## Features

- 8 frequency bands spanning approximately 80 Hz – 10 kHz
- Cascaded Sallen-Key active filters for improved frequency separation
- Microphone preamplification for low-level audio signals
- Envelope detection to convert AC audio signals into DC levels
- 4-level LED intensity indication for each frequency band using comparators
- USB 5 V single-supply
- Custom PCB designed and assembled in KiCad

## Frequency Bands

| Band | Centre Frequency |
|---|---:|
| 1 | 80 Hz |
| 2 | 160 Hz |
| 3 | 320 Hz |
| 4 | 640 Hz |
| 5 | 1.25 kHz |
| 6 | 2.5 kHz |
| 7 | 5 kHz |
| 8 | 10 kHz |

## Filter Design

The initial design used passive filters, but were redesigned using cascaded Sallen-Key active filters to achieve greater roll-off and band separation.

![Filter Design](images/FilterDesign.png)

## Hardware

### Power

The circuit operates from a 5 V USB supply. Since audio signals oscillate about a center point, a virtual ground of 2.5V is used to allow the analog signal stages to operate from a single supply.

![Virtual Ground Design](images/VirtualGround.png)

### Microphone & Preamplifier

A CMA-4544PF-W electret microphone captures the incoming audio signal, which is amplified using an MCP6004 op-amp to provide a suitable signal level for the filter stages.

The CMA-4544PF-W was chosen because its frequency response of 20Hz-20kHz covers the full audio spectrum.

![Microphone PreAmp Design](images/MicPreAmp.png)

### Envelope Detection

Each filtered signal passes through an envelope detector to convert the AC waveform into a varying DC voltage proportional to its amplitude.

![Envelope Detection Circuit](images/EnvelopeDetector.png)

### Comparator & LED Stage

Comparator circuits divide each detected signal into four amplitude thresholds. The resulting outputs drive four LEDs per frequency band to provide a 4-level visualization of audio intensity.

![Comparator and LED Stage](images/comparator_led.jpg)


## Prototyping & Testing

Individual circuit stages were first tested on breadboards and simulated in Multisim before PCB fabrication.

![Breadboard Prototype](images/breadboard.jpg)

This iterative testing helped identify design issues before fabrication and reduced the need for PCB rework.

## PCB Design

The validated circuit was translated into a custom PCB using KiCad, with component placement, routing, and ground pours optimized for a compact and reliable layout.

![PCB Layout](images/pcb_layout.png)

### 3D PCB View

![3D PCB View](images/pcb_3d.png)

### Schematic

![Schematic](images/schematic.png)

## Results

The completed PCB successfully processes audio through the 8 frequency bands and provides visual feedback through the LED array.

![Completed PCB](images/completed_pcb.jpg)

![PCB Testing](images/final_testing.jpg)

## Design Challenges & Iterations

### Passive → Active Filter Redesign

The original passive filter approach did not provide sufficient frequency separation. Sallen-Key active filters were implemented to improve roll-off and isolation between adjacent bands.

### Gain Optimization

The preamplifier gain was iteratively adjusted during breadboard testing to provide sufficient signal amplitude without excessive amplification of noise.

### Single-Supply Operation

Because the circuit operates from a 5 V USB supply, a virtual ground was implemented to allow the op-amp stages to process audio signals within the available supply range.
