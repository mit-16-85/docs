# Computer Setup

## Create Login
- `Settings > Users > Unlock > Add User...`
- Login as new user
```
# see swarm's groups
$ groups swarm
swarm adm dialout cdrom sudo dip video plugdev lpadmin lxd sambashare docker

# give same groups to self
$ sudo usermod -aG $(groups swarm | cut -d ":" -f 2 | xargs | cut -d " " -f 2- | sed 's/ /,/g') $USER
# sudo usermod -aG adm,dialout,cdrom,sudo,dip,video,plugdev,lpadmin,lxd,sambashare,docker
 $USER
```
- Restart to ensure new permissions (e.g., `dialout`) take.

## Source ROS2
```
echo "source /opt/ros/*/setup.bash >> ~/.bashrc
source ~/.bashrc

# test
ros2
```

## Setup Mocap & Zenoh

```
mkdir -p ~/ws/src
cd ~/ws/src

git clone https://gitlab.com/mit-acl/fsw/mocap
git clone https://github.com/pac-ws/zenoh_vendor.git

cd ..
colcon build

echo "source ~/ws/install/setup.bash" >> ~/.bashrc
echo 'alias mocap="ros2 launch mocap vicon.launch.xml"' >> ~/.bashrc
echo 'alias zenoh="ros2 run zenoh_vendor zenoh-bridge-ros2dds -c ~/ws/src/zenoh_vendor/configs/zenoh_gcs.json5"' >> ~/.bashrc
```

## Setup QGC
- Go to: https://github.com/mavlink/qgroundcontrol/release/latest
- Download the AppImage
```
mkdir -p ~/apps
cd apps
mv ~/Downloads/QGroundControl-x86_64.AppImage .
chmod +x QGroundControl-x86_64.AppImage
echo 'alias qgc="~/apps/QGroundControl-x86_64.AppImage"' >> ~/.bashrc
```

## Config Static IP
```
firefox 192.168.0.1
```

## SSH
Create a `config` file for your `ssh` client:
```
mkdir -p ~/.ssh
vi ~/.ssh/config
```

A simple example config might look like:
```
Host d01
    HostName 192.168.0.159
    User acl-1685
```

Create and copy a key from host to robot:
```
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub d01
```