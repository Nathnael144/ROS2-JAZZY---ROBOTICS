

Goal: Learn how to introspect and use actions in ROS 2.

Concept:

Actions are for long-running tasks: they have a goal, feedback, and result.

They can be canceled and provide continuous feedback.

Use a client-server model: action client sends a goal → action server executes it.

1. Setup

Start turtlesim nodes:

ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key

2. Use Actions in Teleop

The arrow keys move the turtle (cmd_vel topic).

Keys G|B|V|C|D|E|R|T rotate the turtle (action).

F cancels a rotation goal.

Example messages in /turtlesim terminal:

[INFO] [turtlesim]: Rotation goal completed successfully
[INFO] [turtlesim]: Rotation goal canceled
[WARN] [turtlesim]: Rotation goal received before a previous goal finished. Aborting previous goal

3. ros2 node info
ros2 node info /turtlesim
ros2 node info /teleop_turtle


/turtlesim has action server /turtle1/rotate_absolute

/teleop_turtle has action client /turtle1/rotate_absolute

4. ros2 action list
ros2 action list
# Output: /turtle1/rotate_absolute


With types:

ros2 action list -t
# Output: /turtle1/rotate_absolute [turtlesim/action/RotateAbsolute]

5. ros2 action type
ros2 action type /turtle1/rotate_absolute
# Output: turtlesim/action/RotateAbsolute

6. ros2 action info
ros2 action info /turtle1/rotate_absolute


Output example:

Action: /turtle1/rotate_absolute
Action clients: 1
    /teleop_turtle
Action servers: 1
    /turtlesim

7. ros2 interface show
ros2 interface show turtlesim/action/RotateAbsolute


Output:

# Goal
float32 theta
---
# Result
float32 delta
---
# Feedback
float32 remaining

8. ros2 action send_goal
ros2 action send_goal <action_name> <action_type> <values>


Example – send goal:

ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 1.57}"


With feedback:

ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: -1.57}" --feedback


theta → goal rotation (radians)

remaining → feedback while rotating

delta → result (displacement to starting position)

Summary

Actions allow long-running tasks with feedback and cancelation.

Use ros2 node info, ros2 action list, and ros2 interface show to introspect actions.

Use ros2 action send_goal to execute a goal from the command line.
