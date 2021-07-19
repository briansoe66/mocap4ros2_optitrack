# mocap4ros2_optitrack

[![Build Status](https://travis-ci.com/MOCAP4ROS2-Project/mocap4ros2_vicon.svg?branch=master)](https://travis-ci.com/MOCAP4ROS2-Project/mocap4ros2_vicon)

This repository contains the drivers to run the mocap4ros2_project with vicon.

**To use and compile this project is obligatory to download first the [mocap_msgs](https://github.com/MOCAP4ROS2-Project/mocap_msgs) repository in your workspace and follow the next instructions:**

## Vicon DataStream SDK

Get the official binaries released in the official download page [here](https://www.vicon.com/software/datastream-sdk/?section=downloads).

You can check the documentation [here](https://docs.vicon.com/spaces/viewspace.action?key=DSSDK19).

### Installing on Linux

Copy all the libraries to /usr/local/lib and move the headers to /usr/local/include/ViconDataStreamSDK/.

```
sudo mv {YOUR_ViconDataStreamSDK}/Linux64/Release/* /usr/local/lib/
cd /usr/local/include/
sudo mkdir ViconDataStreamSDK
sudo mv ../lib/*.h ViconDataStreamSDK/
```

Update the `LD_LIBRARY_PATH` environment variable:

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib/`

It's convenient to automatically update this environment variable in your bash session every time a new shell is launched, so type it into your .bashrc file:

`echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib/"`

### Installing on Windows

Execute the installer of your distribution (typically Win64).

SDK files are placed to `C:\Program Files\Vicon\DataStream SDK\Win64\CPP` by default, so update the `PATH` environment variable with this SDK path:

`set PATH=%PATH%;C:\Program Files\Vicon\DataStream SDK\Win64\CPP`

### Guide

- Connect your computer/laptop to the same network as Vicon system is connected.

- Run Nexus (Vicon software) and calibrate cameras (if required).

- Edit some parameters on configuration file (mocap4ros2_drivers/vicon2_driver/config/vicon2_driver_params.yaml). \
e.g. `host_name` parameter.

- Launch the Vicon-ROS2 driver launcher: `ros2 launch vicon2_driver vicon2.launch.py`

- Check new topics where Vicon info is received in custom message format and TFs format.
     - This driver has one publisher that publish the markers and other TransformBroadcaster that publish the TFs.

- The vicon driver_node works to the frequency established by Vicon System.

- The vicon2_driver is a lifecycle node that has this differents states, to know the different states you can run the next command in a terminal: 

          ` 
          ros2 lifecycle list vicon2_driver_node
               - cleanup [2]
                    Start: inactive
                    Goal: cleaningup
               - activate [3]
                    Start: inactive
                    Goal: activating
               - shutdown [6]
                    Start: inactive
                    Goal: shuttingdown 
          ` 
- If you want to start the vicon2_driver you have to run in other terminal:
          
     `ros2 lifecycle set vicon2_driver_node activate`

- If you want to stop the vicon2_driver you have to run in other terminal:
          
     `ros2 lifecycle set vicon2_driver_node shutdown`

- Is important to do the "source" of the ROS2-Foxy workspace and the Vicon_ws before run one of this commands:
    
     `call local_setup.bat `  (Windows)


# MOCAP4ROS2

This project provides support for ROS2 integration with Vicon cameras (MOCAP systems based on vision) and Technaid TechMCS IMUs (MOCAP systems based on motion sensors).

The project [MOCAP4ROS2](https://rosin-project.eu/ftp/mocap4ros2) is funded as a Focused Technical Project by [ROSIN](http://rosin-project.eu/).


<a href="http://rosin-project.eu">
  <img src="http://rosin-project.eu/wp-content/uploads/rosin_ack_logo_wide.png"
       alt="rosin_logo" height="60" >
</a>

Supported by ROSIN - ROS-Industrial Quality-Assured Robot Software Components.  
More information: <a href="http://rosin-project.eu">rosin-project.eu</a>

<img src="http://rosin-project.eu/wp-content/uploads/rosin_eu_flag.jpg"
     alt="eu_flag" height="45" align="left" >  

This project has received funding from the European Union’s Horizon 2020  
research and innovation programme under grant agreement no. 732287.

***

<p align="center"> 
<img align="center" src="https://github.com/MOCAP4ROS2-Project/mocap4ros2_exp_and_resources/blob/master/resources/mocap4ros_arch.png" 
    alt="mocap4ros_arch" width="100%">
</p>
