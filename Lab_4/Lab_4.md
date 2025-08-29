# AERO 3320 System Dynamics
Maintenance: Stephen Thiam-Choy Kwok-Choon

Email: skwokcho@calpoly.edu

Original Author: Leonardo Torres

# Lab 4: Regulation and Arduino Libraries

**Closed Loop Control**

## 1. Objectives

Students will learn to connect and gather data from an accelerometer using a library. Students will use the accelerometer data to measure the roll angle of the accelerometer and regulate the armature position of a servo motor. This lab will cover:

- Importing and using an Arduino library
- The basics of object oriented programming
- Calculating the roll angle from an accelerometer reading of the gravity vector
- Regulating the armature position of a servo motor using proportional feedback

## 2. Introduction

There are several more advanced coding concepts we will cover with this lab. These more advanced concepts include:

- Code refactoring: https://en.wikipedia.org/wiki/Code_refactoring

- Importing and using Arduino libraries: https://www.arduino.cc/en/Reference/Libraries

- Class definitions and objects: http://www.geeksforgeeks.org/c-classes-and-objects/


Each of the above links goes into some detail that might not have significance for you now. Read the rest of the lab manual and then head back to those links for further insight. Let’s start with code refactoring

### 2.1. Code Refactoring

In lab 3, you wrote separate functions outside the setup() and loo() functions which you then called from the loop() function. The basic idea was to take a chunk of code you used in the loop() function and then move it to some other function defined outside the loop() function. You can then call the new function from the loop() function. The code below is an example of this concept for the servo.

<div style="color:black; background:lightblue; border: 1px dashed black">

``` 
// ORIGINAL SERVO MOVE CODE 
int servoPin = 2; // Define the digital pin number 
int pulse = 1200; // Define the pulse width in microseconds 

void setup() { 
    //Set digital pin mode as an output pin 
    pinMode(servoPin, OUTPUT);
    
} 
    
void loop() { 
    digitalWrite(servoPin, HIGH); //Write a HIGH value to digital
    pin delayMicroseconds(pulse); //Wait desired pulse time
    digitalWrite(servoPin, LOW); //Write a LOW value to digital
    pin delayMicroseconds(20000); //Wait 20 milliseconds 
}
``` 
</div>


<div style="color:black; background:lightblue; border: 1px dashed black">

``` 
// REFACTORED SERVO MOVE CODE 

int servoPin = 2; // Define the digital pin number 

void setup() {
    pinMode(servoPin, OUTPUT);//Set digital pin mode as an output pin 
} 

void loop() {
    // Define the pulse width in microseconds
    int pulse = 1200; 
    servoMove(pulse); 
} 

void servoMove(int pulseLength) {
    //Write a HIGH value to digital pin
    digitalWrite(servoPin, HIGH);

    //Wait desired pulse time
    delayMicroseconds(pulseLength);
    
    //Write a LOW value to digital
    digitalWrite(servoPin, LOW);  
    
     //Wait 20 milliseconds
    pin delayMicroseconds(20000); 
}
``` 
</div>

There are a few things to notice. First, and most obvious change is the addition of the function servoMove(). Remember, a function definition includes a return type, followed by the function name, and then a list of input type and input name pairs separated by commas. In general,

<code>returnType functionName(inputType1 inputName1, inputType2 inputName2, …). </code>

In the code above, the return type is <code>void</code> meaning no variable is returned and the function name is <code>servoMove</code>. There is only one input of type <code>int</code> and the input name is <code>pulseLength</code>. It is important to
remember that the variable <code>pulseLength</code> is now a local variable and is only defined in the function <code>servoMove</code>.
The second change to the code is now the loop defines the variable <code>pulse</code> and then calls the function <code> servoMove </code> instead of the four lines of code used to move the servo. If you were to follow the execution of this code line-by-line, you would see the lines of code are executed in the exact same order for both sets of code. So why bother refactoring?

The most obvious reason is compartmentalization. Imagine a scenario where you needed to make move the servo several times in different ways each time through the loop. Look at the example code below. Notice less code is needed and the loop function is very clear compared to if all the commands to move the servo were in the <code>loop()</code> function.


<div style="color:black; background:lightblue; border: 1px dashed black">

``` 
// BENEFITS OF REFACTORING 

// Define the digital pin number 
int servoPin = 2; 

void setup() { 
    //Set digital pin mode as an output pin 
    pinMode(servoPin, OUTPUT);
} 

void loop() { 
    servoMove(1200); 
    delay(100); 
    servoMove(1800); 
    delay(100); 
    servoMove(600); 
} 

void servoMove(int pulseLength) {
    //Write a HIGH value to digital pin
    digitalWrite(servoPin, HIGH);

    //Wait desired pulse time
    delayMicroseconds(pulseLength);

    //Write a LOW value to digital
    digitalWrite(servoPin, LOW); 

    //Wait 20 milliseconds 
    pin delayMicroseconds(20000); 
}
``` 
</div>


Another reason compartmentalizing your code is useful is because we can test the functionality of the <code>servoMove</code> function independently from the <code>loop()</code> function. This idea is known as unit testing. 

Once we know the <code>servoMove</code> function is fully tested and works, we can store it away and use it any time we want in the future. This leads to the concept of libraries.

### 2.2 Importing and Using Arduino Libraries

The idea of an Arduino library is simple once we appreciate the value of refactoring code. Let’s say you wrote a whole bunch of extra function that allow you to do all sorts of things with a specific sensor or actuator. You have all these functions included in some Arduino code and your code works great for your current setup. But now, you want to use the same sensor or actuator in a different set up, but you keep all the functionality you created in your refactored code. What if there was a way to save all this code in some other place and then simply import the code into your new Arduino sketch? We there is. It’s known as a library!

In fact, you have already been using a library. Every Arduino sketch includes the Arduino library be default. All the commands you have been using for serial communication are in the Arduino library. But what if you want to include a different library? Either one included with the Arduino language, or the custom library you wrote for your sensor? The way you include some other set of code (or library) is to use the #include command.

For example, Arduino actually includes a library designed to run servo motors. Please don’t be mad… The code below is an example of using the Arduino servo library.

testing changes