# Robot Path Display Report
---
## Robot Hardware
The robot utilizes an Arduino-based Adafruit M0 microcontroller, alongside 4 mecanum wheels to move in every direction.
## Task Description
The robot is programmed to record its movements using a pathing logic and display them on the GUI.
## Movement Logic
The movement and position of the robot is calculated within the `stepRobot()` method. It calculates 3 variables based on the four wheel inputs `FL`, `FR`, `BL`, and `BR`.
- `Vx` - transitional velocity variable that gets assigned the value of `(-FL + FR + BL - BR) / 4.0`. 
- `Vy` - transitional velocity variable that gets assigned the value of `(FL + FR + BL + BR) / 4.0`.
- `omega` -rotational velocity variable that gets assigned the value of `(-FL + FR - BL + BR) / 4.0`.

Using these variables, the method then figures out the heading and position of the robot using trigonometry.
```cpp
heading += omega * scale;

			double globalX = Vx * Math.cos(heading) - Vy * Math.sin(heading);
			double globalY = Vx * Math.sin(heading) + Vy * Math.cos(heading);

			posX += globalX * scale;
			posY -= globalY * scale;
```
