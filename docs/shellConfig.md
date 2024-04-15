```sh
source /opt/ros/iron/setup.sh
export GZ_SIM_SYSTEM_PLUGIN_PATH=$HOME/gz_ws/src/ardupilot_gazebo/build:$GZ_SIM_SYSTEM_PLUGIN_PATH
export GZ_SIM_RESOURCE_PATH=$HOME/gz_ws/src/ardupilot_gazebo/models:$HOME/gz_ws/src/ardupilot_gazebo/worlds:$GZ_SIM_RESOURCE_PATH
export PATH=$PATH:$HOME/ardupilot/ArduCopter/:$HOME/ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH
export GAZEBO_MODEL_PATH=${GAZEBO_MODEL_PATH}:$HOME/catkin_ws/src/iq_sim/models
alias sim="sim_vehicle.py"
```