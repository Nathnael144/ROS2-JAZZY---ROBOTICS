

Goal: Learn about services in ROS 2 using command line tools.
Concept: Services are request/response communication between nodes, unlike topics which are continuous streams.

1. Setup

Start turtlesim nodes:

ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key

2. List Active Services
ros2 service list


Example output:

/clear
/kill
/reset
/spawn
/turtle1/set_pen
/turtle1/teleport_absolute
/turtle1/teleport_relative


Show types for all services:

ros2 service list -t

3. Get Service Type
ros2 service type /clear


Output:

std_srvs/srv/Empty

4. Service Info
ros2 service info /clear


Output example:

Type: std_srvs/srv/Empty
Clients count: 0
Services count: 1

5. Find Services by Type
ros2 service find std_srvs/srv/Empty


Output:

/clear
/reset

6. Inspect Service Interface
ros2 interface show std_srvs/srv/Empty


Empty service → no request or response fields.

Example for /spawn service:

ros2 interface show turtlesim/srv/Spawn


Output:

float32 x
float32 y
float32 theta
string name
---
string name

7. Call a Service

Empty service (/clear):

ros2 service call /clear std_srvs/srv/Empty


Service with arguments (/spawn):

ros2 service call /spawn turtlesim/srv/Spawn "{x: 2, y: 2, theta: 0.2, name: ''}"


Example output:

requester: making request: turtlesim.srv.Spawn_Request(x=2.0, y=2.0, theta=0.2, name='')
response: turtlesim.srv.Spawn_Response(name='turtle2')

8. Echo a Service

View requests and responses between a client and server:

ros2 service echo --flow-style /add_two_ints


Example output:

info:
  event_type: REQUEST_SENT
request: [{a: 2, b: 3}]
response: [{sum: 5}]


Note: Service echo requires service introspection to be enabled.

Enable introspection for demo nodes:

ros2 launch demo_nodes_cpp introspect_services_launch.py
ros2 param set /introspection_service service_configure_introspection contents
ros2 param set /introspection_client client_configure_introspection contents

Summary

Services are request/response communication.

Use topics for continuous streaming data.

Commands allow you to:

List services

Inspect types

Call services

Echo service communication
