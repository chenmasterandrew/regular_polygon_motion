# regular_polygon ROS package

This ROS package contains a ROS node that allows for a simple translation and rotation based on velocities and distance/rotation, and for stop if there is anything immediately in front of it, based on laser scanner.

The ROS node takes as input the parameters of the regular polygon, i.e., the number of sides, the side length, and a flag indicating clockwise or counterclockwise.
The ROS node will then make the robot move according to the calculations, starting at one of the vertices, following one of the edges, and completing it either clockwise or counterclockwise.
The node publishes at each of the vertices of the polygon the error using std_msgs/Float32 between the current position and the expected polygon vertices locations according to the calculations.

## Requirements
- ROS -- tested on Melodic, but other versions may work.
- colcon -- used for building the application. 

## Build
Once cloned in a ROS workspace, e.g., `ros_workspace/src/`, run the following commands to build it:

	cd ros_workspace
	colcon build
	
## Run
Run first the robot nodes or simulator. 
Then, source and use the launch file:

	source ros_workspace/install/setup.sh
	roslaunch regular_polygon_motion regular_polygon_motion.launch

## Attribution & Licensing

See LICENSE for further information
