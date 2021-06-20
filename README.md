# How-to-Make-Polar-CNC-Drawing-Machine

![ll](https://user-images.githubusercontent.com/19898602/122661036-e3673b80-d1a3-11eb-83cb-bafaa1b04d45.jpg)


Hello friends welcome back in this new instructbales

Here I have made a simple Polar CNC drawing machine, I kept is as simple as possible complete structure is made out of wood.

I avoid to use 3D printer to keep it simple, so anyone can made it. So basically you think what is polar CNC means, 

so I will tell polar CNC's are quit different in comparison of traditional CNC,

Polar CNC are work in 360 degree format while traditional CNC are work in Cartesian coordinate system like X, Y & Z axis. 

In this this machine the Y axis (turn table) is polar format,

I have used a Custom made PCB to give professional look to my project, I ordered my PCB from [JLCPCB](JLCPCB.COM) they have very affordable rates for PCB

Also there are not charging any extra fees for color PCB.
They have Special offer of $2 for 1-4 Layer PCBs, free SMT assembly monthly.
If you get yourself registered today at [JLCPCB](JLCPCB.COM) you get 18$ welcome coupon from [JLCPCB](JLCPCB.COM).


## WHAT IS POLAR CNC MACHINE ##

So first of we have a question in mind that what is polar CNC right, and how it is different from our 
standerd CNC machine.

SO let me explain you in normal 2 or 3 Axis CNC machine all axis are have liner motion only.
Like X-axis moves left & right Y-axis movies backward and forward, and Z - axis moves UP & DOWN
But in this polar CNC machine the table of CNC machine

or the Y-axis of CNC machine is not moving left and right or backward & forward 
it is moving in circular motion, yes Y-axis is directly connected with the stepper motor
stepper motor rotates the Y--axis in circulation path.

## Polar Pen Machine Kinematics
When you have a round work piece like a drink coaster, it makes sense to have a round work area. 
A round work area works best with a polar coordinate system. A polar coordinate system uses an angle 
and a distance from a center point to define a point in 2D.


![250px-Polar_graph_paper svg_](https://user-images.githubusercontent.com/19898602/122660870-828b3380-d1a2-11eb-8959-23e185739cad.png)

The problem is that most drawing and CAM programs work in Cartesian (X,Y,Z) coordinate systems. 
My machine controller firmware, Grbl, also works in normal linear X,Y, and Z. The process of converting one system to another uses Kinematics.

## The Firmware

![drawing1-300x209](https://user-images.githubusercontent.com/19898602/122660923-faf1f480-d1a2-11eb-9087-8c035dc5bf3d.jpg)

The firmware is side is actually quite easy. I defined the X axis as the distance in mm from the center (the radius). 
The Y axis will control the angle. The Y axis is setup so that millimeters will equal degrees. If I tell the Y to move 360mm, 
it will actually rotate the work area by 360°.  I could have used radians, but my brain works a lot slower in radians.

The machine will only need to home on the X axis. It needs to know where the exact center of the work area is. 
The starting angle does not matter because the coaster is a circle.

The conversion from X, Y to polar is probably won’t fit in into the firmware, so the X, Y conversion is done in a preprocessor software program. 
The X,Y gcode is output from normal CAM programs, then run through a conversion program.

The Conversion Program
The program reads the X,Y gcode, converts any X or Y coordinates into polar coordinates and outputs a new gcode file. The sender simply sends the new files.  The math is actually quite simple.





Typical Gcode sends line data by giving the end points of lines. You simply draw from one point to the next, unfortunately this creates a few problems with a non linear machine.

The basic non-linearity problem
If we were trying to draw the green square centered on the work area, the generated gcode would basically send the corner points. Each corner point has an equal radius to the center. Therefore, the pen will never change radius when going to the next point. This will result in a circle. We want the green square, but we get the red circle.

![nonlinear-300x290](https://user-images.githubusercontent.com/19898602/122660936-1b21b380-d1a3-11eb-8714-aeb20a74b3c6.jpg)


We need to calculate each point along the way to stay on the desired path. The preprocessor divides the line into tiny segments. Each segment has the same problem, but at a scale you won’t be able to see.

The Spiral Problem
If we are drawing a shape that crosses the 0° angle we don’t want the angle to spin the wrong way. If a point is at 350° and the next point is 10° (crosses over 0) we don’t want it to spin backwards from 350° to 10°. We want it to go to 370°.  It happens anywhere the angle difference between 2 points is greater than 180°. The program will choose the shortest direction even if that means going above 360° or below 0° degrees.

![spiral-300x290](https://user-images.githubusercontent.com/19898602/122660955-3b517280-d1a3-11eb-989a-f0aaf6a4c8da.jpg)

The Feed Rate Problem
Feed rate, in CNC terms, is the speed of the tool across the material. The CAM software is setting the feed rate as if this were a Cartesian machine. On this machine, if you were drawing a circle, you would simply move 360 units in Y. Without compensating feed rate, the pen would move across the work piece faster for larger diameter circles. I want to do some sort of compensation to help with this. The coasters are very absorbent, so the  lines look thicker if the speed is slower. A consistent speed will help the quality of the work.

![perimeters-300x245](https://user-images.githubusercontent.com/19898602/122660971-53c18d00-d1a3-11eb-8b36-fd36f80bf9e3.jpg)


Since the lines are all very short, the easiest way to compensate for feed rate is to use the current radius. With a simple circle, Grbl thinks the machine moved 360mm. The real distance is easy to to calculate from the perimeter of that circle.



We can compare it to the 360mm (full circle) and apply the ratio to the desired feed rate from the CAM program.

polarFeedrate = cartesianFeedrate * 360 / (2 * pi * radius)

## VIDEO ## 

This is the link of video you can watch the complete 

making process of polar CNC drawwing machine 
https://youtu.be/dl_XWb1AK2U

##  COMPONENTS ##

Arduino Nano :- https://amzn.to/2UOWLMW

Nema 17:- https://amzn.to/2TNPUa8

Servo :- https://amzn.to/2TZqUfw

## CUSTOM MADE PCB ## 

![A1](https://user-images.githubusercontent.com/19898602/122661273-072b8100-d1a6-11eb-83c0-a3c0f18c33e6.JPG)
![GG](https://user-images.githubusercontent.com/19898602/122661293-42c64b00-d1a6-11eb-88f6-bb288238f309.JPG)

Making such projects without PCB is night mare yes trust me
you cannot get wanted result and professional touch in your project if you ignore PCB
So some days back I have developed my Multipurpose PCB. and order it from [JLCPCB](JLCPCB.COM)
This PCB is used to build wide range of arduino projects 

This PCB is specialy designe for CNC machine it have two L293D IC which control two stepper motors
and provision for micro servo motor

List of the Components you can connect to the PCB

1. 2 stepper motors
2. 1 servo motor


![PCB](https://user-images.githubusercontent.com/19898602/122661250-e2370e00-d1a5-11eb-9c0c-a2b0507c6798.jpg)

## STEPPER MOTORS ##

We have used 2 stepper motors in this project one for X -axis and one for Y-axis
I have choosen the NEMA 17 version of stepper motor
this stepper motor is drive through the A4988 stepper driver IC

![c1](https://user-images.githubusercontent.com/19898602/122661366-2a0a6500-d1a7-11eb-98b1-7f7d3666bb07.JPG)

I have mostly build all parts of this CNC machine from wood
I have cut 4mm wooden sheet in circular shape of 100mm diameter


![c2](https://user-images.githubusercontent.com/19898602/122661367-2e368280-d1a7-11eb-8a3f-140b96be2002.JPG)

Here I have prepared a wooden base from a wood log I have made a grove for
Stepper motor and drill some holes to pass T8 lead screw from it.
I also placed a 8mm flange bearing at the top portion of wooden block to
Hold T8 lead screw straight.



![c3](https://user-images.githubusercontent.com/19898602/122661368-2ecf1900-d1a7-11eb-9481-49e39f58fb86.JPG)

Here I placed the circular table on the T8 lead screw further this circular table 
Is connected with stepper motor with the help of timing belt



![c4](https://user-images.githubusercontent.com/19898602/122661369-2ecf1900-d1a7-11eb-8cf7-8543c5bb9c9a.JPG)

In the same way I prepare the wooden structure for Y-axis, I drilled 8mm hole in
Wooden block and place them parallel on Y-axis structure.
This will hold the 8mm rod of Y-axis 


![c5](https://user-images.githubusercontent.com/19898602/122661370-2f67af80-d1a7-11eb-9504-64aa099eb179.JPG)

At last I mounted PCB on the back side of Y-axis and connected both stepper motors and one servo motor with PCB


## SOFTWARE & FIRMWARE ##

I use a modified version of Grbl 1.1f.  Grbl does not support servos, so I needed to hack that in.  

I used the PWM that is normally used for the spindle speed to control the servo. I turned off the variable speed spindle option and streamlined the spindle functions to the bare minimum I thought Grbl needed.  I adjusted the PWM parameters for use with a servo and added pen_up() and pen_down() functions. 

I tried to put as much of the custom code into one file spindle_control.c. I had to add a few lines in stepper.c to look at the current machine Z height and apply the correct pen up/down function.

ou need arduino IDE to upload code to arduino

and need a special software to process normal G-code to polar G-code Special thanks to bdring they have 

developed a software which can convert normal G-code into Polar G-code..

http://www.buildlog.net/blog/2017/08/...

Firmware : -http://www.buildlog.net/blog/2017/08/...

G-code processor :- http://www.buildlog.net/blog/wp-conte...



