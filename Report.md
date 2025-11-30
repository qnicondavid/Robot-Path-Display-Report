# Robot Path Display Report
---
## Robot Hardware
The robot utilizes an Arduino-based Adafruit M0 microcontroller, alongside 4 mecanum wheels to move in every direction.
## Task Description
The robot is programmed to record its movements using a pathing logic and display them on the GUI.
## Movement Logic
The movement and position of the robot is calculated within the `stepRobot()` method. It uses the four wheel inputs
  
- `FL` - Front left wheel. 
- `FR` - Front right wheel.
- `BL` - Back left wheel.
- `BR` - Back right wheel.
     
To calculate the following:
  
1. `Vx` - (forward/backwards) velocity variable that gets assigned the value of `((-FL + FR + BL - BR) / 4.0)*-1.0`.
    
2. `Vy` - (sideways/strafe) velocity variable that gets assigned the value of `(FL + FR + BL + BR) / 4.0`.
  
3. `omega` -rotational velocity variable that gets assigned the value of `(-FL + FR - BL + BR) / 4.0`.

Then, a scale variable is made to slow everything down so the robot doesn’t move across the screen too fast.

```cpp
heading += omega * scale;
```
  
Using these variables, the method converts the velocity variables `Vy` and `Vx` into our world's coordinate system using the current heading.
This is done so the robot moves relative to where it's facing and not relative to the screen axes.
```cpp
			double globalX = Vx * Math.cos(heading) - Vy * Math.sin(heading);
			double globalY = Vx * Math.sin(heading) + Vy * Math.cos(heading);
```
Then the movement is added to the robot's current position.

```cpp
			posX += globalX * scale;
			posY -= globalY * scale;
```
At the end, it stores both `posX` and `posY` in a constant List variable `path`. 
