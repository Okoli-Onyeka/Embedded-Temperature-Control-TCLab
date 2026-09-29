# Temperature Control Lab Experiment

To run this repository, clone it to your local computer using "git clone https://github.com/Okoli-Onyeka/Embedded-Temperature-Control-TCLab.git"

The Simulink and MATLAB Support Package for Arduino Add-on is required to run the files.

The MATLAB version used for the project is MATLAB 2025a

Note that results will vary due to different response characteristics of the components. The standalone Simulink files can be located in the model folder. Connect Simulink to your Arduino Uno and TCLab kit, and connect the pins indicated in the model to the DC motor, heater, and temperature sensor.

Follow [this tutorial](https://uk.mathworks.com/help/simulink/supportpkg/arduino_ref/getting-started-with-arduino-hardware.html) to learn how to interface Simulink with Arduino Uno.

## The Engineering Story behind the final design - From Initial to Final Concept (in Progress)
This project aimed to design a model in MATLAB and Simulink to control a system's temperature using 2 PID controllers, one for the heater and one for the fan/motor. 

Based on the user input from the dashboard, the system could be controlled at one of two levels: 65 or 45 degrees. 

<img width="1851" height="813" alt="hysteresis" src="https://github.com/user-attachments/assets/9c08284b-fab3-4862-8ae1-76ba23c0f7cb" />

The Image Above shows the final intimidating Simulink model design, but I wish to take you through the process that led to this design so that you can appreciate it more. 

### Initial Algorithm
Firstly, the algorithm of the system's operation was designed as follows

At 45C setpoint

if temperature < 45

  Turn on heater
  
else if temperature = 45

  do nothing
  
else turn on fan

At 65C setpoint

if temperature < 65:

  Turn on heater
  
else if temperature = 65:

  do nothing
  
else turn on fan

From this algorithm, the initial Simulink design was created. At this stage, it was noticed that the algorithm resembled classical control. The condition was basically the error of the system. 

<img width="4032" height="3024" alt="IMG_0474" src="https://github.com/user-attachments/assets/51ee04ed-75b6-418c-869d-979ac7184bc5" />

From the image, a constant block set to 1 is connected to a switch with the 65 and 40 setpoints as inputs. 
The idea is that the constant block can change the system's setpoint. At 0, the switch sets the setpoint to 45, and to 65 at 1. 

Further observation showed the control law is the same for both setpoints; hence the algorithm was compressed to

At setpoint

if error < 0:

  Turn on heater subsystem
  
else if error > 0:

  turn on fan
  
else do nothing

### Latching

Initially, the system seemed to work as expected, yet further observation showed that the fan and heater never turned off after they were turned on. This was perhaps the first bug that was encountered. 

After hours of research and debugging the pins, it was observed that the pins remained in their active state and had to be explicitly turned off when the control condition changed.

To handle this, a switch was used for each subsystem to set the output to zero if the subsystem's condition has not been satisfied. 

<img width="1035" height="777" alt="IMG_0499" src="https://github.com/user-attachments/assets/39549dc3-d60c-4f2f-9f1f-a082ce3fceba" />

#TBC

