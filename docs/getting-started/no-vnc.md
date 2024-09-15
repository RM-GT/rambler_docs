# NoVNC-based Installation

Docker is a faster and more lightweight alternative comparing to normal virtual machines like VMWare and VirtualBox.
## Install Docker

Choosing an appropriate instruction based on your operating system:

- [Windows Instructions](https://docs.docker.com/desktop/windows/install/)
- [Mac Instructions](https://docs.docker.com/desktop/mac/install/)
- [Ubuntu Instructions](https://docs.docker.com/engine/install/ubuntu/)

## Pull and Run Docker Image

Starting your command terminal, run:

```bash
docker run -p 6080:80 --security-opt seccomp=unconfined --shm-size=512m tiryoh/ros2-desktop-vnc:humble
```

ROS2-Desktop-VNC is a docker image that contains NoVNC and humble environment installed. This command launch the image at port 6080, so you can directly access it through the browser.

To see more detailed, check [README for the original image](https://github.com/Tiryoh/docker-ros2-desktop-vnc?tab=readme-ov-file).
