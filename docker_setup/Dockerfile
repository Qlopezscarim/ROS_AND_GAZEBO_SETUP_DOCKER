# Use official ROS Humble base image
FROM ros:humble

# Set environment
ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_WS=/root/ros2_ws

# Update system and install common utilities
RUN apt-get update && apt-get install -y \
    python3-pip \
    git \
    curl \
    wget \
    build-essential \
    cmake \
    nano \
    vim \
    x11-utils \
    && rm -rf /var/lib/apt/lists/*

# Install ROS 2 packages and Gazebo Sim (Ignition Fortress recommended for Humble)
RUN apt-get update && apt-get install -y \
    ros-humble-desktop \
    ros-humble-gazebo-ros-pkgs \
    ros-humble-ros-gz-bridge \
    ros-humble-ros2-control \
    ros-humble-ros2-controllers \
    && rm -rf /var/lib/apt/lists/*

# Optional: install Python packages for RL
RUN pip3 install --no-cache-dir \
    torch \
    gym \
    stable-baselines3 \
    pybullet \
    numpy \
    matplotlib

# Set up ROS workspace mount point
RUN mkdir -p $ROS_WS
WORKDIR $ROS_WS

# Source ROS on container startup
SHELL ["/bin/bash", "-c"]
RUN echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc

# Set entrypoint
ENTRYPOINT ["/bin/bash"]
