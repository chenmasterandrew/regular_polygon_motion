COSC.69.13
22F
Andrew Chen

# PA1
## Method
This program is a fork of https://github.com/quattrinili/simple_motion and uses the `move_forward` and `rotate_in_place` functions provide to move and turn along the sides of a polygon. Information about the polygon on which the robot will move, `side_length`, `num_sides`, and `is_clockwise`, is provided to the launch file as arguments. The launch file in turn sets this information as parameters. The parameters are accessed by the `move_polygon` function called by ther `main` function which is run when the node is launched. 

The`move_polygon` function first calculates the interior angle of the polygon specified by the parameters using the formula `((num_sides - 2) * math.pi) / num_sides`. Then, it calculates the amount to turn in radians depending on whether the robot is traversing the polygon in a counterclockwise or clockwise manner. Specifically, the turning angle is `math.pi + interior_angle` if the motion is clockwise and `math.pi - interior_angle` if the motion is counterclockwise. Then, `move_polygon` loops `num_sides` sides. For each iteration of the loop, the `move_forward` function is called with a distance of `side_length` and the `rotate_in_place` function is called with the turning angle calculated before the loop began. As a result, the robot moves forward and turns along each side of the polygon.

The `move_polygon` function also calculates and reports the error (euclidean distance between expected robot position and actual robot distance) at each vertex of the polygon. The node first subscribes to the `odom` topic to get the actual position of the robot. Then, assuming the robot starts at (0,0) with a yaw angle of 0, `move_polygon` calculates the location of the robot at each vertex of the polygon `(prev_vert_x + cos(turning_angle) * side_length, prev_vert_y + sin(turning_angle) * side_length)`. Then, the function calculates the error using the standard euclidean distance formula and reports it by publishing to the the `rpm_err` topic and logging it with `rospy.loginfo`.

Using these parameters, the main function determines the 
## Evaluation
As shown in the videos, this program works; however, there was a reasonable amount of error, which increased depending on the parameters provided. Error increases with number of sides and side length. Couterclockwise motion also has higher error than clockwise motion as shown in the comparisons below:

    3 sides, side length 1, clockwise: 0.095494620502
    3 sides, side length 1, counterclockwise: 0.442621380091
    3 sides, side length 4, clockwise: 0.319017410278
    5 sides, side length 1, clockwise: 0.448784530163