FROM osrf/ros:humble-desktop

# Add ubuntu user with same UID and GID as your host system, if it doesn't already exist
# Since Ubuntu 24.04, a non-root user is created by default with the name vscode and UID=1000
ARG USERNAME=ubuntu
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN if ! id -u $USER_UID >/dev/null 2>&1; then \
        groupadd --gid $USER_GID $USERNAME && \
        useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME; \
    fi
# Add sudo support for the non-root user
RUN apt-get update && \
    apt-get install -y sudo && \
    echo "$USERNAME ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

# Switch from root to user
USER $USERNAME

# Add user to video group to allow access to webcam
RUN sudo usermod --append --groups video $USERNAME

# Update all packages
RUN sudo apt update && sudo apt upgrade -y

# Install Git
RUN sudo apt install -y git \
    python3-vcstool \
    python3-rosdep \
    python3-colcon-common-extensions

# Rosdep update
RUN rosdep update

# Source the ROS setup file
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc

#########################
## SETUP THE WORKSPACE ##
#########################
# SHELL ["/bin/bash", "-c"]

# Import the workspace
RUN mkdir -p /home/ubuntu/workspace/tiago_ws/src
WORKDIR /home/ubuntu/workspace/tiago_ws
RUN vcs import --input https://raw.githubusercontent.com/pal-robotics/tiago_tutorials/humble-devel/tiago_public.repos src
RUN rosdep install --from-paths src -y --ignore-src

# Build the workspace
SHELL ["/bin/bash", "-c"]
WORKDIR /home/ubuntu/workspace/tiago_ws
RUN source /opt/ros/humble/setup.bash \
    && colcon build --symlink-install
RUN echo "source /home/$USERNAME/workspace/tiago_ws/install/setup.bash" >> /home/$USERNAME/.bashrc