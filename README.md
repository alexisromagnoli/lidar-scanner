Demo: https://www.youtube.com/watch?v=kJW9Uy4j-6k

# Introduction
The goal of this project was to use a rangefinder mounted in servos, which would rotate and allow it to measure different parts of the room. The angles and distances are sent in real time to the computer that reads, converts and creates a 3D scene of the place. In the end, it works like a 3D scanner of the room and any object inside.

We first tried using a sonar rangefinder to make the distance measurements, but even using a sonar with a narrow beam, it was not narrow enough to make precise readings. Furthermore, the waves emitted by the sonar would bounce on angled surfaces and give wrong readings. To overcome this problem we used a LIDAR (laser-based range finder), which is very accurate, has an extremely narrow beam and won’t bounce off surfaces. The only downside is that it is not so precise with shiny surfaces and cannot make readings against transparent surfaces, such as windows, but it is good enough for the purpose we need.

# The Project
The project can be roughly divided in three parts: electronics, arduino programming and the interface programming.

## Electronics
To build the prototype we used two servo motors (model HS-422), which are capable of rotating 180 degrees and keep track of their position. As the rangefinder we used a LIDAR-Lite, the most affordable LIDAR we were able to find, but still an excellent product for its price. Everything was powered by power bank and controlled by an arduino. The schematics can be found in our blog.

## Arduino
The code run by the arduino is pretty straightforward. It moves the servos (keeping track of its position) and reads the distance from the sensor after every movement. Every time it reads the distance, a string is sent through the serial port with information from the distance and the servos position. One of the problems encountered was that reading from the sensor inside nested loops would create unexpected behaviour of arduino, so the logic had to be changed to iterate over servos position using only the arduino built-in loop() function.

## Interface
The computer interface for the prototype, written using C++ and OpenGL, reads the data sent by the arduino, analyses, convert to Cartesian coordinates and plots to the screen. Each point is created in the screen as a cube with its colour varying depending on distance and angles. The interface is also responsible to communicate with arduino and send a starting code, telling the prototype to start scanning. All the scans are shown in the screen in real time, as the distances are being read and transmitted. It is possible to navigate in the 3D view while the scanning is taking progress. The software allows saving the scan to a file and loading it later. A preview of the saved files is available to make it easy to select the desired scan.

# Links
During the development we maintained a weekly report in the project blog. More info can be found there, and also links to our presentation, the github repository for the code and also a time-lapse video with the working prototype.
http://lidarscanner.wordpress.com
