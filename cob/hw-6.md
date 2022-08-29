---
title: Homework 6
layout: cob
---

# Homework 6: Building individual pieces to prepare for our weather-machine final project

Following our discussion in class on Thursday Feb. 27th, **we're going to build an indoor weather machine** to monitor and report atmospheric conditions inside the City of Bridges school space.

The device will have three data-gathering instruments:

1. A PM<sub>2.5</sub> monitor (PM<sub>2.5</sub> is a certain class of especially harmful-to-humans air pollutants—specifically, those which are less than 2.5 microns in diameter)
1. A thermometer
1. A light-level meter

The device will output the measured data via four methods:

1. LCD alphanumeric display to display text and numbers
1. An RGB (red, blue, green) LED which will change displayed color
1. A gauge device, based on a servo motor
1. A speaker which will vary its tone

## Assignment: One input, different outputs

Of the three data-gathering instruments, we only had one on hand as of the date of this assignment, Thursday 2/27. However, all of the outputs were already available. So that we can make some meaningful progress towards building our weather machine next week, we've broken the class into four separate assignments: one per available output.

Each person or team will be responsible for building a machine that uses a **photoresistor input** and a **uniquely assigned output**. (The particular team members' assignments are listed below.)

### Deliverables

1. Each team should come to class prepared to **show their working device**, which actively reads the values from a photoresistor and uses that information to drive an output device.
1. Each team should **paste the code they wrote to [this document](https://docs.google.com/document/d/1yhbf36Ccr1JtWHjRkLxDi6u7bVHyI9NmAq_Pl-F5Fxc/edit?usp=sharing)**. Having all the code in one accessible place will help us combine all of it later.
1. Each team should **draw an electrical schematic** showing how their wired up their system; having these available for reference by the other teams will better allow us to combine the multiple devices together. Bring this schematic to class on Tuesday.

### Teams

* **Akhil** 
    - Input: photoresistor.
    - Output: LCD display [(tutorial link)](https://courses.ideate.cmu.edu/60-223/s2020/tutorials/I2C-lcd). Display should read `light: XXX` where `XXX` is the light level detected.
* **Austin**
    - Input: photoresistor.
    - Output: RGB (red, green, blue) LED. The LED should tend towards red when the light level is low, and tend towards blue when it is high. Everywhere in the middle it should appropriately blend along a continuum. Read about the `analogWrite()` function in the [Arduino reference documents](https://www.arduino.cc/reference/en/language/functions/analog-io/analogwrite/) to get some information about how to do this. See the discussion of how to use the `map()` function in the assignment for [Homework 5]({{site.baseurl}}/cob/hw-5.html) for information about how to turn the photoVal into an appropriate `analogWrite()` value.
* **Husayn**
    - Input: photoresistor.
    - Output: hobby servo. The servo should turn to the 20º position when the light level is at its lowest, and the 160º position when it's at its highest. See the discussion of how to use the `map()` function in the assignment for [Homework 5]({{site.baseurl}}/cob/hw-5.html) for information about how to turn the photoVal into an appropriate degree value.
* **Kai and Phoenix**
    - Input: photoresistor.
    - Output: speaker tone. The speaker should play a higher tone (1000Hz) when the light value is higher, and a lower tone (150Hz) when it's lower. See the discussion of how to use the `map()` function in the assignment for [Homework 5]({{site.baseurl}}/cob/hw-5.html) for information about how to turn the photoVal into an appropriate tone value.
    
### Good luck, everyone! Write me an email if you need help.