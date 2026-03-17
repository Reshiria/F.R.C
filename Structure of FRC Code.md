FRC code has a bit of a unique structure.

To understand how the software begins to interact with the hardware. First, the moment you hit deploy, the GradleRIO system starts(Gradle is the software that packages your code to a usable state. You WILL have Gradle problems. It's inevitable.) and packages your code into a .jar. 

The exact process is that the gradle builds then sends.

Building refers to the process of transferring human words to robot binary, connecting libraries, and packing into a .jar.

The files are copied onto the RoboRIO. This is why, you need to deploy after every change if you want it to reflect.

Then, on the RoboRIO, a Linux system starts the Robot.

WPILib starts the hardware abstraction layer(HAL) which connects to all the controllers, power distributors, and CAN.

The robot code is then instantiated, before running robotStart in Main, the entry point.

In the constructor of Robot, the robot itself is instantiated once. This is where your logger, data senders, command logging, and robot container should go.

Frankly all this section is kind of hard to understand, and most certainly NOT necessary to know about. I think most teams(like atleast 95%) can get by without properly understanding this whole section. However, this is all setup for this.

FRC code runs on a 50hz loop(20ms) meaning that it cycles through the periodic every 20ms. Every command, action, and computation occurs within that 20ms loop. If it doesn't it runs on, interrupts other processes, and causes problems. Don't leak cpu kids.

Every 20ms, everything in Robotcontainer's "containers" are called. In the constructor(bc they only run once) all subsystems should be defined. In the containers, the subsystems should run commands.

You might at this point wonder what a command or subsystem is.

A subsystem is a software implementation of hardware. It is in short defining motors, gears, and belts so that the code knows what the hardware can do. Commands are the code actually telling the subsystems what to do, but organized in a scheduled fashion.

Below is a simplified model of how the whole structure is set up. There are many ways to structure your code but this is the one I'm most intimately familiar with and would recommend.
![[Pasted image 20260317124353.png]]

This is the key point to take note of: your job with coding for the most part, pertains towards making subsystems, commands, and calling them. Using the various tools the command scheduler offers, you can do cool operations like shoot on the move and raise the intake while driving.

TLDR:
The robot code interacts with the hardware through packaging and gradle. During this process, the robot itself is instantiated, with all the subsystems defined in robot container's constructor and runs a 20ms loop. FRC coding fills this 20ms control loop with commands that manipulate subsystems.

The next topic is [[How to make a basic subsystem]]