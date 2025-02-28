# Gazebo-for-Mac-Windows

## Overview

Gazebo is an open source tool that is used for simulation with robots and virtual environments.

## Installation
---
## Mac(Using Homebrew)

Run the following code in a terminal:

``
brew tap osrf/simulation
brew install gz-harmonic
``

## How to Run the System
---
## Mac

Launch Gazebo server by Running:

``
gz sim -v 4 shapes.sdf -s  
``
Launch Gazebo gui in another terminal:

``
gz sim -v 4 -g 
``
