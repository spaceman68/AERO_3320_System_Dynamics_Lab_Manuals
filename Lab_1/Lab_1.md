# AERO 3320 System Dynamics

Author: Stephen Thiam-Choy Kwok-Choon

## Lab 1 Sensor Characterization and Calibration

### Objectives

<!-- justify text - <div style="text-align: justify"> your-text-here </div>     -->

<div style="text-align: justify"> Students will pick a thermistor and build hardware and software systems to take data. The students will be required to discuss sources of error, quantify errors and calibrate sensors. This lab will cover the following topics: </div>

- Sensor Types
- Interfaces
- Analog to Digital Conversion
- Quantization of Error
- Calibration
- Data Acquisition

<div style="text-align: justify"> This lab will provide experience designing, building and implementing hardware and software systems designed to take data. At the completion of this lab you should be able to calibrate analog sensors, use them to record physical properties from the world as well as identify and quantify the sources of error. </div>


### Introduction

<div style="text-align: justify"> Choosing the appropriate sensor for a specific purpose requires knowledge of the characteristics of different classes of sensors and how these different classes of sensors perform in different applications and operating environments. In general, all sensors respond to a physical phenomenon by changing some characteristic of the sensor. For example, the resistance across a thermistor changes as the temperature changes. Clearly, we also must measure resistance which is also a form of a sensor. However, most analog sensors we will deal with in this class convert some physical quantity (temperature, light intensity, distance, pressure) into an electrical signal, typically voltage or resistance. We consider measuring voltage, resistance or current, as a fundamental measurement.

The course text book discusses many different sensor types based on what physical phenomenon you are attempting to measure. Many of these sensor types are beyond the scope of this class, but may be useful further along in your career.

Fundamentally, a measurement systems is comprised of a sensor, a variable conversion element, and some sort of device used to process the information known as a signal processor. Figure 1.1 in the book givens a schematic view of a measurement system. In this class, you will work with a variety of sensors, construct a variable conversion element and program a signal processor to record data. For this lab, the sensor you use will be a thermistor, the variable conversion unit will consist of a voltage divider, and the signal processor will be an Arduino micro controller. The breadboard view for this system is shown in Figure 1 and the wiring schematic is shown in Figure 2. </div>



