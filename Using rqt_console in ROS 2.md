Using rqt_console in ROS 2

Always source ROS 2 before running commands:

source /opt/ros/jazzy/setup.bash

1. Launch rqt_console
ros2 run rqt_console rqt_console


A GUI window opens with three main sections:

Top: Displays log messages from nodes.

Middle: Filter messages by severity (Info, Warn, Error, Debug, Fatal) and other properties.

Bottom: Highlight messages containing a specific string.

2. Generate log messages

Start turtlesim:

ros2 run turtlesim turtlesim_node


Then, publish a topic to make the turtle run into the wall:

ros2 topic pub -r 1 /turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: 0.0}}"


The turtle will collide with the wall repeatedly.

rqt_console will show repeated Warn messages for this behavior.

Stop publishing with Ctrl+C.

3. Logger levels

ROS 2 log messages have severity levels:

Level	Meaning
Fatal	System is terminating to protect itself
Error	Significant problem preventing proper function
Warn	Unexpected or non-ideal activity
Info	Normal system status updates
Debug	Step-by-step detailed messages

Default severity level: Info (shows Info, Warn, Error, Fatal)

4. Change default logger level

Set logger severity when launching a node:

ros2 run turtlesim turtlesim_node --ros-args --log-level WARN


Only messages of level Warn or higher will be shown.

Info and Debug messages are suppressed.

Summary

rqt_console lets you view, filter, and analyze logs from ROS 2 nodes.

Useful for debugging complex systems and understanding event sequences.

Combine with ros2 topic pub to generate log messages for testing.
