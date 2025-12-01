# 🤖 Niryo Robot NED-2 — URDF & Visualization Package (ROS2)

This package provides the full **URDF, meshes, Gazebo extensions, and RViz launch files** required to visualize the **Niryo NED-2 industrial robot arm** in **ROS2**.

It is intended for simulation, visualization, research, robotics courses, and projects that require a fully modeled 6-DOF robotic arm with gripper.

---

# 📂 Package Contents

niryo_robot_ned2/
│
├── CMakeLists.txt
├── package.xml
│
├── config/
│ └── default_config.rviz
│
├── launch/
│ ├── display.launch
│ └── without_mesh_display.launch
│
├── meshes/
│ ├── gripper_1/ ← STL files for gripper components
│ ├── led_ring/ ← LED ring mesh
│ └── ned2/ ← Full robot link geometries (DAE / STL / COLLADA)
│
└── urdf/
└── ned2/
├── niryo_ned2.urdf.xacro
├── niryo_ned2_gazebo.urdf.xacro
├── niryo_ned2_camera.urdf.xacro
├── niryo_ned2_gripper1_n_camera.urdf.xacro
├── niryo_ned2.transmission.xacro
├── niryo_ned2_param.urdf.xacro
└── without_mesh_niryo_ned2.urdf.xacro



---

# 🛠 Dependencies

This package requires:

- **ROS2 Humble**
- `robot_state_publisher`
- `xacro`
- `joint_state_publisher_gui` (optional)
- `rviz2`

Install missing dependencies:

```bash
sudo apt install ros-humble-joint-state-publisher-gui
sudo apt install ros-humble-xacro
sudo apt install ros-humble-robot-state-publisher
```
---
 
# 🚀 How to Build

Clone the package into your ROS2 workspace:
```
cd ~/ros2_ws/src
git clone https://github.com/sanskarmudnur2005/ROS2_HUMBLE_NIRYO_NED_2

cd ~/ros2_ws
colcon build --symlink-install
source install/setup.bash

```
---

# ✅ How to Visualize NED-2 in RViz

You need two terminals, or three if you include joint_state_publisher.

🟦 Terminal 1 — Start robot_state_publisher

Generate URDF from Xacro:
```
cd ~/ros2_ws
source /opt/ros/humble/setup.bash
source install/setup.bash

ros2 run xacro xacro \
  ~/ros2_ws/src/niryo_robot_ned2/urdf/ned2/niryo_ned2.urdf.xacro \
  -o /tmp/ned2.urdf
```

Publish robot description:
```
ros2 run robot_state_publisher robot_state_publisher /tmp/ned2.urdf

```
Leave this terminal open and running<br>

🟩 Terminal 2 — Launch RViz
```
cd ~/ros2_ws
source /opt/ros/humble/setup.bash
source install/setup.bash

rviz2
```
Inside RViz:<br>
Add → RobotModel<br>
Set Fixed Frame = base_link<br>
(Optional) Load default RViz config:<br>

```
rviz2 -d ~/ros2_ws/src/niryo_robot_ned2/config/default_config.rviz
```
<br>

🟥 (Optional) Terminal 3 — Joint State Publisher GUI

If you want to manually move the robot joints:
```
ros2 run joint_state_publisher_gui joint_state_publisher_gui
```

---

# 🎯 Additional Launch Files
1️⃣ With full meshes
```
ros2 launch niryo_robot_ned2 display.launch
```

2️⃣ Without heavy meshes (faster RViz)
```
ros2 launch niryo_robot_ned2 without_mesh_display.launch
```

---

⭐ License

Open-source under the license declared in package.xml.
