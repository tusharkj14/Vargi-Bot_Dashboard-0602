# This Documentation covers the Code related to Dispatching the package

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
        :type arg_list: list
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
         


    5   attach_box(self, box_name,  timeout=4):
        
        This Function attaches a given package to the
        end effector in both Gazebo and Moveit, so that it can
        form a collision free path.
        it also uses the Vaccum gripper Service
        
        Parameters:
                type box_name: string
                    name of the package


    6   detach_box(self, arg_name, timeout=4):
        This Function detaches a given package to the
        end effector in both Gazebo and Moveit
        it also uses the Vaccum gripper Service
        
        Parameters:
                type box_name: string
                    name of the package
    

    7   remove_object(self, arg_name, timeout=4):
        
        This Function removes a package from the planning
        scene in moveit
        
        Parameters:
                type box_name: string
                    name of the package
        


    8   moveit_play_planned_path_from_file(self, arg_file_path, arg_file_name):
        
        This function loads the yaml file containing
        the already travelled path by a UR5 arm between two poses
        
        Parameters:
            type arg_file_path: string
                    The directory where the yaml file is stored
            
            type arg_file_name: string
                    The name of the yaml file to load


    9   moveit_hard_play_planned_path_from_file(self, arg_file_path, arg_file_name, arg_max_attempts):
        
        This function loads the yaml file containing
        the already travelled path by a UR5 arm between two poses
        until true while looping for a given number of attempts
        
        Parameters:
            type arg_file_path: string
                    The directory where the yaml file is stored
            
            type arg_file_name: string
                    The name of the yaml file to load
            
            type arg_max_attempts: Int value for range
                    The number of attempts to set the joint angles

## Class Camera1
class to access 2d camera

     
    1.  get_qr_data(self, arg_image):
        
        This function uses the decode attribute of pyzbar
        then we sort the packages according to the Rect Coordinates
        and save the sorted color list at self.qr
        Parameters:
                type arg_image: Numpy Array
                    An image in the form of a numpy array
        

    2.  callback(self, data):
         
        callback fn called when 2d camera topic is subscribed
        
        Parameters:
                type data: 2d Camera Message
                    Message received using 2d camera


## Sending Order Details
To send order details to the second node

    sendorder(s1, s2, s3):
        
        This function gets the order details bound with
        the package just disptached and publishes
        it on a topic for the 2nd node to access it
        also it waits till any one subscribes to the topic
        
        Parameters:
                type s1: string
                    the order ID of the package
                
                type s2: String
                    City of Order
                
                type s3: String
                    Order Quantity


## Getting Package

    get_pkg(arg_name, arg_list):
         
        This function plays the saved trajectory
        to the package that it gets from select_pkg function
        Then appends the data to the Orders Dispatch sheet
        and deletes the instance of the order details globaly
        
        Parameters:
                type arg_name: string
                    the name of the package
                
                type arg_list: list
                    List containing the order details of the package that has to be sent


## Selecting Package

    select_pkg(arg_list):
         
        This function finds out which
        package to select using their order ID.
        Since each Order ID is unique, we made the Code
        find the package to dispatch using the order ID
        
        2 Threads are made - 
        One to get the required package 
        One to send the order details of that package to node 2
        
        Parameters:
                type arg_list: list
                    List containing the order details of the package that has to be sent


## Callback Function for Incoming Orders

    func_callback(data):
         
        This function gets messages from the "Incoming Orders"
        rostopic and append it to a global list called
        lst_order.
        Appends the data to the Incoming Orders Sheet
        
        Parameters:
                type data: Rostopic Message
                    Data contained in the rostopic message
         


## Sending Package Colours

    sendcolor(lst): 
         
        This function gets the sorted color list for all the package
        and then publish it on a topic for the 2nd node to access it
        also it waits till any one subscribes to the topic
        
        Parameters:
                type arg_list: list
                    List containing the colour names of different packages



## Main Function


> The Main Function-
> Starts the conveyor belt
> Gets the value of different colors of the packages and calls sendorder
> Appends data into the Inventory Sheet
> Constantly Subscribed to the Rostopic to get incoming orders from Action Server

    """
        to make sure that the High priority orders , those with
        order ID starting with 1 is sent first, we are sorting the
        incoming orders list in descending order
        and then select the last element of the list
    """
