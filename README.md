## Special Instructions

### ArduPilot Installation

To install ArduPilot, you'll need to follow these steps:

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

### Special Link

For ArduPilot to work correctly, it requires `python` to be available at `/usr/bin/env`. You can create a symbolic link for this purpose:

```sh
ln -s /usr/bin/python3 /usr/bin/python
```

This command creates a soft link named `python` pointing to `/usr/bin/python3`.
This version breaks down the ArduPilot installation process into clear steps and provides a more structured approach to the instructions. Additionally, it explains the purpose of creating the symbolic link for ArduPilot.
