# Use official ROS Jazzy base image (Ubuntu 24.04)
FROM ros:jazzy

# Remove old ROS keys (safety)
RUN rm -f /usr/share/keyrings/ros* && rm -f /etc/apt/trusted.gpg.d/ros*

# Create keyrings directory
RUN mkdir -p /usr/share/keyrings

# Install curl + gnupg
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    && rm -rf /var/lib/apt/lists/*

# Add latest ROS key
RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
    | gpg --dearmor -o /usr/share/keyrings/ros2-latest-archive-keyring.gpg

# Environment
ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_WS=/root/ros2_ws

# Common utilities
RUN apt-get update && apt-get install -y \
    python3-pip \
    git \
    wget \
    build-essential \
    cmake \
    nano \
    vim \
    x11-utils \
    && rm -rf /var/lib/apt/lists/*

# ROS 2 Jazzy + Gazebo Harmonic
RUN apt-get update && apt-get install -y \
    ros-jazzy-desktop \
    ros-jazzy-ros-gz-sim \
    ros-jazzy-ros-gz-bridge \
    ros-jazzy-ros2-control \
    ros-jazzy-ros2-controllers \
    && rm -rf /var/lib/apt/lists/*

# Python venv for RL stack
RUN apt-get update && apt-get install -y python3-venv

RUN python3 -m venv /opt/rl_venv
ENV PATH="/opt/rl_venv/bin:$PATH"

RUN pip install --no-cache-dir \
    torch \
    gym \
    stable-baselines3 \
    pybullet \
    numpy \
    matplotlib


# Workspace
RUN mkdir -p $ROS_WS
WORKDIR $ROS_WS

# Auto-source ROS
SHELL ["/bin/bash", "-c"]
RUN echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc

ENTRYPOINT ["/bin/bash"]