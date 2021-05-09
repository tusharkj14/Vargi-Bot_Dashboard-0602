# This Documentation covers the different message files contained in pkg_ros_iot_bridge and pkg_task5

## msgMqttSub.msg

`directory - pkg_ros_iot_bridge/msg`

	time timestamp
	string topic
	string message																																		 

>This is the .msg file message that stores the data/message received at the mqtt topic

## msgOrder.msg

`directory - pkg_task5/msg`

	string order_id																																	 

>This is the .msg file message that stores the order details of a package that is going to be dispatched

## msgColor.msg

`directory - pkg_task5/msg`

	string color																																 

>This is the .msg file message that stores the color of each package as received using 2d camera
