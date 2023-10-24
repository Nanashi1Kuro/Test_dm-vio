FROM osrf/ros:noetic-desktop-full-focal
RUN for retry in $(seq 10); do apt-get update -o Acquire::https::Verify-Peer="false" -o Acquire::https::Verify-Host="false" -o Acquire::AllowInsecureRepositories="true" && break; done
RUN apt-get upgrade -y
RUN apt-get install sudo -y
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN apt-get install -y git

RUN mkdir packages
WORKDIR /packages
RUN git clone https://github.com/Nanashi1Kuro/dm-vio.git
RUN apt-get install -y wget
RUN apt-get install -y cmake libsuitesparse-dev libboost-all-dev libyaml-cpp-dev libeigen3-dev
RUN apt install -y libtbb-dev

#RUN git clone https://gitlab.com/libeigen/eigen.git
#WORKDIR /packages/eigen
#RUN mkdir build
#WORKDIR /packages/eigen/build
#RUN cmake ..
#RUN cmake --build .
#RUN make install

WORKDIR /packages
RUN git clone https://github.com/borglab/gtsam.git
RUN cd gtsam 
WORKDIR /packages/gtsam
RUN git checkout 4.2a6     
RUN mkdir build
WORKDIR /packages/gtsam/build
RUN cmake -DGTSAM_POSE3_EXPMAP=ON -DGTSAM_ROT3_EXPMAP=ON -DGTSAM_USE_SYSTEM_EIGEN=ON -DGTSAM_BUILD_WITH_MARCH_NATIVE=OFF ..
RUN make -j6
RUN make install
RUN cd ..
RUN cd ..
WORKDIR /packages
RUN apt install -y libgl1-mesa-dev libglew-dev pkg-config libegl1-mesa-dev libwayland-dev libxkbcommon-dev wayland-protocols
RUN git clone https://github.com/stevenlovegrove/Pangolin.git
WORKDIR /packages/Pangolin
RUN git checkout v0.6
RUN mkdir build
#RUN cd build
WORKDIR /packages/Pangolin/build
RUN cmake ..
RUN cmake --build .
RUN make install
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0AD9A3000D97B6C9
RUN sh -c 'echo "deb [arch=amd64] http://packages.usenko.eu/ubuntu $(lsb_release -sc) $(lsb_release -sc)/main" > /etc/apt/sources.list.d/basalt.list'
RUN apt-get update
RUN apt install -y librealsense2-dev
WORKDIR /packages/
RUN apt-get install -y curl apt-transport-https
RUN cd ..
RUN cd ..
WORKDIR /packages/
RUN mkdir -p /etc/apt/keyrings
RUN curl -sSf https://librealsense.intel.com/Debian/librealsense.pgp | sudo tee /etc/apt/keyrings/librealsense.pgp > /dev/null
RUN echo "deb [signed-by=/etc/apt/keyrings/librealsense.pgp] https://librealsense.intel.com/Debian/apt-repo `lsb_release -cs` main" | \
tee /etc/apt/sources.list.d/librealsense.list
WORKDIR /packages
RUN apt-get update
RUN apt-get install -y librealsense2-dkms librealsense2-utils librealsense2-dev
RUN apt-get install -y \
        ros-noetic-navigation \
        ros-noetic-gmapping
RUN apt-get install -y mc
RUN apt-get install -y qtcreator qt5-default

WORKDIR /packages/dm-vio
RUN mkdir build
WORKDIR /packages/dm-vio/build
RUN cmake ..
RUN make -j6
WORKDIR /packages
RUN apt-get install -y python3-pip
RUN pip3 install evo --upgrade --no-binary evo

#WORKDIR /packages/mr_ws/src
#RUN export DMVIO_BUILD=/packages/dm-vio/build
#RUN git clone https://github.com/Nanashi1Kuro/dm-vio-ros.git
#RUN source /opt/ros/noetic/setup.bash
#RUN catkin_make

