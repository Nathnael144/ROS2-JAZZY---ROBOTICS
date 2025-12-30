

Goal: Learn how to get, set, save, and reload parameters for nodes.

Concept:

Parameters are node-specific configuration values: integers, floats, booleans, strings, lists.

They allow nodes to customize behavior at runtime or startup.

1. Setup

Start turtlesim nodes:

ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key

2. List Parameters
ros2 param list


Example output:

/teleop_turtle:
  scale_angular
  scale_linear
  use_sim_time
/turtlesim:
  background_r
  background_g
  background_b
  use_sim_time

3. Get Parameter Value
ros2 param get <node_name> <parameter_name>


Example:

ros2 param get /turtlesim background_g
# Output: Integer value is: 86

4. Set Parameter Value
ros2 param set <node_name> <parameter_name> <value>


Example:

ros2 param set /turtlesim background_r 150


Note: This only changes the parameter temporarily for the current session.

5. Dump Parameters to File
ros2 param dump <node_name> > <file_name>


Example:

ros2 param dump /turtlesim > turtlesim.yaml


Example file content:

/turtlesim:
  ros__parameters:
    background_b: 255
    background_g: 86
    background_r: 150
    use_sim_time: false

6. Load Parameters from File
ros2 param load <node_name> <parameter_file>


Example:

ros2 param load /turtlesim turtlesim.yaml


Warning: Some read-only parameters (like QoS overrides) cannot be changed at runtime.

7. Load Parameter File at Node Startup
ros2 run <package_name> <executable_name> --ros-args --params-file <file_name>


Example:

ros2 run turtlesim turtlesim_node --ros-args --params-file turtlesim.yaml


Note: All parameters, including read-only ones, will be applied at startup.

Summary

Parameters define node configuration values.

Use ros2 param get and ros2 param set to read and modify them at runtime.

Use ros2 param dump to save parameters, and ros2 param load or --params-file to reload them.
