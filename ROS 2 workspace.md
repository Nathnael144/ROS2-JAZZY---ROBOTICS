1️⃣ What is a ROS 2 workspace? 
A workspace is a folder where you develop, build, and test ROS 2 packages.

Think of it like this:

Underlay → the main ROS 2 installation
👉 /opt/ros/jazzy

Overlay → your personal development workspace
👉 ~/ros2_ws

📌 Overlay overrides underlay
If a package exists in both places, ROS 2 will use the overlay version first.

This lets you:

Experiment safely

Modify packages without breaking the system ROS 2

Develop your own nodes

2️⃣ Prerequisites (what you must have)

Make sure these are installed:

sudo apt install git python3-colcon-common-extensions \
                 python3-rosdep ros-jazzy-turtlesim


Initialize rosdep (only once):

sudo rosdep init
rosdep update

3️⃣ Step-by-step explained (with ALL commands)
✅ Step 1: Source ROS 2 Jazzy (Underlay)

Every new terminal must source ROS 2:

source /opt/ros/jazzy/setup.bash


📌 This makes ROS 2 commands like ros2, colcon available.

✅ Step 2: Create a workspace

Create a workspace and a src folder:

mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src


📌 Rule:
All ROS 2 packages must go inside src/

✅ Step 3: Clone a sample package (turtlesim)

Make sure you are inside src:

git clone https://github.com/ros/ros_tutorials.git -b jazzy


📌 Why -b jazzy?

Each ROS version has its own branch

You MUST use the matching distro

✅ Step 4: Resolve dependencies with rosdep

Go back to workspace root:

cd ~/ros2_ws


Install dependencies:

rosdep install -i --from-path src --rosdistro jazzy -y


📌 This reads package.xml files and installs missing libraries.

If everything is installed, you’ll see:

All required rosdeps installed successfully

✅ Step 5: Build the workspace (colcon)

From ~/ros2_ws:

colcon build


Expected output:

Starting >>> turtlesim
Finished <<< turtlesim


After build, you’ll see:

ls

build  install  log  src


📌 install/ contains setup files for your overlay

✅ Step 6: Source the overlay (IMPORTANT)

🚨 Open a NEW terminal
Never build and source in the same terminal.

In the new terminal:

Source ROS 2 underlay:

source /opt/ros/jazzy/setup.bash


Go to workspace:

cd ~/ros2_ws


Source overlay:

source install/local_setup.bash


Now run turtlesim:

ros2 run turtlesim turtlesim_node


✔ This turtlesim is coming from your overlay workspace

7️⃣ Step 7: Modify the overlay (prove it works)

Edit turtlesim source code:

nano ~/ros2_ws/src/ros_tutorials/turtlesim/src/turtle_frame.cpp


Find:

setWindowTitle("TurtleSim");


Change to:

setWindowTitle("MyTurtleSim");


Save and exit.

Rebuild (old terminal):
cd ~/ros2_ws
colcon build

Run again (overlay terminal):
ros2 run turtlesim turtlesim_node


🎉 Window title will show MyTurtleSim

8️⃣ Verify underlay is untouched

Open another brand-new terminal:

source /opt/ros/jazzy/setup.bash
ros2 run turtlesim turtlesim_node


✔ Title will be TurtleSim (original)

This proves:

Overlay ≠ Underlay

Your system ROS 2 is safe

🧠 Key concepts you just learned
Concept	Meaning
Workspace	Folder containing ROS 2 packages
Underlay	Base ROS 2 installation
Overlay	Your development workspace
colcon build	Builds packages
local_setup.bash	Activates overlay
Overlay precedence	Overlay overrides underlay
