romeo_moveit_config
===================

This is a MoveIt! config package generated by the MoveIt! wizard.
It requires a ROMEO model which you can get from here:

https://github.com/ros-aldebaran/romeo_robot/tree/master/romeo_description
or from the binary package : ros-indigo-romeo-description

The moveit package must be run on a remote computer and not directly on your robot.

1 Compile the package
=====================

romeo_moveit_config package doesn't need any compilation so running rospack profile should be enough

For the dcm packages you need to compile the C++ nodes.  In order to compile romeo_dcm packages, you need to set the environment variable AL_DIR to the path to naoqiSDK-c++ on your computer.

Then you can run the usual 

.. code-block:: bash

    catkin_make

And your ready to play with your romeo

2 Run MoveIt
============

Without robot
-------------
You can run this moveit package either unconnected to any robot or attached to a robot (real or simulated):
For a standalone execution :

.. code-block:: bash

    roslaunch romeo_moveit_config demo.launch

On a real ROMEO
---------------
To use moveit on a real robot you need to instanciate ros controllers on your Romeo.
To do so you need the romeo_dcm packages (in the metapackage romeo_robot : https://github.com/ros-aldebaran/romeo_robot)

To launch it on a real Romeo : 

(First, set the NAO_IP environment variable to your Romeo's ip.)
Modify the bringup configuration file : romeo_dcm_bringup/config/romeo_dcm.yaml
Set the rosparam "RobotIP" to your Romeo's IP address

.. code-block:: bash

    roslaunch romeo_dcm_bringup romeo_dcm_bringup_remote.launch

Wait until romeo_dcm_bringup node is ready, then run:

.. code-block:: bash

    roslaunch romeo_moveit_config moveit_planner_romeo.launch

3 Use Moveit:
=============
RVIZ has been open: you can see that a MotionPlanning plugin has been launched.
First check the box "Allow approximate IK Solutions" on the bottom of the left column.
Then click on the Planning tab.

Select which part of the robot you want to move:
In the plugin list on the upper part of the left column, you can select a group under MotionPlanning/Planning Request/Planning Group 


Now you can define your motion by drag and dropping the interactive markers.
You can compute a trajectory by clicking the 'planning' button 
Once the motion is satisfying you can try it on your real robot using 'execute' or 'plan and execute'.

NOTE: The start state is not updated automatically, you have to go to 'Select Start State' select 'Current' and click 'Update'. 
