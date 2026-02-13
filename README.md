# Autonomous Mobile Robot (ROS 2 Jazzy)

A complete autonomous differential drive robot built with **ROS 2 Jazzy**. This project demonstrates Simulation, Simultaneous Localization and Mapping (SLAM), and Autonomous Navigation using the Nav2 stack.


## Features

* ** Teleoperation:** Manual control using keyboard teleop.
* **SLAM (Simultaneous Localization & Mapping):** Generates 2D occupancy grid maps using `slam_toolbox`.
* **Autonomous Navigation:** Fully integrated with the **Nav2** stack for path planning and obstacle avoidance.
* **Perception:** Equipped with Lidar and Camera sensors (simulated in Gazebo).

---

## Prerequisites

* **OS:** Ubuntu 24.04 (Noble Numbat)
* **ROS 2 Distro:** Jazzy Jalisco
* **Simulator:** Gazebo Harmonic

### Dependencies
Install the required ROS 2 packages:
```bash
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-slam-toolbox ros-jazzy-ros-gz
```

---

## Installation

1.  **Clone the repository:**
    ```bash
    mkdir -p ~/ros2_ws/src
    cd ~/ros2_ws/src
    git clone https://github.com/PukyBots/Autonomous-Navigation-Robot.git](https://github.com/PukyBots/Robot-Car-Simulation-with-Gazebo-and-Rviz.git
    ```

2.  **Build the workspace:**
    ```bash
    cd ~/ros2_ws
    colcon build --packages-select diff_drive_robot --symlink-install
    source install/setup.bash
    ```

---

## Usage Guide

### 1. Launch Simulation

set the Resource Path:

```
export GZ_SIM_RESOURCE_PATH=~/ros2_ws/src/Autonomous-Navigation-Robot/assets/gazebo_models:$GZ_SIM_RESOURCE_PATH
```

Start the robot in the Gazebo environment:
```bash
ros2 launch diff_drive_robot robot.launch.py use_sim_time:=true
```

### 2. Mapping Mode (SLAM)
To create a new map of the environment:
```bash
ros2 launch diff_drive_robot mapping.launch.py use_sim_time:=true
```

* **Control:** Open a new terminal and run:
    ```bash
    ros2 run teleop_twist_keyboard teleop_twist_keyboard
    ```
* **Save Map:** When finished mapping, run:
    ```bash
    ros2 run nav2_map_server map_saver_cli -f ~/my_map
    ```

### 3. Autonomous Navigation

To run the full system, you need to type the following in the terminal-

### Terminal: Simulation (Gazebo)

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 launch diff_drive_robot bringup.launch.py

```

#### How to Navigate:
1.  Open **RViz**.
2.  Click **"2D Pose Estimate"** and set the robot's current position on the map.
3.  Click **"Nav2 Goal"** and click anywhere on the map to send the robot there!

---

## Project Structure

```bash
diff_drive_robot/
├── launch/             # Launch files for Robot, Mapping, and Navigation
├── urdf/               # Robot description (Xacro/URDF)
├── worlds/             # Gazebo world files
├── maps/               # Saved maps (.yaml and .png)
├── rviz/               # RViz configuration files
└── package.xml
```

---

## Author

**Pulkit Garg**
