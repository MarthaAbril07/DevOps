FROM ubuntu

RUN apt-get update  -y \
    && apt-get upgrade -y \ 
    && apt-get install -y \
    ssh \
    sshpass \
    sudo \
    software-properties-common

RUN add-apt-repository --yes --update ppa:ansible/ansible \
    && apt-get install -y ansible

WORKDIR /home/ansible_controller_project

COPY startup.sh .

RUN useradd -rm -d /home/ansible_controller_project -s /bin/bash -g root -G sudo -u 1001 ansible_controller_project
RUN echo ansible_controller_project:12345 | chpasswd
RUN echo "ansible_controller_project ALL=(ALL:ALL) NOPASSWD: ALL" |  EDITOR="tee -a"  visudo


RUN mkdir -p /home/ansible_controller_project/.ssh


CMD ["/bin/bash", "/home/ansible_controller_project/startup.sh"]
