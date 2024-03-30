FROM osrf/ros:galactic-desktop

ARG USERNAME
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

SHELL ["/bin/bash", "-c"]

# Create the user; see https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user 
RUN groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid ${USER_UID} --gid ${USER_GID} -m -s /bin/bash ${USERNAME}

RUN apt-get update && apt-get install -y sudo \
    && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER ${USERNAME}

RUN echo "source /opt/ros/galactic/setup.bash" >> /home/${USERNAME}/.bashrc

CMD ["/bin/bash"]

