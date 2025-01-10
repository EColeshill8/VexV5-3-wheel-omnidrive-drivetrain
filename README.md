# VexV5-3-wheel-robot-drivetrain
A working omnidirectional drivetrain for Vex V5 using only 3 wheels


Hi! Welcome to my repository on a cool drivetrain idea I came up with in the 2023-2024 Vex V5 competition, *Over Under*. First off, unless specified otherwise, all mentioned wheels are Omni wheels, and I refer to my drive base as the tricycle, even though it does not resemble a tricycle. Anyways, the drive base is made of a triangle. The thought behind this was that I could save the weight of a square base, and achieve omnidirectional movement with 2 fewer wheels than an H-drive (where you have a standard 4 wheel tank drive-base and add a fifth wheel in the middle orthogonal to the other wheels). I was trying to lift the bot off the ground on the pole (never quite finished/tested that system unfortunately) and I thought it would help to have a light bot because the motors suck. The code I attached includes code to run other systems on my bot (I had a catapult, front-end ram, and lifter also on the bot), so keep that in mind if you use my code. Also... It's in block code because for some reason I thought it would be easier and quicker than if I used Python (it wasn't). So sorry for that. Also, check out the folder in the repository for photos and videos of the drive-base concept in action!

*Picture of drive base:*

![IMG_4922](https://github.com/user-attachments/assets/c103e936-78fc-4d4a-849b-63a5e110b70c)

This is an image with the front ram attached to the drive base


**Code + Set up:**
The code I made is a vector equation of all factors for each wheel. To get the robot to drive in any direction, I made an equation for each wheel to tell it how much to spin proportionally for any given direction. These equations also include how much each wheel needs to spin if I ask the robot to spin (yaw) as well. There are A LOT of variables that you can tweak in my code, but I will outline the ones you should be tweaking. These are found in the setup "when start" stack. Do not touch anything in the equations themselves!

<img width="253" alt="Screenshot 2025-01-03 at 4 44 35 PM" src="https://github.com/user-attachments/assets/98266051-8849-4639-b46b-07e60679f03d" />

*Right & Left deflection:*
This variable controls the deflection of the wheel relative to the forward/backward (y) axis. You can measure the angle (in degrees) that your right and left wheels deflect from this axis and put your measurements into the respective variables, and the equation will handle the components of spin for you. If you use the same setup I did, you should have a negative Left deflection and a positive right deflection.

<img width="198" alt="Screenshot 2025-01-03 at 4 44 54 PM" src="https://github.com/user-attachments/assets/9575c86d-22ca-4c24-a9c9-fcc740086bbb" />

*Speed or something(SOS)/Speed or something R(SOSR)*
First off I want to apologize for these variable names. I never thought I would put this out there, however it does adequately describe what it does. This variable handles the speed (or something -\_-_-_/- ) of the entire robot. Speed or something (SOS) is in reference to the forward left and right wheels, and speed or something R (SOSR) is in reference to the rear wheel. when SOS is 100, and SOSR is 1, the robot will move at a regular speed. When SOS is >100, and SOSR is >1, the robot will move faster, and if SOS is <100 (and greater than 0) and SOSR is <1 (but greater than 0) the robot will move slower. This stops the motor speed from maxing out (and tuning the robot in case the rear wheel needs more of an effect, although I always left it at 1). But why aren't we always driving forward at max speed if the stick is all the way engaged?? Well, that's because at different points the motors need to run at different speeds even if the robot is moving at the same speed in different directions. So if you max out the motors when you are driving directly forward, for example, they can't drive sideways because that requires one motor speeding up and one motor slowing down. I had a toggle switch on my controller that could override this and set the speed much higher at the cost of having adequate omnidirectional movement so I could just charge ahead and have bursts of speed when I wanted them. You might have to/want to play with these variables, but to be honest, it's probably not necessary unless your robot isn't weighted well and the back wheel needs to add extra power.

<img width="190" alt="Screenshot 2025-01-03 at 4 45 06 PM" src="https://github.com/user-attachments/assets/31dc8982-d0ed-4450-8fda-e256a9720122" />

*Control stick shenanigans:*
Off to the side, there is a stack of statements including the control stick axis 1. I was confused looking at it (it's been almost a year since I made this program), so I figured I would mention what it does here. At first glance, it looks like something to add a dead zone to the controller, and while it is, it is also integral to moving backward. Can't remember what the problem was now, but my solution was to change the equation for forward vs backward movement (and it works quite well. You can see an attached video in the main thread). Do not touch anything in here (unless you want to make the dead zone greater or less, but I found you needed at least 0.05 of dead zone unless it breaks, and I set my values to 0.06). If you do fiddle with it, it could very well break it, and your guess is as good as mine these days for how to fix it. 

<img width="352" alt="Screenshot 2025-01-03 at 4 45 36 PM" src="https://github.com/user-attachments/assets/2e144f98-8fcb-4d63-bec9-0a587ea25594" />

*EQUATIONS FOR EACH WHEEL:*
Rear wheel:

<img width="853" alt="Screenshot 2025-01-03 at 4 46 48 PM" src="https://github.com/user-attachments/assets/2ffdd6a4-f897-4a9a-9209-7c36cb58d618" />

Right wheel:

<img width="948" alt="Screenshot 2025-01-03 at 4 47 43 PM" src="https://github.com/user-attachments/assets/4fb3cfb7-69b8-4562-a6e4-63396b53db64" />

Left wheel:

<img width="923" alt="Screenshot 2025-01-03 at 4 48 03 PM" src="https://github.com/user-attachments/assets/0be2f038-ea35-4191-9b04-6605a9c01d4c" />

Unless you want pain, don't touch these equations...


**Autonomous mode**
So to be totally honest I don't think I ever ended up running an auto mode. However I did build the framework for it (for the most part), and you are more than welcome to try it out. I tried to make it as easy as possible to use, so I just used the same wheel equations as before but changed the inputs to be from a script instead of the controller. I used a little equation to take a vector (in degrees) and set it into components that the equations understand (as it's the same way the controller input works), and input those components into an equation. This way the user has to only specify the direction of travel, the time duration, and any other information they want to include (like stopping or other motor actuation). Below I included an example I had kicking around somewhere. Just hook that up in any way you want and (theoretically) it will drive autonomously. Unfortunately, that's as much help as I can give you with autonomous driving, but if you choose to pursue it, good luck! And if you are super stuck/have something cool to show me, send me an email at encoleshill@icloud.com.

Wheel equations for auto mode:

<img width="711" alt="Screenshot 2025-01-03 at 4 49 12 PM" src="https://github.com/user-attachments/assets/ed5c126d-ff3b-45c4-89ee-c3e4ca679553" />

Vector component equation:

<img width="254" alt="Screenshot 2025-01-03 at 4 58 16 PM" src="https://github.com/user-attachments/assets/2fb32056-36bc-46a1-b1ff-3c2973d84af0" />

Autonomous drive script:

<img width="161" alt="Screenshot 2025-01-03 at 4 57 08 PM" src="https://github.com/user-attachments/assets/58a47b3f-d4b7-44cc-9e02-16c2d84479ab" />

Note: You have to control spin by simply telling each motor to spin in a direction. Never got around to implementing that fully...



**Closing statement**
First of all, thank you for reading, and good luck if you choose to build this yourself. If you have any questions or comments, you can reach me more reliably at encoleshill@icloud.com. Don't hesitate to reach out (I'm an engineering student now, so I'm pretty busy, but I will do my best to get back to you in a timely manner). I originally designed this with high customizability and ease of use so that I could share it with others, and I want nothing more than for people to use, modify, and improve my design. All parts of the drivetrain and code were developed and made solely by me (I haven't seen a drive base like this anywhere else before, but not to say it's the first one out there). With that, check out the code, videos, and photos in this repository if you haven't already, and have a great day! Good luck!
