FROM osrf/ros:galactic-desktop

ARG USERNAME
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

SHELL ["/bin/bash", "-c"]

RUN apt-get update --fix-missing && \
    apt-get install -y python3-pip \
    ros-galactic-rviz2 \
    ros-galactic-ackermann-msgs \
    ros-galactic-navigation2 \
    ros-galactic-xacro \
    ros-galactic-joint-state-publisher
RUN apt-get -y dist-upgrade
RUN python3 -m pip install transforms3d==0.4 numpy==1.24
# f1tenth gym
RUN git clone https://github.com/f1tenth/f1tenth_gym
RUN cd f1tenth_gym && \
    python3 -m pip install -e .

# Create the user; see https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user 
RUN groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid ${USER_UID} --gid ${USER_GID} -m -s /bin/bash ${USERNAME}

RUN apt-get update && apt-get install -y sudo \
    && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER ${USERNAME}

RUN echo "source /opt/ros/galactic/setup.bash" >> /home/${USERNAME}/.bashrc

CMD ["/bin/bash"]

