# Running Mighty on ARM Macs

## 1. Install Docker Desktop for Mac
* Download Docker Desktop from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
* OPTIONAL (but recommended): Go to Settings -> Resources -> Resource Allocation and move all sliders to their maximum position. To build the image on your own machine you will need at least 16 GB of RAM and 4 GB of swap.

***

## 2. Install TigerVNC to Create a Virtual Display
* While any VNC viewer can be used, TigerVNC is free and available on Homebrew ([https://tigervnc.org/](https://tigervnc.org/)). 
* Install the viewer using the following command: 
    ```sh
    brew install tigervnc-viewer
    ```
* It should automatically appear in your applications folder. 

***

## 3. Clone the Repository and Navigate to the Docker Folder:
   ```sh
   mkdir -p ~/code/ws/src
   cd ~/code/ws/src
   git clone https://github.com/mit-acl/mighty.git
   cd mighty/docker
   git switch 16.85
   ```

## 4. OPTION 1: Modify `Dockerfile` and `mighty.sh` Inside the Directory
* Add the following code to the  `Dockerfile` just before the `# Set up Entry Point` Comment: 
    ```dockerfile
    # --- Add lightweight desktop + TigerVNC ---
    RUN apt-get update && apt-get install -y software-properties-common && \
        add-apt-repository universe && \
        apt-get update && \
        apt-get install -y \
            xvfb \
            x11vnc \
            fluxbox \
            net-tools && \
        rm -rf /var/lib/apt/lists/*

    # --- Environment for VNC ---
    ENV DISPLAY=:1
    ```
* Add this code to  `mighty.sh` after the first commented line:
    ```bash
    # --- Start TigerVNC (no password, XFCE desktop) ---
    set -e
    Xvfb :1 -screen 0 1440x900x24 &
    fluxbox &
    x11vnc -display :1 -forever -nopw -shared &
    sleep 2
    ```
* This is where the screen resolution and port number are assigned.
***

## 4. OPTION 2: Download and Load the Pre-Built Docker Image
* Download `mightyARM.tar` from [https://drive.google.com/file/d/1T90HYWYy3yFQD2NMCkAU0RMv6OuJWxr2/view?usp=sharing](https://drive.google.com/file/d/1T90HYWYy3yFQD2NMCkAU0RMv6OuJWxr2/view?usp=sharing) and put it in the same directory.
* Load the image:
    ```sh
    docker load -i mightyARM.tar
    ```
* Only recommended if your machine does not have the resources to build the image, you will lose the ability to modify the screen resolution and port assignment.
***

## 5. Build the Docker Image With Emulation 
* In the same directory, run the following command to force an emulated build and allow gazebo to run on ARM architecture: 
    ```sh
    docker build --platform linux/amd64 -t mighty .
    ```
* This step must be redone if you make any changes to the configuration files, such as changing the screen resolution. 

***

## 6. Run the Example Simulation
* In the same directory, run this command to start the container and the loaded simulation: 
    ```sh
    docker run -it \
      --platform=linux/amd64 \
      --privileged \
      -p 5900:5900 \
      --rm mighty
    ```
* You'll know this was successful when the tmux window appears in your terminal with a green bar, it could take a while.

***

## 7. Connect to the Virtual Display on Mac
* Open the TigerVNC Viewer application. 
* Connect to the display by typing the following into the connection box: 
    ```
    localhost:5900
    ```
* A window should pop up showing the simulation.
* If the tmux window hasn't appeared yet you may not be able to connect since the container will not be broacasting a display yet. 

***
