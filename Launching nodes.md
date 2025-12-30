1. Run a Launch File

Use the ros2 launch command to run a Python launch file:

ros2 launch turtlesim multisim.launch.py


Example launch file: multisim.launch.py

from launch import LaunchDescription
import launch_ros.actions

def generate_launch_description():
    return LaunchDescription([
        launch_ros.actions.Node(
            namespace='turtlesim1', package='turtlesim',
            executable='turtlesim_node', output='screen'),
        launch_ros.actions.Node(
            namespace='turtlesim2', package='turtlesim',
            executable='turtlesim_node', output='screen'),
    ])


This launch file starts two turtlesim nodes with separate namespaces (turtlesim1 and turtlesim2).

Note: Launch files can also be written in XML or YAML formats.

2. (Optional) Control the Turtles

Once the turtlesim nodes are running, you can control them using topics:

Move turtlesim1 turtle:

ros2 topic pub /turtlesim1/turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: 1.8}}"


Move turtlesim2 turtle:

ros2 topic pub /turtlesim2/turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: -1.8}}"


Each turtle can move independently in opposite directions.

Summary

Launch files let you start multiple nodes simultaneously with one command.

You can configure namespaces, remappings, and node parameters within launch files.

This simplifies running complex systems with many nodes.
