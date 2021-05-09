# This Documentation covers the working of the Action Server node

## Class IotRosBridgeActionServer

class for the action server

	- __init__(self):    # constructor
         
        Constructs the object for the Action Server
        It also Subscribes to the Mqtt topic to constantly
        get orders that are spawned

    -   mqtt_sub_callback(self, client, userdata, message):
         
        This function subscribes to mqtt topic to check for
        incoming orders and then publishes it on a rostopic

    -  on_goal(self, goal_handle):
        
        function generated during receiving of goal
		
		Parameters:
			type goal_handle: list
                     Contains the goal sent in a python list format
        

    -	process_goal(self, goal_handle):
        
        function generated to process goal
		
		Parameters:
				type goal_handle: list
                     Contains the goal sent in a python list format
        


## Main Function 

>	A rospy node is made
>	and an action server class object
>	is constructed.