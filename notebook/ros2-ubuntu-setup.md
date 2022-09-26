# ros2-ubuntu-setup

***Author: Dingkun***

***Last Update:  2022/Sep/24***

***Visit [My GitHub](https://github.com/oct19) for more info***

---

## Ubuntu Installation

1. Download and install latest LTS version of Ubuntu as .iso file
2. Use `Rufus` software to install .iso file to USB
3. Install Ubuntu (parallel with existing operation system)
4. Use Tsinghua Ubuntu mirror (Required if in China)

        sudo sed -i "s@http://.*archive.ubuntu.com@https://mirrors.tuna.tsinghua.edu.cn@g" /etc/apt/sources.list

        sudo sed -i "s@http://.*security.ubuntu.com@https://mirrors.tuna.tsinghua.edu.cn@g" /etc/apt/sources.list

5. Update and upgrade Ubuntu

        sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade

6. Fix github connection issue (Required if in China)

    1. Open Terminal:

            sudo gedit /etc/hosts

    2. Add new line: `123.456.789 raw.githubusercontent.com` and replace `123.456.789` with the IP address, which can be found on ipaddress.com

## ROS2 Installation

***Follow instructions from ROS2 documentation for specific distribution. Here we use ROS2 Humble for demonstration.***

1. Check locale in Terminal, and make sure you have a locale which supports UTF-8

        locale

2. Setup Sources

        sudo apt install curl gnupg2

        sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg

3. Use Tsinghua ROS2 mirror (Required if in China)

        echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] https://mirrors.tuna.tsinghua.edu.cn/ros2/ubuntu jammy main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

4. Install

        sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade
        sudo apt install ros-humble-desktop

## Configuring environment

1. Add sourcing to your shell startup script, so every terminal run ROS2 on startup

        echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc

    To undo this, locate your system’s shell startup script and remove the appended source command.

2. Check environment variables

        printenv | grep -i ROS

## Testing

    ros2 run demo_nodes_cpp talker

In another terminal:

    ros2 run demo_nodes_py listener

Turtlesim

    sudo apt install -y ros-humble-turtlesim
    ros2 run turtlesim turtlesim_node

## Additional Installation

1. Github Command Line Interface

        curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
        && sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
        && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
        && sudo apt update \
        && sudo apt install gh -y

## Issues

1. command: `ros2 node list` not working

        ros2 daemon stop
        ros2 daemon start
        ros2 daemon status
