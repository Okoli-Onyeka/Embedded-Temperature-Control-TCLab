# Temperature Control Lab Experiment

To run this repository, clone it into your local computer using "git clone https://github.com/Okoli-Onyeka/Embedded-Temperature-Control-TCLab.git"

The Simulink and MATLAB support package for Arduino Add-on is required to run the files.

The MATLAB version used for the project is MATLAB 2025a

Note that results will vary due to different response characteristics of the components. The standalone simulink files can be located in the model folder, connect simulink to your arduino uno and TCLab kit, connect the pins indicated in the model to the DC motor, heater, and temperature sensor.

Follow [this tutorial](https://uk.mathworks.com/help/simulink/supportpkg/arduino_ref/getting-started-with-arduino-hardware.html) to learn how to interface simulink with arduino uno.

## The Engineering Story behind the final design - From Initial to Final Concept (in Progress)
The aim of this project was to design a model in MATLAB and Simulink to control a systems temperature using 2 PID controllers, one for the heater and one for the fan/motor. 

Based on the user input from the dashboard, the system could be controlled at one of two levels, 65 or 45 degrees. 

<img width="1851" height="813" alt="hysteresis" src="https://github.com/user-attachments/assets/9c08284b-fab3-4862-8ae1-76ba23c0f7cb" />

The Image Above shows the final intimidating simulink model design, but I wish to take you through the process that led to this design so that you can appreciate it more. 

### Initial Algorithm
Firstly, the algorithm of the systems operation was designed as follows

...At 45C setpoint..
...if temperature < 45..
  Turn on heater
else if temperature = 45
  do nothing
else turn on fan

At 65C setpoint
if temperature < 65:
  Turn on heater
else if temp34ature = 65:
  do nothing
else turn on fan

From this algorithm, the initial simulink design was created. At this stage, it was noticed that the algorithm resembled classical control. The condition was basically the error of the system. 

<img width="4032" height="3024" alt="IMG_0474" src="https://github.com/user-attachments/assets/51ee04ed-75b6-418c-869d-979ac7184bc5" />

From the image, a constant block set to 1 is connected to a switch with the 65 and 40 setpoints as inputs. 
The idea is, the constant block can be changes the systems setpoint. At 0, the switch places the setpoint to 45 and to 65 at 1. 

Further observation showed the control law is the same for both setpoints, hence the algorithm was compressed to

At setpoint
if error < 0:
  Turn on heater subsystem
else if error > 0:
  turn on fan
else do nothing

A proper toggle switch was also used to replace and simplify the existing design. 

