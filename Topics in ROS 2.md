🎯 Goal

Use command-line tools and rqt_graph to inspect, debug, and understand ROS 2 topics and how nodes communicate.

🔹 1. Setup (Run Turtlesim Nodes)

Start the turtlesim node:

ros2 run turtlesim turtlesim_node


Start the keyboard teleoperation node:

ros2 run turtlesim turtle_teleop_key


Default node names:

/turtlesim

/teleop_turtle

🔹 2. rqt_graph

Purpose: Visualize nodes and topics graphically.

Run rqt_graph:

ros2 run rqt_graph rqt_graph


Alternative (from rqt GUI):

Plugins → Introspection → Node Graph


Shows:

/teleop_turtle publishing to /turtle1/cmd_vel

/turtlesim subscribing to /turtle1/cmd_vel

🔹 3. ros2 topic list

Purpose: List all active topics.

ros2 topic list


List topics with message types:

ros2 topic list -t


Example output:

/turtle1/cmd_vel [geometry_msgs/msg/Twist]
/turtle1/pose [turtlesim/msg/Pose]

🔹 4. ros2 topic echo

Purpose: Display live data being published on a topic.

ros2 topic echo /turtle1/cmd_vel


Example output:

linear:
  x: 2.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0

🔹 5. ros2 topic info

Purpose: Show basic information about a topic.

ros2 topic info /turtle1/cmd_vel


Example output:

Type: geometry_msgs/msg/Twist
Publisher count: 1
Subscription count: 2

🔹 5.1 Verbose Topic Info
ros2 topic info /turtle1/cmd_vel --verbose


Shows:

Publisher & subscriber node names

QoS settings

Topic type hash

Reliability, history, durability, etc.

🔹 6. ros2 interface show

Purpose: Show the structure of a message type.

ros2 interface show geometry_msgs/msg/Twist


Output:

Vector3 linear
  float64 x
  float64 y
  float64 z
Vector3 angular
  float64 x
  float64 y
  float64 z

🔹 7. ros2 topic pub

Purpose: Publish messages to a topic from the command line.

General syntax:
ros2 topic pub <topic_name> <msg_type> '<args>'

🔸 a) Publish using YAML dictionary
ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"


Publish only selected fields:

ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: 1.8}}"

🔸 b) Publish an empty (default) message
ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist


Equivalent to:

ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}" --rate 1

🔸 c) Autocomplete message template
ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist <TAB>


Final editable autocomplete example:

ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist 'linear:
  x: 0.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0
'

🔸 d) Raw autocompleted string
ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist \
\'linear:\^J\ \ x:\ 0.0\^J\ \ y:\ 0.0\^J\ \ z:\ 0.0\^Jangular:\^J\ \ x:\ 0.0\^J\ \ y:\ 0.0\^J\ \ z:\ 0.0\^J\'

🔸 e) Publish once only
ros2 topic pub --once -w 2 /turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: 1.8}}"


--once → publish once and exit

-w 2 → wait for 2 subscribers

🔸 f) Publishing timestamps automatically

With header:

ros2 topic pub /pose geometry_msgs/msg/PoseStamped \
'{header: "auto", pose: {position: {x: 1.0, y: 2.0, z: 3.0}}}'


With Time field:

ros2 topic pub /reference sensor_msgs/msg/TimeReference \
'{header: "auto", time_ref: "now", source: "dummy"}'

🔹 8. ros2 topic hz

Purpose: Measure publishing frequency (Hz).

ros2 topic hz /turtle1/pose

🔹 9. ros2 topic bw

Purpose: Measure bandwidth usage of a topic.

ros2 topic bw /turtle1/pose

🔹 10. ros2 topic find

Purpose: Find topics by message type.

ros2 topic find geometry_msgs/msg/Twist


Output:

/turtle1/cmd_vel

🔹 11. Clean Up

Stop all running nodes:

Ctrl + C

🧠 Final One-Line Summary

ROS 2 topic commands allow you to list, visualize, inspect, publish, and analyze topic-based communication, making them essential tools for debugging and understanding data flow between nodes.
