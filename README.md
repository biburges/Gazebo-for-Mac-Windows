# Gazebo-for-Mac-Windows

## Overview

Gazebo is an open source tool that is used for simulation with robots and virtual environments.

## Installation
### Mac(Using Homebrew)

Install Homebrew:

``
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
``

Run the following code in a terminal:

``
brew tap osrf/simulation
``
``
brew install gz-ionic
``

**NOTE: If you get a warning that says something like the following:**

Error: The maximum number of open files on this system has been reached. Use ulimit -n to increase this limit.

**This means it hit the maximum number of file descriptors in the system. Execute the following code to increase the limit:**

``
ulimit -n 100000
``

---
### Windows (Installing Gazebo Classic 11)
- Ensure you have windows subsystem for linux (WSL) installed, if not, install by running
  ```
  wsl --install
  ```
- Restart laptop after installation
- Run wsl by simply typing the following into the powershell terminal run as administrator
  ```
  wsl
  ```
- Type the following to update all the packages
  ```
  sudo apt update && sudo apt upgrade -y
  ```
- Type the following to install the gazebo simulator, via snap, which is a package management system designed for linux which contains all the dependencies.
  ```
  sudo snap install gazebo
  ```
- The folloing installs gazebo
  ```
  sudo apt install gazebo
  ```
- Run gazebo
  ```
  gazebo
  ```

## How to Run the System

### Mac

Launch Gazebo server by Running:

``
gz sim -v 4 shapes.sdf -s  
``

Launch Gazebo gui in another terminal:

``
gz sim -v 4 -g 
``

---
### Windows
- Run gazebo for windows by running the following in powershell (as admin)
  ```
  wsl
  gazebo
  ```

## Build a Robot(Car)
### Importing a car model
- Clone a pre-built model of a car via a github repo from the link below
  ```
  git clone https://github.com/osrf/car_demo
  ```
- Navigate to the cloned repo and view the models the repository possess
- Open up a gazebo simulation through running
  ```
  wsl
  gazebo
  ```
- To spawn the appropriate model, type the following
  ```
  gz model --spawn-file=model.sdf --model-name=my_box <where model.sdf is changed to the name of your model's .sdf file>
  ```
### Build a World

First Create a SDF file titled ``` building_robot.sdf ``` and paste the following code into it:

```
<?xml version="1.0" ?>
<sdf version="1.10">
    <world name="car_world">
        <physics name="1ms" type="ignored">
            <max_step_size>0.001</max_step_size>
            <real_time_factor>1.0</real_time_factor>
        </physics>
        <plugin
            filename="gz-sim-physics-system"
            name="gz::sim::systems::Physics">
        </plugin>
        <plugin
            filename="gz-sim-user-commands-system"
            name="gz::sim::systems::UserCommands">
        </plugin>
        <plugin
            filename="gz-sim-scene-broadcaster-system"
            name="gz::sim::systems::SceneBroadcaster">
        </plugin>

        <light type="directional" name="sun">
            <cast_shadows>true</cast_shadows>
            <pose>0 0 10 0 0 0</pose>
            <diffuse>0.8 0.8 0.8 1</diffuse>
            <specular>0.2 0.2 0.2 1</specular>
            <attenuation>
                <range>1000</range>
                <constant>0.9</constant>
                <linear>0.01</linear>
                <quadratic>0.001</quadratic>
            </attenuation>
            <direction>-0.5 0.1 -0.9</direction>
        </light>

        <model name="ground_plane">
            <static>true</static>
            <link name="link">
                <collision name="collision">
                <geometry>
                    <plane>
                    <normal>0 0 1</normal>
                    </plane>
                </geometry>
                </collision>
                <visual name="visual">
                <geometry>
                    <plane>
                    <normal>0 0 1</normal>
                    <size>100 100</size>
                    </plane>
                </geometry>
                <material>
                    <ambient>0.8 0.8 0.8 1</ambient>
                    <diffuse>0.8 0.8 0.8 1</diffuse>
                    <specular>0.8 0.8 0.8 1</specular>
                </material>
                </visual>
            </link>
        </model>
	<model name='vehicle_blue' canonical_link='chassis'>
    	    <pose relative_to='world'>0 0 0 0 0 0</pose>
	    <link name='chassis'>
            	<pose relative_to='__model__'>0.5 0 0.4 0 0 0</pose>
    		<inertial> <!--inertial properties of the link mass, inertia matix-->
        		<mass>1.14395</mass>
        		<inertia>
            			<ixx>0.095329</ixx>
            			<ixy>0</ixy>
            			<ixz>0</ixz>
            			<iyy>0.381317</iyy>
            			<iyz>0</iyz>
            			<izz>0.476646</izz>
        		</inertia>
    		</inertial>
		<visual name='visual'>
        		<geometry>
            			<box>
                			<size>2.0 1.0 0.5</size>
            			</box>
        		</geometry>
        		<!--let's add color to our link-->
        		<material>
            			<ambient>0.0 0.0 1.0 1</ambient>
            			<diffuse>0.0 0.0 1.0 1</diffuse>
           			<specular>0.0 0.0 1.0 1</specular>
        			</material>
    			</visual>
			<collision name='collision'>
            			<geometry>
                			<box>
                    				<size>2.0 1.0 0.5</size>
                			</box>
            			</geometry>
        		</collision>
    		</link>
		<link name='left_wheel'>
    			<pose relative_to="chassis">-0.5 0.6 0 -1.5707 0 0</pose>
    			<inertial>
        			<mass>1</mass>
        			<inertia>
            				<ixx>0.043333</ixx>
            				<ixy>0</ixy>
            				<ixz>0</ixz>
            				<iyy>0.043333</iyy>
           				<iyz>0</iyz>
            				<izz>0.08</izz>
        			</inertia>
    			</inertial>
    			<visual name='visual'>
        			<geometry>
            				<cylinder>
               					<radius>0.4</radius>
                				<length>0.2</length>
            				</cylinder>
        			</geometry>
        			<material>
            				<ambient>1.0 0.0 0.0 1</ambient>
            				<diffuse>1.0 0.0 0.0 1</diffuse>
            				<specular>1.0 0.0 0.0 1</specular>
        			</material>
    			</visual>
    			<collision name='collision'>
        			<geometry>
            				<cylinder>
                				<radius>0.4</radius>
                				<length>0.2</length>
            				</cylinder>
        			</geometry>
    			</collision>
		</link>

		<link name='right_wheel'>
    			<pose relative_to="chassis">-0.5 -0.6 0 -1.5707 0 0</pose> <!--angles are in radian-->
    			<inertial>
        			<mass>1</mass>
        			<inertia>
            				<ixx>0.043333</ixx>
            				<ixy>0</ixy>
            				<ixz>0</ixz>
            				<iyy>0.043333</iyy>
            				<iyz>0</iyz>
            				<izz>0.08</izz>
        			</inertia>
    			</inertial>
    			<visual name='visual'>
        			<geometry>
            				<cylinder>
                				<radius>0.4</radius>
                				<length>0.2</length>
            				</cylinder>
        			</geometry>
        			<material>
            				<ambient>1.0 0.0 0.0 1</ambient>
            				<diffuse>1.0 0.0 0.0 1</diffuse>
            				<specular>1.0 0.0 0.0 1</specular>
        			</material>
    			</visual>
    			<collision name='collision'>
        			<geometry>
            				<cylinder>
                				<radius>0.4</radius>
                				<length>0.2</length>
            				</cylinder>
        			</geometry>
    			</collision>
		</link>
		<frame name="caster_frame" attached_to='chassis'>
    			<pose>0.8 0 -0.2 0 0 0</pose>
		</frame>
		

		<link name='caster'>
    			<pose relative_to='caster_frame'/>
    			<inertial>
        			<mass>1</mass>
        			<inertia>
            				<ixx>0.016</ixx>
            				<ixy>0</ixy>
            				<ixz>0</ixz>
            				<iyy>0.016</iyy>
            				<iyz>0</iyz>
            				<izz>0.016</izz>
        			</inertia>
    			</inertial>
    			<visual name='visual'>
        			<geometry>
            				<sphere>
                				<radius>0.2</radius>
            				</sphere>
        			</geometry>
        			<material>
            				<ambient>0.0 1 0.0 1</ambient>
            				<diffuse>0.0 1 0.0 1</diffuse>
            				<specular>0.0 1 0.0 1</specular>
        			</material>
    			</visual>
    			<collision name='collision'>
        			<geometry>
            				<sphere>
                				<radius>0.2</radius>
            				</sphere>
        			</geometry>
    			</collision>
		</link>
		<joint name='left_wheel_joint' type='revolute'>
    			<pose relative_to='left_wheel'/>
			<parent>chassis</parent>
    			<child>left_wheel</child>
    			<axis>
        			<xyz expressed_in='__model__'>0 1 0</xyz> <!--can be defined as any frame or even arbitrary frames-->
        			<limit>
            				<lower>-1.79769e+308</lower>    <!--negative infinity-->
           				<upper>1.79769e+308</upper>     <!--positive infinity-->
        			</limit>
    			</axis>
		</joint>
		<joint name='right_wheel_joint' type='revolute'>
    			<pose relative_to='right_wheel'/>
    			<parent>chassis</parent>
    			<child>right_wheel</child>
    			<axis>
        			<xyz expressed_in='__model__'>0 1 0</xyz>
        			<limit>
            				<lower>-1.79769e+308</lower>    <!--negative infinity-->
            				<upper>1.79769e+308</upper>     <!--positive infinity-->
        			</limit>
    			</axis>
		</joint>
		<joint name='caster_wheel' type='ball'>
    			<parent>chassis</parent>
    			<child>caster</child>
		</joint>
	</model>
    </world>
</sdf>


```
This should have created a two wheel car that looks like the following:

![My Image](car.png)

(For Mac) Then navigate in your terminal to where you put the file and then run the code ``` gz sim -v 4 building_robot.sdf -s``` in one terminal to launch the simulator server and `` gz sim -v 4 -g `` in another terminal to launch the gui

## Move the Robot(Car)

You want to add a plugin which will help control the robot in the world that was created. This can be done by pasting the following code into your `` building_robots.sdf `` file

```

<plugin
    filename="gz-sim-diff-drive-system"
    name="gz::sim::systems::DiffDrive">
    <left_joint>left_wheel_joint</left_joint>
    <right_joint>right_wheel_joint</right_joint>
    <wheel_separation>1.2</wheel_separation>
    <wheel_radius>0.4</wheel_radius>
    <odom_publish_frequency>1</odom_publish_frequency>
    <topic>cmd_vel</topic>
</plugin>

```

(For Macs) to launch the server run the code ``` gz sim -v 4 building_robot.sdf -s``` in one terminal and `` gz sim -v 4 -g `` in another terminal to launch the gui and in a third terminal ``gz topic -t "/cmd_vel" -m gz.msgs.Twist -p "linear: {x: 0.5}, angular: {z: 0.05}"`` to send commands to your robot. This one is sending a command to move at a linear speed of x:0.5 and angular speed of y:0.05

However, if you want to control the robot using you keyboard, using the arrow keys, you want to do the following steps:

- In one terminal type `` gz sim -v 4 building_robot.sdf -s ``
- In another terminal type `` gz sim -v 4 -g ``
- In your `` building_robot.sdf `` code, in the top right corner click on the plugins dropdown list (vertical ellipsis), click the Key Publisher
- In a third terminal type `` gz topic -e -t /keyboard/keypress ``

In the `` gz topic -e -t /keyboard/keypress `` terminal, data will show based on the key you pressed, this is how you will code your motions in the `` building_robots.sdf `` file. For example, if the up arrow gave a data value of 16777235 and you wanted that to be the code to represent you moving forward, add this code to your sdf file

```
<!-- Moving Forward-->
<plugin filename="gz-sim-triggered-publisher-system"
        name="gz::sim::systems::TriggeredPublisher">
    <input type="gz.msgs.Int32" topic="/keyboard/keypress">
        <match field="data">16777235</match>
    </input>
    <output type="gz.msgs.Twist" topic="/cmd_vel">
        linear: {x: 0.5}, angular: {z: 0.0}
    </output>
</plugin>

```

## Commentary

### Mac

The install process was really easy and simple when I used Harmonic and Ionic versions but running the program proposed problems as I found myself having to uninstall and reinstall the software every time I wanted to make an update to the sdf file

