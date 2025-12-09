# tiago_meta
## Overview

This repository serves as a meta workspace for organizing and managing future robotics projects using ROS 2 Humble as the base. It provides a structured environment to streamline development, integration, and deployment of ROS 2 packages and related tools.

## Getting Started

### Docker Configuration

To set up the development environment using Docker:

1. Clone this repository:
    ```bash
    git clone https://github.com/ffpangestu/tiago_meta.git
    cd tiago_meta/containers
    ```
2. Build the Docker image:
    ```bash
    docker build -t tiago_gazebo:humble .
    ```
3. Run the container:
    ```bash
    docker run -it \
      --privileged \
      --network=host \
      --ipc=host \
      -e DISPLAY \
      -v /tmp/.X11-unix:/tmp/.X11-unix:rw \
      -v "$(pwd)/..":/home/ubuntu/workspace/project \
      -w /home/ubuntu/workspace \
      tiago_gazebo:latest
    ```

### VS Code Dev Container (Optional)

You can run this docker container directly in VS Code. Open the folder in VS Code and select "Reopen in Container" to start developing in a pre-configured environment.