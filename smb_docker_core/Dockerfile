FROM osrf/ros:noetic-desktop-full

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics
    
    
RUN apt update
RUN apt install -y python3-catkin-tools python3-pip python3-vcstool git software-properties-common wget vim nano 


RUN rosdep update


RUN mkdir -p /home/catkin_ws/src && \
    cd home/catkin_ws && \
    catkin init && \
    catkin config --extend /opt/ros/noetic -DCMAKE_BUILD_TYPE=Release && \
    cd src && \
    mkdir hardware ui && \
    git clone https://github.com/ETHZ-RobotX/smb_common.git core && \
    git clone https://github.com/tomlogan501/robosense_simulator.git hardware/robosense_simulator && \
    git clone https://github.com/ETHZ-RobotX/smb_powerstatus.git hardware/smb_powerstatus && \
    git clone https://github.com/ETHZ-RobotX/smb_rviz_plugins.git ui/smb_rviz_plugins && \
    rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y && \
    catkin build smb_gazebo

RUN mkdir /home/catkin_ws/src/.vscode   
ADD ./.vscode/* /home/catkin_ws/src/.vscode
WORKDIR /home/catkin_ws/src
