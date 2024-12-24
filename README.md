# Container Images Used For PX4 SITL Simulation

## How-to-Build

- Clone the repositoy including submodules:

```bash
git clone https://github.com/kestr31/PX4-SITL-Containers.git --recursive
```

- Build process is automated using bash script `build.sh`.
- `build.sh` allows use of following arguments:
  - `all`: Build all modified images (AirSim, QGroundControl, ROS2).
  - `airsim`: Build AirSim image.
  - `qgc`: Build QGroundControl image.
  - `ros2`: Build ROS2 image.
- Example usage is as following:

```bash
./scripts/build.sh airsim
```

- You can modify the username in the image name by changing the `CONTAINER_BUILD_USERNAME` at `scripts/include/commonEnv.sh.`.

> Base image and tag are currently hard-coded in the script.

## List of Images Used Per SITL Simulation Service

- Services replying on images built using this repository:
  - **AirSim**: Modified from [adamrehn/ue4-runtime:22.04-cudagl12-x11](https://hub.docker.com/layers/adamrehn/ue4-runtime/22.04-cudagl12-x11/images/sha256-91ad394e6166c82457e7a4fae5eea5e95b4f58159bb018ed860525e4e7b488e1?context=explore)
  - **QGroundControl**: Submodule from [kestr31/QGC-app-docker](https://github.com/kestr31/QGC-app-docker)
  - **ROS2**: Modified from [athackst/dockerfiles (ros2)](https://github.com/athackst/dockerfiles/tree/main/ros2)
    - Based on `galactic-cuda.Dockerfile`.

- Services relying on images build by the others:
  - **PX4-Autopilot**: [px4io/px4-dev-simulation-focal:2024-05-18](https://hub.docker.com/layers/px4io/px4-dev-simulation-focal/2024-05-18/images/sha256-99716166fe296ef587fd1a97df64d0a004481ec96898e0a28d9ccbf42efa71f9?context=explore)
    - **Source**: [PX4/PX4-containers, Tag 2024-05-18](https://github.com/PX4/PX4-containers/tree/2024-05-18)
  - **Gazebo-Classic**: [althack/gazebo:gazebo11-base](https://hub.docker.com/layers/althack/gazebo/gazebo11-base/images/sha256-de4ffbf5f4b7c19b9e21731ea8a7637b4b9e1979c65fe1c35676964af0fd2f81?context=explore)
    - **Source**: [athackst/dockerfiles (gazebo)](https://github.com/athackst/dockerfiles/tree/main/gazebo)

## Downloading TensorRT debian package

- In order to build the `sitl-ros2` image, you need to download the TensorRT debian package.
- Download TensorRT debian package from [NVIDIA TensorRT](https://developer.nvidia.com/nvidia-tensorrt-8x-download)
  - EA Stands for `Early Access` and GA stands for `General Availability`. please choose the latest GA version.
  - **The package must be for CUDA 11.8 and Ubuntu 22.04.**
  - Place the package in the `Dockerfile/ROS2` directory.

---
