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

## Build a Robot

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
    </world>
</sdf>

```
Then navigate in your terminal to where you put the file and then run the code ``` gz sim building_robot.sdf ``` to launch the simulator
