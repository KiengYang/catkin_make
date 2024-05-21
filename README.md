## Autonomous Mobile Robot with TurtleBot3 (ROS Noetic)

This repository documents the development of an Autonomous Mobile Robot (AMR) using TurtleBot3 in a ROS Noetic environment.

### System Architecture

**Hardware:**

* TurtleBot3 model (Burger, Waffle) 
* Additional sensors used (LiDAR) 
* Computing platform (PC or Laptop)

**Software:**

* Ubuntu version: 20.04
* ROS version: Noetic
* Navigation packages: turtlebot3_navigation
* Localization method: SLAM
  
### Hardware Setup

This section should link to the official TurtleBot3 assembly manuals and provide details on:

* Connection details between robot components and computer
* Sensor mounting and calibration procedures (if applicable)


**Software Implementation Details**

**1. Prerequisites:**

   - Ensure you have a Ubuntu 20.04 system with ROS Noetic installed. Refer to the official ROS installation guide for detailed instructions: [http://wiki.ros.org/melodic/Installation/Ubuntu](http://wiki.ros.org/melodic/Installation/Ubuntu)

**2. Clone the Repository:**

   ```bash
   git clone https://github.com/KiengYang/catkin_make.git
   ```

**3. Navigate to Workspace:**

   ```bash
   cd catkin_make/src
   ```

**4. Download package**

   ```git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
   ```

**5. Build the Workspace:**

   ```cd
   ~/catkin && catkin_make
   ```

**6. Source ROS Environment Variables:**

   ```source
   ~/catkin_make/devel/setup.bash
   ```

**Running the Robot**

**1. Launch Simulation World (Burger Model):**

   ```bash
   export TURTLEBOT3_MODEL=burger
   roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
   ```

**2. Launch TurtleBot3 World (Waffle Model):**

   ```bash
   export TURTLEBOT3_MODEL=waffle
   roslaunch turtlebot3_gazebo turtlebot3_world.launch
   ```

**3. Teleoperate the Robot:**

   ```bash
   roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
   ```

**4. Run SLAM (Gmapping):**

   ```bash
   roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
   ```

**5. Save the Generated Map:**

   ```bash
   rosrun map_server map_saver -f ~/map
   ```

   **Note:** This saves the map to your home directory (`~/map`). You can change the filename and location if desired.

**6. Run Navigation Node (Using Saved Map):**

   ```bash
   roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
   ```

**7. Set Initial Pose in RViz**

   - Open RViz by running `rviz`.
   - Click the "2D Pose Estimate" button in the RViz menu bar.
   - Click on the map where the robot is currently located.
   - Drag the green arrow to indicate the robot's orientation.
   - Repeat steps a-c until the LiDAR sensor data aligns with the saved map. Use keyboard teleoperation (`roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`) for precise positioning if needed.

**8. Set Navigation Goal in RViz**

   - Click the "2D Nav Goal" button in the RViz menu bar.
   - Click on the desired destination point on the map.

**Troubleshooting and Tips:**

* Ensure the `TURTLEBOT3_MODEL` environment variable is set correctly for the model you're using.
* Double-check ROS package dependencies and ensure they are built and sourced correctly.
* Refer to the official ROS documentation and TurtleBot3 tutorials for advanced usage and troubleshooting: 
