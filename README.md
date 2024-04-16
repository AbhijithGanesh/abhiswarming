Certainly! Here's the document with an added index:

---

# Abhiswarming ROS package

## Index
1. [Requirements](#requirements)
2. [Special Instructions](#special-instructions)
    - [Add ROSDEP dependencies](#add-rosdep-dependencies)
    - [Micro-XRCE-DDS-Gen](#micro-xrce-dds-gen)
    - [ArduPilot Installation](#ardupilot-installation)
        - [Ardupilot](#ardupilot)
        - [Ardupilot Plugin](#ardupilot-plugin)
    - [Special Python3 Link](#special-python3-link)
    - [ROS2 Check](#ros2-check)
    - [MAV Proxy](#mav-proxy)

## Requirements <a id="requirements"></a>

To use the Abhiswarming ROS package, ensure you have the following software installed:

1. **MicroXRCE**
2. **ArduPilot**
3. **Gazebo8**
4. **MAVProxy**
5. **ROS2 - Iron**

These components are essential for proper functionality. Additionally, clone the following repository into your workspace directory:

```sh
git clone https://github.com/micro-ROS/micro-ROS-Agent.git ~/workspace_dir
```

Before proceeding, run `colcon build`.

## Special Instructions <a id="special-instructions"></a>

### Add ROSDEP dependencies <a id="add-rosdep-dependencies"></a>

```sh
cd ~/ros2_ws
source /opt/ros/humble/setup.bash
sudo apt update
rosdep update
rosdep install --from-paths src --ignore-src -r
```

### Micro-XRCE-DDS-Gen <a id="micro-xrce-dds-gen"></a>

**Warning: Ensure JAVA is installed**
MicroXRCE requires Java to function properly.

```sh
git clone --recurse-submodules https://github.com/ardupilot/Micro-XRCE-DDS-Gen.git
cd Micro-XRCE-DDS-Gen
./gradlew assemble
```

### ArduPilot Installation <a id="ardupilot-installation"></a>

#### Ardupilot <a id="ardupilot"></a>

Navigate to the home directory:

```sh
cd ~
sudo apt install git
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
git checkout Copter-3.6
git submodule update --init --recursive
```

Install required dependencies:

```sh
sudo apt install python-matplotlib python-serial python-wxgtk3.0 python-wxtools python-lxml python-scipy python-opencv ccache gawk python-pip python-pexpect
```

Install Python packages:

```sh
sudo pip install future pymavlink MAVProxy
```

Append the following lines to the end of either `~/.bashrc` or `~/.zshrc`:

```sh
export PATH=$PATH:$HOME/ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH
```

#### Ardupilot Plugin <a id="ardupilot-plugin"></a>

1. Install required dependencies:

    ```sh
    sudo apt install libgz-sim8-dev rapidjson-dev
    ```

2. Set up Gazebo workspace:

    ```sh
    mkdir -p gz_ws/src && cd gz_ws/src
    git clone https://github.com/ArduPilot/ardupilot_gazebo
    ```

3. Build ArduPilot Gazebo plugin:

    ```sh
    export GZ_VERSION=harmonic
    cd ardupilot_gazebo
    mkdir build && cd build
    cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo
    make -j4
    ```

### Special Python3 Link <a id="special-python3-link"></a>

To ensure ArduPilot functions correctly, create a symbolic link for `python`:

```sh
ln -s /usr/bin/python3 /usr/bin/python
```

This command creates a soft link named `python` pointing to `/usr/bin/python3`.

### ROS2 Check <a id="ros2-check"></a>

```sh
source ~/ros2_ws/install/setup.bash
# See the node appear in the ROS graph
ros2 node list
# See which topics are exposed by the node
ros2 node info /ardupilot_dds
# Echo a topic published from ArduPilot
ros2 topic echo /ap/geopose/filtered
```

### MAV Proxy <a id="mav-proxy"></a>

```sh
mavproxy.py --console --map --aircraft test --master=:14550
```

Following these instructions will ensure the successful setup and operation of the Abhiswarming ROS package.
