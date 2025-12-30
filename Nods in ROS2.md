🧠 Simple Definition

A ROS 2 node is a process that performs computation and communicates with other nodes using ROS mechanisms (topics, services, actions, parameters).

🔧 Real-World Analogy

Imagine a robot as a human body:

Human	ROS 2
Eyes	Camera node
Brain	Control node
Ears	Sensor node
Mouth	Actuator / motor node

Each part works independently, but together they form a complete system.

📦 What a Node Can Do

A ROS 2 node can:

✅ Publish data (send messages)

✅ Subscribe to data (receive messages)

✅ Provide services (answer requests)

✅ Call services

✅ Run actions (long tasks)

✅ Use parameters (config values)

🧩 Example: Mobile Robot
Node Name	Purpose
camera_node	Publishes camera images
lidar_node	Publishes laser scan data
controller_node	Computes velocity
motor_node	Drives motors
localization_node	Estimates robot position

Each node is separate, but they communicate.

📡 Node Communication (Very Important)

Nodes do not talk directly.

They communicate via:

Topics → continuous data (sensor streams)

Services → request/response

Actions → long-running tasks

Parameters → configuration

Example:

camera_node  →  /image_raw  →  vision_node

🐢 Example You Already Used (Turtlesim)

When you run:

ros2 run turtlesim turtlesim_node


You start a node called:

/turtlesim


In another terminal:

ros2 run turtlesim turtle_teleop_key


That starts another node:

/teleop_turtle


They communicate using topics!

🛠️ List Running Nodes
ros2 node list


Get node details:

ros2 node info /turtlesim

In ROS 2, remapping means changing a node’s communication names (topics, services, actions, parameters) without modifying the source code.

🧠 Simple Definition

Remapping allows you to redirect where a node sends or receives data at runtime.

🔧 Why Remapping Is Needed

Robots are modular. The same node might be used in:

different robots

different sensors

simulations vs real hardware

Instead of rewriting code, you remap names.

📡 What Can Be Remapped

You can remap:

Topics (/cmd_vel, /scan)



Background
1. The ROS 2 Graph

The ROS graph is a network of nodes and the connections between them.

Visualizes how data flows between nodes in a robotic system.

2. Nodes in ROS 2

Nodes are modular executables responsible for a single task (e.g., publishing sensor data, controlling motors).

Nodes communicate via topics, services, actions, or parameters.

One executable can contain multiple nodes.

Tasks
1. ros2 run

Launch an executable from a package:

ros2 run <package_name> <executable_name>


Example:

ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key

2. ros2 node list

List all active nodes:

ros2 node list


Example workflow:

Start turtlesim_node:

ros2 run turtlesim turtlesim_node


Start turtle_teleop_key:

ros2 run turtlesim turtle_teleop_key


Check active nodes:

ros2 node list


Expected output:

/turtlesim
/teleop_turtle

2.1 Node Remapping

Change the default node name using --ros-args --remap:

ros2 run turtlesim turtlesim_node --ros-args --remap __node:=my_turtle


Check nodes again:

ros2 node list


Output:

/my_turtle
/turtlesim
/teleop_turtle

3. ros2 node info

Get detailed information about a node:

ros2 node info <node_name>


Example:

ros2 node info /my_turtle


Sample output:

/my_turtle
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Service Servers:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /my_turtle/describe_parameters: rcl_interfaces/srv/DescribeParameters
    ...
  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute


Shows subscribers, publishers, services, and actions.

Provides insight into ROS graph connections.

Summary

A node is a fundamental modular unit in ROS 2.

Use ros2 run to launch nodes, ros2 node list to list them, and ros2 node info to inspect them.

Node remapping allows custom naming and topic/service reassignments.

Understanding nodes is essential before exploring topics, services, parameters, and actions.

Services

Actions

Node names

Namespaces
