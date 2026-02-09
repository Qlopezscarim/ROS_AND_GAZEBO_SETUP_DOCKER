all:
	echo "ROS"

ROS:
	xhost +local:
	sudo systemctl start docker
	sudo systemctl enable docker
	sudo docker run -it \
	--dns 8.8.8.8 \
	--device=/dev/video0:/dev/video0 \
	--device=/dev/video1:/dev/video1 \
	--name ros_jazzy_sim_container \
	--env="DISPLAY=$$DISPLAY" \
	--env="QT_X11_NO_MITSHM=1" \
	--volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
	-v /home/qlopezscarim/ros2_ws:/root/ros2_ws \
	ros_jazzy_sim:latest

EXTROS:
	sudo docker exec -it ros_jazzy_sim_container /bin/bash

SAVEROS:
	sudo docker commit ros_jazzy_sim_container ros_jazzy_sim:latest
