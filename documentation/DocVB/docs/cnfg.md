# This Documentation covers the contents of config folder in pkg_ros_iot_bridge and pkg_task5

## config_pyiot.yaml

`directory - pkg_ros_iot_bridge/config`

*****	This is a .yaml file that comprises the different IoT gateways sign up details

	config_pyiot:
  		
		mqtt:
		    server_url: "broker.mqttdashboard.com"    
		    server_port: 1883
		    topic_sub: "/eyrc/vb/giLGamsh/orders"  
		    topic_pub: "eyrc/giLGamsh/ros_to_iot" 
		    qos: 0


## rviz

`directory - pkg_task5/config`

	The 2 Moveit Planning Scenes
	One for Ur5_1 :	shelf.scene
	One for Ur5_2 : bins.scene


## Saved Trajectories

`directory - pkg_task5/config`

	The .yaml file  that contains the already computed collision-free path
	for a ur5 arm to travel between two poses

	package_xx: It is the saved trajectory between the conveyor belt position of Ur5 arm and the respective package
	package_xx_to_cb: It is the saved trajectory between the the respective package and conveyor belt position of Ur5 arm 

	

