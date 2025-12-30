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
