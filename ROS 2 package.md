1️⃣ What is a ROS 2 package?

A package is a unit of code that contains nodes, configuration, and metadata.

Packages can be CMake-based (C++) or Python-based.

You can share, install, and reuse packages easily.

Minimum contents for a CMake package:

my_package/
  CMakeLists.txt
  package.xml
  include/my_package/   # headers
  src/                  # source files (nodes)

2️⃣ Prerequisites

ROS 2 workspace (ros2_ws)

ROS 2 installed and sourced

colcon installed

3️⃣ Steps to create a package
Step 1: Go to workspace src
cd ~/ros2_ws/src

Step 2: Create a C++ package
ros2 pkg create --build-type ament_cmake --license Apache-2.0 --node-name my_node my_package


--node-name my_node → creates a simple "Hello World" node

--license Apache-2.0 → sets the license

This generates:

my_package/
  CMakeLists.txt
  include/my_package/
  package.xml
  src/my_node.cpp

Step 3: Build the package

Go to workspace root:

cd ~/ros2_ws
colcon build


Optional: Build only your package:

colcon build --packages-select my_package

Step 4: Source your overlay

Open a new terminal, source ROS 2 underlay:

source /opt/ros/jazzy/setup.bash


Then source your workspace overlay:

cd ~/ros2_ws
source install/local_setup.bash

Step 5: Run your node
ros2 run my_package my_node


Expected output:

hello world my_package package

Step 6: Examine package contents

Inside ros2_ws/src/my_package:

CMakeLists.txt  include  package.xml  src


src/my_node.cpp → your C++ node code

package.xml → metadata (dependencies, license, maintainer)

Step 7: Edit package.xml (optional)

Open package.xml:

<description>Beginner client libraries tutorials practice package</description>
<maintainer email="your_email@example.com">Your Name</maintainer>
<license>Apache-2.0</license>


📌 You can add dependencies under _depend tags for future packages.

✅ Summary

Navigate to workspace src

Create package with ros2 pkg create

Build workspace with colcon build

Source workspace overlay

Run your node with ros2 run

Edit package.xml for metadata and dependencies
