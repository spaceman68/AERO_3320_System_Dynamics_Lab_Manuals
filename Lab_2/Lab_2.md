# AERO 3320 System Dynamics

Maintenance: Stephen Thiam-Choy Kwok-Choon

Email: skwokcho@calpoly.edu

Original Author: Leonardo Torres

# Lab 2: Measurement Uncertainty, Noise and Filtering

## 1 Objectives

Students will take results from the readings of a digital sensor to characterize the measurement noise and design filters to reduce the impact of systemic and random noise. This lab will cover the following topics:
- Characterize the systematic and random errors in measurement data from a digital sensor
    - Repeat parts of lab 1 as necessary
- Implement procedures to reduce systematic errors
- Implement a digital low-pass filter to reduce random errors in data
- Measure several quantities to calculate a physical quantity
    - Propagate errors in calculation

## 2 Introduction

In lab 1, we used the Arduino platform and Matlab to take data from an analog thermistor. When the temperature is relatively constant, the reading from the thermistor is also relatively constant. However, if you look closely at the data, you will see small variations in the temperature readings even though there is no real change in the actual temperature of the room. As described in chapter three of the text book, these variations are classified random errors. The fact that you had to calibrate the sensor because of the tolerance of the resistor in your voltage divider is a *systematic error*. **Please read sections 1 through 5 of Chapter 3**. The book has a good discussion on these issues. In this lab, you will look into the systematic and random errors of an ultrasonic distance sensor. 

For more on these sensors, see the following: https://en.wikipedia.org/wiki/Ultrasonic_transducer, and https://www.sparkfun.com/products/13959.

### 2.1 Digital Sensors