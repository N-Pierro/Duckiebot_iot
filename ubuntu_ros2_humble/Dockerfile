# using a ubuntu linux image 
FROM ubuntu:22.04


ENV DEBIAN_FRONTEND=noninteractive
# update packages and install required tools 

RUN apt update && apt install -y sudo curl locales gnupg2 lsb-release build-essential && \
    locale-gen en_US.UTF-8 && \
    update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 && \
    export LANG=en_US.UTF-8 


# create new user 'duckie' with sudo permission
RUN useradd -m -s /bin/bash duckie && \
    echo "duckie:duckie" | chpasswd && \
    echo "duckie ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/duckie
    
    
# Add the ROS 2 GPG key with apt
# Add the repository to source list

RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null && \


    #sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key | apt-key add - && \
    #sudo sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list' && \
    #update and install ros_humble-desktop
    sudo apt update && apt install -y ros-humble-desktop && \
    # Source the ros 2 setup script
    sudo echo "source /opt/ros/humble/setup.bash" >> /etc/bash.bashrc


CMD [ "/bin/bash" ]

