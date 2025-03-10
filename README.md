# Drone-Landing-on-Boats
Simulation of the landing of PX4 quadcopters—equipped with a gimbal/camera and carrying parcels—on boats in a Gazebo wave environment using novel reinforcement learning techniques

Below are the steps to integrate the [asv_wave_sim](https://github.com/srmainwaring/asv_wave_sim) world with a PX4 drone on Ubuntu 24.04:

1. Install [Gazebo Harmonic](https://gazebosim.org/docs/harmonic/install_ubuntu/)
2. Install [PX4](https://docs.px4.io/main/en/dev_setup/dev_env_linux_ubuntu.html ) 
3. Install [asv_wave_sim](https://github.com/srmainwaring/asv_wave_sim), making sure to build the wave control plugin
4. Place the gz_ws folder into the PX4-Autopilot folder.
5. Add [this modified waves.sdf file](https://pastebin.com/ududh4dR) to the PX4-Autopilot/Tools/simulation/gz/worlds folder
6. `cd PX4-Autopilot/gz_ws`
7. 'source ./install/setup.bash'
8. Set environment variables
   
```
export GZ_VERSION=harmonic

export GZ_IP=127.0.0.1

export GZ_SIM_RESOURCE_PATH=\
$GZ_SIM_RESOURCE_PATH:\
$HOME/PX4-Autopilot/gz_ws/src/asv_wave_sim/gz-waves-models/models:\
$HOME/PX4-Autopilot/gz_ws/src/asv_wave_sim/gz-waves-models/world_models:\
$HOME/PX4-Autopilot/gz_ws/src/asv_wave_sim/gz-waves-models/worlds

export GZ_SIM_SYSTEM_PLUGIN_PATH=\
$GZ_SIM_SYSTEM_PLUGIN_PATH:\
$HOME/PX4-Autopilot/gz_ws/install/lib

export GZ_GUI_PLUGIN_PATH=\
$GZ_GUI_PLUGIN_PATH:\
$HOME/PX4-Autopilot/gz_ws/src/asv_wave_sim/gz-waves/src/gui/plugins/waves_control/build
```

9. Install QGroundControl https://docs.px4.io/main/en/dev_setup/qgc_daily_build.html 
10. Open terminal and run ./QGroundControl.AppImage 
11. Open a new terminal window and run `PX4_SYS_AUTOSTART=4001 PX4_GZ_WORLD=waves PX4_GZ_MODEL_POSE="0,0,5" PX4_SIM_MODEL=gz_x500_gimbal ./build/px4_sitl_default/bin/px4` to spawn a drone with gimbal above wam-v
12. Wait a few seconds and QGroundControl will display "Ready To Fly". 
