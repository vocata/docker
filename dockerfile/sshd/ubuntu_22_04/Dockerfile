FROM ubuntu:jammy

ARG USERNAME=docker
ARG HOMEPATH=/home/$USERNAME

RUN yes | unminimize

RUN apt-get update && apt-get -y install build-essential wget curl vim sudo openssh-server net-tools iputils-ping iproute2

RUN useradd -m -s /bin/bash $USERNAME && echo "$USERNAME:$USERNAME" | chpasswd && adduser $USERNAME sudo

RUN ssh-keygen -A && mkdir /run/sshd

# USER $USERNAME
# WORKDIR $HOMEPATH

COPY proxy $HOMEPATH/.proxy

CMD ["/usr/sbin/sshd", "-D"]
