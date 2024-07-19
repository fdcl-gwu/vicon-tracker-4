# Vicon Tracker 4 

## Vicon Tracker 4 tutorials
### Video Links
- [Layout and Controls](https://youtu.be/iXMBGGSAyso?feature=shared)
- [Managing and Tracking Objects](https://youtu.be/Uvf8JNWBt8s?feature=shared)
- [Tracker 4 tutorials Playlist](https://youtube.com/playlist?list=PLxtdgDam3USVlWZdhZdWePKzN6MT7f6gU&feature=shared)
- [Tracker 3 tutorials Playlist](https://youtube.com/playlist?list=PLxtdgDam3USXPrhGA70ix8WT_nZBLK7qB&feature=shared)

### Docs
- [User Guide for Tracker](https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/docs/Vicon%20Tracker%20User%20Guide.pdf)
- [Transition Guide from Tracker 3 to 4](https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/docs/Vicon%20Tracker%204%20Migration%20Guide.pdf)
- [Tracker to ROS 1](https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/docs/Guide%20to%20installing%20and%20running%20ROS-v5.pdf)
    - [Git hub page for ROS 2](https://github.com/OPT4SMART/ros2-vicon-receiver)

## How To - Virtual-Reality Peripheral Network (VRPN)
According to an [official website](https://help.vicon.com/space/Tracker41/14322890/Work+with+VRPN),
_The Virtual-Reality Peripheral Network (VRPN) is a library that provides an interface between 3D immersive applications and tracking systems used for Virtools. Vicon Tracker has a built-in VRPN server that streams data natively into these applications or will enable the development of simple interfaces using VRPN._ 

The object, such as a quadrotor, can retrieve position and attitude data from the Vicon server via [VRPN](https://en.wikipedia.org/wiki/VRPN).
This data typically consists of position and orientation (as a quaternion), which are essential for precise control and navigation, i.e., 

```
vrpn_float64	pos[3];		// Position of the sensor
vrpn_float64	quat[4];	// Orientation of the sensor
```

### Setup Instructions
The FDCL's VRPN libraries in C++ can be found at https://github.com/fdcl-gwu/vrpn, and the minimal working code is available at https://github.com/fdcl-gwu/fdcl-vicon.

To integrate with the Vicon server, follow these setup steps:

(1) Ensure that the Vicon server, the desktop computer running Vicon Tracker 4, and the rover (e.g., Nvidia Jetson) are connected to the same network via a WiFi router.

<img src="https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/figs/wifi_router.jpg" width=100%>

<img src="https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/figs/vicon_server.jpg" width=100%>

(2) Open Vicon Tracker 4 on the desktop computer. Navigate to the `View` menu and click on the `Connections` panel. Select the `Enabled` check box.

<img src="https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/figs/vrpn.png" width=100%>

(3) When creating an object with Vicon Tracker 4, its reference frame is determined when calibrating the VICON cameras with the Vicon Active Wand.
At SEH2200, the first axis points towards the right (22nd Street) when sitting at the base station; the second axis points forward (I Street) when sitting at the base station; the third axis points upward, [more information](https://github.com/fdcl-gwu/fdcl-uav/blob/master/docs/Documentation/Documentation.tex).

<img src="https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/figs/vicon_frame.jpg" width=100%>

### Specifying the IP address for Vicon software
After setting up the Vicon system, it is crucial to specify the IP address to prevent the Vicon Tracker 4 from freezing during flight. Follow these steps:
1. Visit "www.routerlogin.net" (or "192.168.1.1").
2. Navigate to the "LAN Setup" section under the "ADVANCED" tab.
3. Set the router's gateway IP address to match the Vicon system's IP address, such as 192.168.10.254.
4. Configure the static IP addresses for the Vicon system as 192.168.10.1 and 192.168.10.2.
5. Reserve the necessary IP addresses.
<img src="https://github.com/fdcl-gwu/vicon-tracker-4/blob/main/figs/Netgear%20Router%20R7800.png" width=100%>
For your reference,

- [Specifying the IP address for your Vicon software](https://help.vicon.com/space/Connect/1605699/Specifying+the+IP+address+for+your+Vicon+software)
- [Configuring network card settings in Windows 11](https://help.vicon.com/space/Connect/1607823/Configuring+network+card+settings+in+Windows+11)
- [How do I locate my router’s IP address?](https://kb.netgear.com/23664/How-do-I-locate-my-router-s-IP-address)
- [Nighthawk R7800 Router Change IP address](https://community.netgear.com/t5/Nighthawk-Wi-Fi-5-AC-Routers/Nighthawk-R7800-Router-Change-IP-address/td-p/1218266)
- [Netgear Nighthawk R6700 | How To Change WiFi Name & Password](https://www.youtube.com/watch?v=vRHKSulrN38)
