## Reference:
* 5-DOF Robotic Arm Design Sample: https://circuitcellar.com/research-design-hub/build-a-4-dof-robotic-arm-part-1/
* General Knowledge on Robotic Design: http://www.robotplatform.com/knowledge.html
* Discussion on PID Control: https://robotics.stackexchange.com/questions/167/what-are-good-strategies-for-tuning-pid-loops
* 正向运动学的数学知识: https://zhuanlan.zhihu.com/p/33985103  
                   https://www.alanzucconi.com/2017/04/17/procedural-animations/
* Python Robotic Resources: https://pythonrobotics.readthedocs.io/en/latest/getting_started.html
* Robotic System Textbook: https://github.com/krishauser/RoboticSystemsBook/blob/079bfe5a8e649aef0b6409cc4b99820456fcf7ca/WhatIsRobotics.ipynb
* Pandas自带的数据分析处理：http://www.360doc.com/content/20/0127/18/27915469_888197502.shtml

This article describe a 4-DOF robotic arm design w/ 1 x DC motor and 4 x Digital Servo motor, and PID algo is design via Matlab.

## Basic Concept

Torque, Dead Band Width, 2-Channel H-bridge Driver Module, Bi-Phase Encoder, Configuration Space, Robot Pose Representation in three dimensions, Homogeneous Transformations, Denavit-Hartenberg parameters, Direct kinematics and inverse kinematics with the pseudo-inverse Jacobian

It is important to have motors with the correct torque specifications for each one of the joints, there are free online apps to 
calculate torque for robotic arm joints [4]. You need to provide inputs, such as the configuration of the robotic arm 
(how many degrees of freedom it has), link lengths, link weights, loads and so on.
We can begin the experimental robotic arm design based on the off-the-shelf aluminum robotic arm kit [3] to ease the mechanical 
implementation and concentrate all efforts on the electronics and code parts of the system.

## Klampt
Klamp’t(Kris’ Locomotion and Manipulation Planning Toolbox) is an open-source,cross-platform software package for modeling, simulating, planning, and optimization for complex robots, particularly for manipulation and locomotion tasks. This manual is meant to givea high-level roadmap of the library’s functionalityand shouldnot be considered a replacement forthe detailed API documentation.

## Comparison w/ Other Solutions
* ROS (Robot Operating System)is a large operating system designed for distributed controlof physical robots.Although it does come with planning toolsthey are not as flexible as those in Klamp’t.ROS has limited support for legged robots, and is poorly suited for prototyping high-rate feedback control systems.ROS is heavy-weight and not completely cross-platform(only Ubuntu is fully supported). ROS also has many more wrappers for integration with hardware platforms and sensors.
* OpenRAVE (Robotics and Animation Virtual Environment)is similar to Klamp’tand was developed concurrently by a similar group at CMU.OpenRAVE has more sophisticated manipulation functionality.Does not support planning for legged robots, but simulation is possible with some effort.Simulation models areoften conflated with planning models whereas in Klamp’tthey are fullydecoupled. Heavy-weight.
* Gazebo, Webots, V-REP, etcare robot simulation packages built off of the same class of rigid body simulations as Klamp’t.They have more sophisticated sensor simulation capabilities, cleaner APIs, and nicer visualizationsbut aretypically built for mobile robotsand have limited functionality for modeling, planning,and optimization.Klamp’talso has improved mesh-mesh collision handlingthat makes collision handling much more stable.

## Configuration & Task Space
Definition: The joint configuration of a robotic arm is the set of all joint angles that unequivocally describe their pose.

Description:
q = { θ 1 , θ 2 , θ 3 , θ 4 }

θ 1 : joint 1 angle

θ 2 : joint 2 angle

θ 3 : joint 3 angle

θ 4 : joint 4 angle

The configuration space is constrained to a subset of all possible combinations of angles, because joints generally have physical limits, due to the arm structure design and motor rotation limits.

θ 1 : [-90,+90]   (joint 1)

θ 2 : [-25,+155] (joint 2)

θ 3 : [-135,+45] (joint 3)

θ 4 : [-90,+90]   (joint 4)



## Reference
http://docplayer.net/31476196-1-what-is-klamp-t-features-currently-supported-platforms-comparison-to-related-packages-4.html
