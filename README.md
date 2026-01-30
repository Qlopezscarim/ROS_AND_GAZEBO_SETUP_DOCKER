# General installation for the ROS + Gazebo sim/Ignation platform
## Currently these instructions are for a dockerized platform for ROS:HUMBLE and the newer gazebo
make a workspace:
```
mkdir ~/ros_humble_docker
cd ~/ros_humble_docker
```

Next you're likely going to want to add docker permissions to your user if needed:
```
sudo usermod -aG docker $USER
```

Copy the provided Dockerfile into that directory: (Found online no personal claims to have made this) <br>
Run the following command: <br>
```
docker build -t ros_humble_sim:latest .
```
