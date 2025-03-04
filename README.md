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
brew install gz-harmonic
``

**NOTE: If you get a warning that says something like the following:**

Error: The maximum number of open files on this system has been reached. Use ulimit -n to increase this limit.

**This means it hit the maximum number of file descriptors in the system. Execute the following code to increase the limit:**

``
ulimit -n 100000
``

---
### Windows

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

## Build a Robot(Car)

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
Then navigate in your terminal to where you put the file and then run the code ``` gz sim -v 4 building_robot.sdf -s``` in one terminal to launch the simulator server and `` gz sim -v 4 -g `` in another terminal to launch the gui
