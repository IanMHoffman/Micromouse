# Micromouse Project Introduction

This is a personal project of mine to design, build, and program a new micromouse that will be internationally competitive. I have designed a few for fun using off the shelf components and development boards. This one will be designed on custom PCBs to make better use of space and weight.

* TOC
{:toc}

## What Is A Micromouse?

Many people have not heard of a micromouse. It is a robot designed to solve a maze, like a mouse is often portrayed doing. It is actually the worlds longest running robotic contest introduced by IEEEin 1977. There is are two main micromouse divisions, classic and half size. Regardless of the division each mouse is required to solve the maze completely autonomously. As the mouse navigates the maze it locates and records the locations of the walls. This allows the mouse to solve the maze and pick the shortest, or fastest path to the objective.

### Classic Micromouse

Classic micromouse, often just called micromouse, where the robot has to solve a 16x16 grid of cells. each cell is a 180mm square. The walls of the maze are 50mm high. The mouse starts in a corner and has to make it to the central objective, a 2x2 area centered in the maze. The mice themselves must be able to fit into a 25cm square. There is no height limitation for the robot.

### Half Size Micromouse

Half size micromouse is the newest form of the competition. It was introduced for the 30th All Japan Micromouse Competition in 2009. Unlike classic micromouse this form has a 32x32 grid of cells. The cell dimensions have also been reduced by half to a 90mm square. The size of a half mouse is limited to a 12.5cm square while still having no height restriction.

# Hardware Selection

## MCU (Microcontroller Unit)

This has been a big topic for me. I really want something to experiment on so I am ultimately looking at something fast and powerful. I would also like it to have plenty of extra pins if I decide to try something crazy. I am also a fan of STM32 boards due to information and support available for them. 

Current Selections is a:
### [STM32H743ZGT6](https://www.arrow.com/en/products/stm32h743zgt6/stmicroelectronics)

* Clock Rate: 480 MHz
* Data Bus Width: 32 bit
* Program Memory Size: 1 MB
* RAM Size: 1060 KB
* Interfaces: CAN/I2C/I2S/SPI/UART/USART/USB
* Number of I/Os: 114
* Number of Timers: 20

## Odometry (Encoders)

## Wall Sensors

Traditionally in micromouse walls have been detected using Inferred LEDs. I am going to be a rebel and use something different. I also would like to experiment with looking just barely over a wall to detect the next row and drastically reduce search time.

Current Selections is a:
### [VL6180X](https://www.st.com/en/imaging-and-photonics-solutions/vl6180x.html)

This is a Time of Flight (ToF) sensor that measures the time it takes light to bounce off a object and come back. Unlike a IR sensor that measures the amount of light reflected. These sensors are much more precise and not prone to the problems that plague current robots that perform differently just by changing the ambient light.

In my testing I have been able to run multiple of these sensors, side by side and crossing paths, at once with no interference. They reliably run at a 10 hz sample rate. By tweaking the "READOUT__AVERAGING_SAMPLE_PERIOD" and the "SYSRANGE__MAX_CONVERGENCE_TIME" you can see a 100 hz sample rate.

readout__averaging_sample_period:

The internal readout averaging sample period can be adjusted from 0 to 255. Increasing the sampling period decreases noise but also reduces the effective max convergence time and increases power consumption: 
Effective max convergence time = max convergence time - readout averaging period. 
Each unit sample period corresponds to around 64.5 µs additional processing time. 
The recommended setting is 48 which equates to around 4.3 ms.

sysrange__max_convergence_time:

Maximum time to run measurement in Ranging modes. Range 1 - 63 ms (1 code = 1 ms); Measurement aborted when limit reached to aid power reduction. 
For example, 0x01 = 1ms, 0x0a = 10ms.
Note: 
Effective max_convergence_time depends on readout_averaging_sample_period setting.

## Accelerometer 

## Motors

## Tires