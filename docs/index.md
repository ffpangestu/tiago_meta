# Index
## ROS2
  - [Useful --ros-args commands](ros-args.md)

## Project layout
    workspace/                                   # Container workspace directory
         container/                              # Mounted directory
                .devcontainer/
                       devcontainer.json         # VSCode dev container args
                       Dockerfile                # The docker container
                docs/
                       index.md                  # Documentation entrypoint
                       ...
                README.md
         additional packages/                    # Additional ROS2 packages from source
         ...
