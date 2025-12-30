Recording and Playing Back Data with ROS 2
Goal

Record and replay data published on topics or services to examine it later.

Prerequisites

ROS 2 Jazzy installed

turtlesim and demo nodes installed

Source ROS 2 in every terminal:

source /opt/ros/jazzy/setup.bash

Managing Topic Data
1. Setup

Start turtlesim and teleop nodes:

ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key


Create a directory for recordings:

mkdir ~/bag_files
cd ~/bag_files

2. Choose a Topic

List topics in the system:

ros2 topic list


Example: /turtle1/cmd_vel is used to control the turtle.

Check the live data:

ros2 topic echo /turtle1/cmd_vel


Use arrow keys in teleop to see published messages.

3. Record Topics

Single topic:

ros2 bag record /turtle1/cmd_vel


Press Ctrl+C to stop recording. Data is saved in a new bag directory.

Multiple topics:

ros2 bag record -o subset /turtle1/cmd_vel /turtle1/pose


-o subset names the bag file subset.

Record all topics:

ros2 bag record -a

4. Inspect Topic Data

Check details of a bag file:

ros2 bag info subset


Example output:

Topics: 
/turtle1/cmd_vel | Type: geometry_msgs/msg/Twist | Count: 9
/turtle1/pose    | Type: turtlesim/msg/Pose  | Count: 3004

5. Play Topic Data

Replay recorded data:

ros2 bag play subset


Turtle will move following your recorded path.

Check topic publish rate:

ros2 topic hz /turtle1/pose

Managing Service Data
1. Setup

Run demo nodes:

ros2 run demo_nodes_cpp introspection_service --ros-args -p service_configure_introspection:=contents
ros2 run demo_nodes_cpp introspection_client --ros-args -p client_configure_introspection:=contents

2. Check Service Availability
ros2 service list
ros2 service echo --flow-style /add_two_ints

3. Record Services

Specific service:

ros2 bag record --service /add_two_ints


All services:

ros2 bag record --all-services

4. Inspect Service Data
ros2 bag info <bag_file_name>


Example output shows service requests/responses count and type.

5. Play Service Data
ros2 bag play --publish-service-requests <bag_file_name>


Sends the recorded service requests to the server.

You can inspect results with:

ros2 service echo --flow-style /add_two_ints

Summary

ros2 bag record captures data on topics and services.

ros2 bag info inspects the recording.

ros2 bag play replays the data.

Useful for debugging, testing, and sharing experiments.
