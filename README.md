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
