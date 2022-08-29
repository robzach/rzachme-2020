---
title: Homework 5
layout: cob
---

<style>
    td, th {
        padding: 0.25em;
        border: solid;
        border-width: 1px;
        }
    table {
        margin-left: 2em;
        border-collapse: collapse;
        }
    pre {
        margin-left: 3em;
        }
</style>

# Homework 5: New Combinations

*due Thursday 2/27*

## Part 1: Ideation *(do this part first!)*

*As copied from Homework 4—this discussion is critical and I want to be sure we can figure something meaningful out on Thursday*

We're going to be building something in the next week and a half. We'll make something that will *measure something*, for a scientific or knowledge-building purpose. I want to talk seriously on Thursday about what that thing might be, and so to see some ideas for this part of the homework, I'd like you to look up some examples of scientific apparatus (really just sensors) to get an idea of the variety of things people have made using the Arduino: [here's a collection of a lot of examples from the main Arduino project site](https://create.arduino.cc/projecthub?category=sensors-environment&sort=trending).

### Deliverable: written ideas

Please **come to class with three ideas for sensors or apparatus for us to make.** Write these down. Each idea should include:

* A title of the sensor/apparatus
* A sentence or two description of what the sensor/apparatus will do
* A block-diagram style drawing of the inputs and outputs you'd like the device to use

We'll discuss all of these on Thursday. The more ideas we have to discuss, the better we can plan what we want to build!

## Part 2: Technical assignment *(work on this only after completing part 1)*

1. Select at least one input of interest.
2. Select at least one output of interest.
3. Combine these inputs and outputs, via the Arduino, so that the input(s) control the output(s) in some way. While your device is working, send the input and output data to the computer via the serial monitor.

### Deliverables

1. Working machine that reads an input and actively changes an output
2. Hand-drawn block diagram showing the flow of information
3. Hand-drawn electrical schematic showing your circuit

### Notes

Here is a listing of the inputs we've learned so far (as of the end of class on 2/25), as a refresher:

* potentiometer
* momentary tactile pushbutton
* photoresistor
* HC-SR04 ultrasonic ranger

Here are the outputs we've learned so far:

* light-emitting diode (LED)
* hobby servo motor
* small speaker
* serial feedback on the computer

Not counting the serial feedback as an output, there are therefore 5 possible inputs &times; 3 possible outputs = 15 possible combinations. But that's if you only use *one* output with *one* input! Lots more possibilities emerge if you use multiple inputs or outputs, which you are welcome to do for this assignment.

### Using the `map()` function to change one range into another

Let's say you have an input like a potentiometer that will have a range of, say, 0–1023. You want to use it to affect (i.e. drive) an output that has a different range, such as a dimmable LED. (This would use the `analogWrite()` function, which has a range of 0–255.)

You can use a built-in function called `map()` to automatically turn one range into the other. At at minimum, it will need to do:

input range | output range
--- | ---
0 | 0
1023 | 255

But what about all the stuff in the middle? That's where the `map()` function really helps out: it will automatically turn, in this case, an input value of `512` into an output value of `128` (this is the halfway point for each scale).

In this instance, the function would be constructed:

```c
map(potVal, 0, 1023, 0, 255);
```

Note that there are five values inside the parentheses. These are, in order:

1. The number to change
2. The minimum value of the input range
3. The maximum value of the input range
4. The minimum value of the output range
5. The maximum value of the output range

Finally, to complete the use of the function, you need to simply load the resulting value into a variable (or it will be lost—that would be like doing `analogRead(POTPIN)` instead of `int potVal = analogRead(POTPIN)`). So the complete use would look like:

```c
int LEDVal;
LEDVal = map(potVal, 0, 1023, 0, 255);
```

Now `LEDVal` contains the result of the `map()` function, and you can use it to change the LED's brightness, i.e.:

```c
analogWrite(LEDPIN, LEDVal);
```


### Code structure thoughts

Here's an example structure to serve as a framework when you're thinking about writing code to run your device:

#### Above the `setup()`

* Write a brief comment that explains what this code does
* Make your pin assignment variables.

#### In the `setup()`

* Do all your `pinMode()` declarations.
* Turn on serial communication.

#### In the `loop()`

1. Read input variables, set up output variables
2. Do the math needed to drive your outputs
3. Drive your outputs
4. Send data back to the user via the serial monitor

#### Sample code implementing the above pattern

```c
// this code reads a potentiometer and turns on an LED when it is above a certain level

const int POTPIN = A0;
const int LEDPIN = 6;

void setup() {
  pinMode(POTPIN, INPUT);
  pinMode(LEDPIN, OUTPUT);
}

void loop() {
  // 1a. Read input values and load into variables
  int potVal = analogRead(POTPIN);

  // 1b. Set up output variables as needed
  int LEDVal = LOW;

  // 2. Do math or make decisions
  // (i.e. change output variables as needed)
  if (potVal > 400) {
    LEDVal = HIGH;
  } else {
    LEDVal = LOW;
  }

  // 3. Drive outputs
  digitalWrite(LEDPIN, LEDVal);

  // 4. Report back to the user
  Serial.print("potVal = ");
  Serial.print(potVal);
  Serial.print(", LEDVal = ");
  Serial.println(LEDVal);
}
```


#### Sample code using the above pattern and the `map()` function

```c
// this code reads a potentiometer to change an LED's brightness

const int POTPIN = A0;
const int LEDPIN = 6;

void setup() {
  pinMode(POTPIN, INPUT);
  pinMode(LEDPIN, OUTPUT);
}

void loop() {
  // 1a. Read input values and load into variables
  int potVal = analogRead(POTPIN);

  // 1b. Set up output variables as needed
  int LEDVal = 0;

  // 2. Do math or make decisions
  // (i.e. change output variables as needed)
  LEDVal = map(potVal, 0, 1023, 0, 255);

  // 3. Drive outputs
  analogWrite(LEDPIN, LEDVal);

  // 4. Report back to the user
  Serial.print("potVal = ");
  Serial.print(potVal);
  Serial.print(", LEDVal = ");
  Serial.println(LEDVal);
}
```