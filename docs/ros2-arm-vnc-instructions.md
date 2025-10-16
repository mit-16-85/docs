# Running ROS2 on ARM Macs

## 1. Install Docker Desktop for Mac
* Download Docker Desktop from https://www.docker.com/products/docker-desktop.
* Follow the installation instructions and start Docker Desktop.
* Ensure Docker is configured to run Linux containers, which is the default setting.

## 2. Install TigerVNC to Create a Virtual Display
* While any VNC viewer can be used, TigerVNC is free and available on Homebrew (https://tigervnc.org/). 
* Install the viewer using the following command: 
    ```sh
    brew install tigervnc-viewer
    ```
* It should automatically appear in your applications folder. 

## 3. Create a Local ROS 2 Workspace Directory
* This directory is needed for image configuration files and to share code between your Mac and the Docker container.
* The `~` places the directory in your home folder (`users/[your username]/`).
* Create the directory with this command: 
    ```sh
    mkdir -p ~/ros2_ws_VNC/src
    ```

## 4. Create `Dockerfile` and `start_vnc.sh` Inside the Directory
* The first file must be named `Dockerfile` (case-sensitive) with no extension. 
    * **Note:** macOS might automatically add a `.txt` extension and hide it. Check in 'Get Info' to ensure the filename is correct. 
* The `Dockerfile` should contain the following: 
    ```dockerfile
    # Use official ROS 2 Humble desktop image
    FROM osrf/ros:humble-desktop
    
    # Install packages: Xvfb (virtual X server), x11vnc (VNC server), fluxbox (lightweight window manager), net-tools (optional for debugging)
    RUN apt-get update && apt-get install -y \
    xvfb \
    x11vnc \
    fluxbox \
    net-tools \
    && rm -rf /var/lib/apt/lists/*
    
    # Set environment variables for ROS 2 Humble
    ENV ROS_DISTRO humble
    ENV DISPLAY $=:1$
    
    # Copy start script to container
    COPY start_vnc.sh /start_vnc.sh
    RUN chmod +x /start_vnc.sh
    
    # Default command runs the start script
    CMD ["/start_vnc.sh"]
    ```
* The `start_vnc.sh` file should contain the following:
    ```bash
    #!/bin/bash
    set -e
    
    Xvfb:1-screen 0 1440x900x24 &
    fluxbox &
    x11vnc-display:1-forever-nopw -shared &
    sleep 2
    
    source /opt/ros/humble/setup.bash
    
    # Do not launch rviz2 here!
    # Instead, keep the container running with a sleep or bash to keep X and VNC alive.
    tail -f /dev/null
    ```

## 5. Build the Docker Image
* Open a terminal window and navigate to your directory. 
* Run the following command (note the period at the end): 
    ```sh
    docker build -t ros2-humble-vnc .
    ```
* This step must be redone if you make any changes to the configuration files, such as changing the screen resolution. 

## 6. Run a Docker Container
* In the same directory, run the following command as a single line: 
    ```sh
    docker run -it --rm -p 5900:5900 --name ros2_humble_vnc_container ros2-humble-vnc
    ```
* This process must always be running for the virtual display to be active.

## 7. Connect to the Virtual Display on Mac
* Open the TigerVNC Viewer application. 
* Connect to the display by typing the following into the connection box: 
    ```
    localhost:5900
    ```
* A window should pop up showing an empty Linux desktop. 

## 8. Set Up the ROS 2 Shell
* Open a new terminal window on your Mac and start a ROS 2 shell by running these two commands sequentially: 
    ```sh
    docker exec -it ros2_humble_vnc_container bash
    ```
    ```sh
    source /opt/ros/humble/setup.bash
    ```
   
* Test that this works by running `rviz2`; it should launch in the TigerVNC window.
* You can open multiple terminals this way for other nodes. 