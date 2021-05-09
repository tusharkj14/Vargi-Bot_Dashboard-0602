# This Documentation covers the Code related to Shipping the package

## Class IotActionClient
This Class is to use methods related to
Action client for an action server.

    1.  __init__(self):
         
        creates a class for the action client, to
        send goals to the action server. This time
        to publish/append Data from the UR5_2 arm side
        to the google spreadsheet
         

    2.  on_transition(self, goal_handle):
         
        function generated during transition of goal
        
        Parameters
        ------------------
        :type goal_handle: list
        :            Contains the goal to be sent in a python list format
        ------------------
        
        Is called when the send goal method is called
         

    3.  send_goal(self, arg_topic, arg_string):
         
        function to send goal to action server
        Python list and string methods are called
        and a goal is sent to the action server
        
        Parameters
        ------------------
        :type arg_topic: string
        :           the name of the method that selects which spreadsheet to update
        :type arg_sring: string
        :           the message that has to be appended in the google sheet
         

## Class CartesianPath

This class is used for methods related to
the moveit UR5 arm

    1   __init__(self, arg_robot_name):
        
        This constructs an object for UR5 moveit class
        which finds the package on the conveyor belt
        and drops it into the respective bin
        
        Parameters:
            type arg_robot_name: string
                                 it is the UR5 arm which we are trying to use
        


    2   go_to_pose(self, arg_pose):
         
        This function makes the UR5 arm to go to a
        particular pose for which Inverse Kinematics is valid
        
        Parameters:
             type arg_pose: geometry_msgs msg
                            Set of valid coordinates
        


    3   set_joint_angles(self, arg_list_joint_angles):
         
        This function sets the different joints
        of UR5 arm to the given value
        
        Parameters:
                type arg_list_joint_angles: List of angles in Radians
                                            Different Angles ranging from -180 to +180
                                            for each joint angle
        


    4   hard_set_joint_angles(self, arg_list_joint_angles, arg_max_attempts):
         
        This function sets the different joints
        of UR5 arm to the given value.
        It loops through a range until the result is achieved
        
        Parameters:
                type arg_list_joint_angles: List of angles in Radians
                                            Different Angles ranging from -180 to +180
                                            for each joint angle
                type arg_max_attempts: Int value for range
                                       The number of attempts to set the joint angles
         


    5   go_home(self):
        function used to set joint angles to reach the conveyor belt
        Uses the hard set joint angle method


    6   check_count(self, stri):
         
        This function checks the name of the package 
        and find its color using the color list that 2d camera
        sent to this node
        Parameters:
                type stri: string
                       contains the package name for which the bin is checked
        Result :
                i : integer value which indexes to the color of the required package
    

    7   go_to_bin(self, col):
         
        This functions goes to the respective colored bin for each package
        and after detaching it calls the conveyor belt to full power
        After we drop the package, the conveyor belt
        is started again and the ur5 goes to the home position.
        Meanwhile the Shipped Orders sheet is appended with the data
        
        Parameters:
                type col:  string
                       It is a string value which tells us about the colour
                       of the package to drop it into the same colored bin
        


    8   func_cb3(self, data):
        
        This functions is the callback function for
        the '/get_order' rostopic which contains the
        order details of the package recieved
        
        Parameters :
                type data:  string
                        The message received from the rostopic


    9   func_cb2(self, data):
         
        callback function for logical camera 2
        when the package is just under the ee link of ur5_2, it is stopped
        then conveyorbelt is stopped and package is attached
        
        Parameters :
                type data: Logical Camera Message
                       The set of information that is provided by the logical Camera 2
        

## Callback function to get colours of respective Packages

     
    callback function for subscribing to the rostopic to get the sorted colors list
    Parameters
    ------------------
    :type data:  string
    :       The message received from the rostopic
     


## Main Function


> The main function subscribes and collect the
> lists of colors of package from node 1.
> Then is constantly subscribed to the logical camera 2
> to get the pakcage and drop it for shipping the package

