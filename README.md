# CivilDrones
## Software In The Loop
#### The SITL (software in the loop) simulator allows you to run Plane, Copter or Rover without any hardware. It is a build of the autopilot code using an ordinary C++ compiler, giving you a native executable that allows you to test the behaviour of the code without hardware.It takes advantage of the fact that ArduPilot is a portable autopilot that can run on a very wide variety of platforms.

*This article provides an overview of SITL’s benefits and architecture.*

###### SITL Architecture
Note in the image below the port numbers are indicative only and can vary depending on your environment.

![](https://user-images.githubusercontent.com/10976047/51415178-396bcb00-1b75-11e9-9d89-dcc1d00e5d5e.jpg)

DroneKit-SITL is the simplest, fastest and easiest way to run SITL on Windows, Linux (x86 architecture only), or Mac OS X. It is installed from Python’s pip tool on all platforms, and works by downloading and running pre-built vehicle binaries that are appropriate for the host operating system.

Install DroneKit on windows using `<pip install dronekit-sitl>` 

The complete instruction is explaied on [DroneKit-SITL](http://python.dronekit.io/develop/sitl_setup.html). Which is very simple to 
follow.

After the installation connect your flight controller via USB and run the the python script SITL/DroneKit_Simulator.py to get all the vehicle attributes, which might look like below image

![](https://user-images.githubusercontent.com/10976047/51426373-13344280-1bea-11e9-8b1e-b10c17eedb16.png)

In Order to create a virual vehicle run the command

`<dronekit-sitl copter--home=51.500796,6.545725,584,353>` 

This will create a virtul copter at specified coordinates which is also my Home location

![](https://user-images.githubusercontent.com/10976047/51426417-ce5cdb80-1bea-11e9-87fc-35840493b1a1.PNG)

Vehicle is created at TCp port 5670

MAVProxy is a fully-functioning GCS for UAV's. The intent is for a minimalist, portable and extendable GCS for any UAV supporting the MAVLink protocol (such as the APM).

A complete windows installer for MAVProxy is available at 
http://firmware.ardupilot.org/Tools/MAVProxy/.

Goto MavProxy root directory and run the following command

`<mavproxy.exe --master tcp:127.0.0.1:5760 --out 127.0.0.1:14550>` 

This will port the the vehicle from port 5670 to a UDP port 14550 , which then can be connected to Mission Planner for further
analysis
![](https://user-images.githubusercontent.com/10976047/51426482-cbaeb600-1beb-11e9-9c50-44e15b101bce.PNG)
![](https://user-images.githubusercontent.com/10976047/51426483-cf423d00-1beb-11e9-9115-f34e2b70d69f.PNG)

Once you see the `<Readt to FLY ublox>` command on your prompt your vehicle is now ready to fly. If you can't please make sure that all your installations are in order.

Open the installed Mission planner or Q-ground Controller software. Change the port to UDP on the top right corner, make sure you connect to correct specified UDP port and hit connect.

![](https://user-images.githubusercontent.com/10976047/51426539-89d23f80-1bec-11e9-8d2f-25492e7c1d84.PNG)

![](https://user-images.githubusercontent.com/10976047/51426564-d1f16200-1bec-11e9-9c5a-0f11f63d24f5.PNG)

After connecting the vehicle your mission plannr should look as shown below. Confirm with your home coordinates.

![](https://user-images.githubusercontent.com/10976047/51426642-d407f080-1bed-11e9-8c4e-b1d74e0c719d.PNG)

Now the drone is ready to fly. goto SITL/Simple_Go_To.py and execute the script. This is ARM your drone and fly to the specified coordinates and return back to your home location. The complete pictorial represenation is shown below.

![](https://user-images.githubusercontent.com/10976047/51426728-ee8e9980-1bee-11e9-9a67-3db069acd430.png)
![](https://user-images.githubusercontent.com/10976047/51426729-ee8e9980-1bee-11e9-92fa-ce0c08a6960e.png)
![](https://user-images.githubusercontent.com/10976047/51426730-ef273000-1bee-11e9-894f-753367052204.png)

The complete set of Python commands, instructions can be found on 
http://python.dronekit.io/develop/best_practice.html

Follow examples on 
http://python.dronekit.io/examples/running_examples.html


## Hardware In The Loop 

#### Hardware-in-the-Loop (HITL or HIL) is a simulation mode in which normal PX4 firmware is run on real flight controller hardware. This approach has the benefit of testing most of the actual flight code on the real hardware.

###### HITL Architecture

![](https://user-images.githubusercontent.com/23422449/51610645-88bb4e00-1f1d-11e9-9090-d170b7585e24.png)

###### jMAVSim

jMAVSim is a simple multirotor/Quad simulator that allows you to fly copter type vehicles running PX4 around a simulated world. It is easy to set up and can be used to test that your vehicle can take off, fly, land, and responds appropriately to various fail conditions (e.g. GPS failure).

Clone and setup jMAVSim.

The installation steps are explaied in [jMAVSim](https://github.com/PX4/jMAVSim), which is very simple to 
follow.

After the installation connect your flight controller via USB and note the port name from 'Device Manager'.

On Windows, to run the simulator use the below code:

`<java -cp lib/*;out/production/jmavsim.jar me.drton.jmavsim.Simulator -serial COM9 9600 -qgc -m>` 

COM9 9600 - this is the option to mention the method to connect to Flight conroller via USB
qgc - Forward message packets to QGC via UDP at 127.0.0.1:14550

Once the simulator is up below window opens and starts sending MAVLink messages.

![](https://user-images.githubusercontent.com/23422449/51617767-3aae4680-1f2d-11e9-950f-dcc3e0c3194c.png)


Open Q-ground Control or Mission Planner. This automatically connects the simulated drone and displays in the application.

![](https://user-images.githubusercontent.com/23422449/51619144-fa9c9300-1f2f-11e9-8834-465f9161829d.png)

This lets you check if the hardware components are funtioning properly.

By connecting RC you can simulate flying the drone in the simulated world.

Hope this gives an idea on SITL and HITL

Happy flying!! :airplane: :thumbsup:
