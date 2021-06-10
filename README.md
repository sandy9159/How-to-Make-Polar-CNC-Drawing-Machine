# How-to-Make-Polar-CNC-Drawing-Machine

Hello friends welcome back in this new instructbales

Here I have made a simple Polar CNC drawing machine, I kept is as simple as possible complete structure is made out of wood.

I avoid to use 3D printer to keep it simple, so anyone can made it. So basically you think what is polar CNC means, 

so I will tell polar CNC's are quit different in comparison of traditional CNC,

Polar CNC are work in 360 degree format while traditional CNC are work in Cartesian coordinate system like X, Y & Z axis. 

In this this machine the Y axis (turn table) is polar format,

I have used a Custom made PCB to give professional look to my project, I ordered my PCB from JLCPB.COM they have very affordable rates for PCB like 2$ for 10PCB

Also there are not charging any extra fees for color PCB. $2 for 10 PCBs (Any Color): https://jlcpcb.com

## WHAT IS POLAR CNC MACHINE ##

So first of we have a question in mind that what is polar CNC right, and how it is different from our 
standerd CNC machine.

SO let me explain you in normal 2 or 3 Axis CNC machine all axis are have liner motion only.
Like X-axis moves left & right Y-axis movies backward and forward, and Z - axis moves UP & DOWN
But in this polar CNC machine the table of CNC machine

or the Y-axis of CNC machine is not moving left and right or backward & forward 
it is moving in circular motion, yes Y-axis is directly connected with the stepper motor
stepper motor rotates the Y--axis in circulation path.

## VIDEO ## 

This is the link of video you can watch the complete 

making process of polar CNC drawwing machine 
https://youtu.be/dl_XWb1AK2U

##  COMPONENTS ##

Arduino Nano :- https://amzn.to/2UOWLMW

Nema 17:- https://amzn.to/2TNPUa8

Servo :- https://amzn.to/2TZqUfw

## STEPPER MOTORS ##

We have used 2 stepper motors in this project one for X -axis and one for Y-axis
I have choosen the NEMA 17 version of stepper motor
this stepper motor is drive through the A4988 stepper driver IC


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

## CUSTOM MADE PCB ## 


PCB is the heart of this project, I have design like all the components must be surface mount on PCB so there is a big challenge is in front of me how to manage to buy different different components on my own. it quite difficult to get them all in time. so i came to know about PCB + SMT service of JLCPCB.COM like JLCPCB offering complete PCB with components solder on it. they have huge collection of components to choose from. this was so much help full for me it save my lots of time and money by using PCB + SMT service of https://jlcpcb.com/IAT and now there is also one good news for you you can now earn 10$ coupon for from JLCPCB just use https://easyeda.com/editor to design your PCB and order it from https://jlcpcb.com/IAT Design & Order on EasyEDA, PCB+SMT $10 Off: https://easyeda.com/editor Get $10 coupon & Join JLC&EDA Group: https://jlcpcb.com/EDA https://www.youtube.com/watch?v=rUtlYrG-U5g Watch full video https://www.youtube.com/watch?v=R9FUyvKBm8k
