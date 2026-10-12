# ROS 2 Common Interfaces

A collection of custom ROS 2 interfaces that can be reused by robotics projects.

## Repository Structure

```text
ros2-common-interfaces/
└── custom_interfaces/
    ├── action/
    │   └── OdomRecord.action
    ├── srv/
    │   ├── FindWall.srv
    │   └── TextRecognition.srv
    ├── include/
    ├── src/
    ├── CMakeLists.txt
    └── package.xml
```

## Included Interfaces

### `OdomRecord.action`

Defines an action with:
- **Goal:** no fields currently defined
- **Result:** `geometry_msgs/Point[] list_of_odoms`
- **Feedback:** `float32 current_total`

### `FindWall.srv`

Defines a service request with:
- `bool wallfound`

The response section is currently empty.

### `TextRecognition.srv`

Defines a service request with:
- `string label` — label to look for

The response contains:
- `bool success` — whether the label was found
- `int32 start_x`, `int32 start_y` — starting coordinates of the bounding box
- `int32 end_x`, `int32 end_y` — ending coordinates of the bounding box

## Dependencies

The package declares these ROS 2 dependencies:
- `ament_cmake`
- `rosidl_default_generators`
- `rosidl_default_runtime`
- `std_msgs`
- `geometry_msgs`
- `action_msgs`

## Build Instructions

This repository contains the `custom_interfaces` ROS 2 package. Clone it into the `src` directory of a ROS 2 workspace.

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
git clone <repository-url>
```

Build the interface package from the workspace root:

```bash
cd ~/ros2_ws
source /opt/ros/$ROS_DISTRO/setup.bash
rosdep install --from-paths src --ignore-src -r -y
colcon build --packages-select custom_interfaces
source install/setup.bash
```

Replace `<repository-url>` with the URL of this repository. If you already have a ROS 2 workspace, use its existing `src` directory instead of creating a new workspace.

## Verify the Interfaces

After building and sourcing the workspace, check that ROS 2 can find the generated interfaces:

```bash
ros2 interface show custom_interfaces/action/OdomRecord
ros2 interface show custom_interfaces/srv/FindWall
ros2 interface show custom_interfaces/srv/TextRecognition
```

## Usage

Projects that depend on these interfaces must build `custom_interfaces` in the same ROS 2 environment and declare the appropriate dependency in their own package configuration.

Currently, these interfaces are used by the Wall Follower TurtleBot project. Other projects can reuse them when needed.

## Notes

- This repository preserves the existing interface package structure and metadata.
- Interface definitions may evolve as the projects using them develop.
- This README does not change the package's license or other package metadata.
