# rbq_ros2

ROS 2 message and interface packages for the [Rainbow Robotics](https://www.rainbow-robotics.com/) **RBQ** quadruped robot.

## Install

Once released to the ROS 2 build farm:

```bash
sudo apt install ros-humble-rbq-msgs
```

Until then, build from source:

```bash
mkdir -p ~/rbq_ros2_ws/src && cd ~/rbq_ros2_ws/src
git clone https://github.com/RainbowRobotics/rbq_ros2.git
cd ~/rbq_ros2_ws
sudo rosdep init   # first time on this machine only
rosdep update
rosdep install --from-paths src --ignore-src -y
colcon build
```

## Packages

| Package | Description |
|---------|-------------|
| `rbq_msgs` | Message definitions for the RBQ quadruped robot |

More packages (`rbq_api`, `rbq_description`, `rbq_examples`, `rbq_rviz_plugins`) are planned.

## Supported distributions

| ROS 2 | Ubuntu | Status |
|-------|--------|--------|
| Humble Hawksbill | 22.04 Jammy | supported |

Jazzy and later are planned.

## Relationship to the RBQ framework — how this repo is maintained

This is a **published, downstream-facing mirror**. The canonical source lives in the RBQ
framework monorepo, under `rbq_sdk/ros2/src/`. A one-way sync mirrors each package's whole
directory (`msg/`, `CMakeLists.txt`, `package.xml`, and any `src/`, `launch/`, `urdf/`, …)
here; it never reads changes back.

**Two consequences for contributors:**

- **The `<version>` in each `package.xml` is stamped by the sync**, from the framework's
  single version source (`src/rcl/version.txt`). Do not hand-edit it — it will be overwritten.
- **Any change you make here (to `msg/`, `CMakeLists.txt`, `package.xml`, or package sources)
  is silently overwritten by the next sync.** To propose a change, open an issue instead; it
  has to land in the framework repo first. (If external contribution volume grows, this repo
  will be promoted to the source of truth.)

## License

Apache-2.0. See [LICENSE](./LICENSE).
