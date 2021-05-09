## What we did to find the solution to Vargi Bot theme objective?

## Step-1
 
 We went through lines and lines of codes related to pyzbar and cv2, which in turn is used by the 2d Camera.
 The same small object near the UR5_1 arm on the left side of the task world. It captures an image, but an image which it interprets in the form of Numpy array. The image itself was not clear enough to identify all 12 packages located on the shelf. So we did some image clearing, removed the noise, changed it to black and white among others. After that we got a clear image of 12 packages. The next step was to decode the qr code located on each of the package. It came out to be another array, but then we found out about the unique values in the rectangle coordinates.
 We then sorted these coordinates in ascending order of x and y coordinates. We had to sort the array thrice, once along x-axis, once along y-axis, and the last just because the x and y values were not too much unique,  so we again sorted in the batch of three.
 Then we finally got the different values of colours for different package.

## Step-2
 After we get the sorted colours according to the packages in the shelf, we send this list to the node-2, 
([using](file:///home/tushar/DocVB/site/node_t5_u1/index.html#sending-package-colours)) which is the ur5_2 arm, where the packages are going to get Shipped.
 Meanwhile both the UR5_1 and UR5_2 arms travels and sets the joint angles facing the conveyor belt and the action-server 
([This](/home/tushar/DocVB/site/rib/index.html)) gets active.

## Step-3
 The next step is sending the sorted colour list to the action server via the action client
([client](file:///home/tushar/DocVB/site/node_t5_u1/index.html#class-iotactionclient)) stating that we want to append the "inventory" sheet. From there it is sent to the iot py node
[Upadte Inventory](file:///home/tushar/DocVB/site/iot/index.html#function-for-updating-inventory-sheet) wherein some math and string functions are used and data is appended.

## Step-4
We Wait till Sim-Time reaches 60 seconds(or one minute), after which the action server starts publishing the incoming orders on a rospy topic specified.
The UR5_1 node collects this order and appends it on a global list in the python node.
([This fnx](file:///home/tushar/DocVB/site/node_t5_u1/index.html#callback-function-for-incoming-orders)).
The values are aslo pushed to incomming orders sheet

## Step-5
We now get the package using the last element of the global lists of order inside the python node.
If the list has more than 1 element, then it is sorted on the basis of the order id
Since we saw that the order id is unique and starts with '1' for High Priority, '2' for Medium and '3' for Low Priority package.
So Sorting the Order IDs in descending order seemed more viable.
We found out which package to chose using the same Order ID.
If it ends with 1, then it is in the first row. If 2, then second row and so on.......
Meanwhile the order details of the package about to get dispatched is published on the rostopic.
([Orders](file:///home/tushar/DocVB/site/msg/index.html#msgordermsg))

## Step-6
Now our UR5_1 arm starts from its conveyor belt position for the package using the already saved trajectories in our config folder.
([Config Folder](file:///home/tushar/DocVB/site/cnfg/index.html#saved-trajectories)). Attaches the package using the method defined in Class ur5moveit
and travels back along the path already saved to the conveyor belt.

## Step-7
The attached package is dropped at the conveyor belt and its subsequent details are pushed to the action server to update the Dispatched Orders Sheet
and the package goes to the ur5_2 arm using conveyor belt.

## Step-8
The second Node 
([ur5_2](file:///home/tushar/DocVB/site/node_t5_u2/index.html#main-function)) which is constantly subscribed to the logical camera 2 messages checks for an upcoming package. When the package is just under the camera and also the UR5_2 arm, its y coordinate reaches 0 w.r.t. the logical camera 2.
Then the conveyor belt is stopped and the UR5_2 attaches the package
It checks for the colour of the package_XX using some math and the "XX" in the sorted color list it got from node 1 defined in the Cartesian Path class.
The UR5_2 travels to the respective colored bin and drops the package. The OrdersShipped Sheet is appended using the action server and class

**The Above Step-5 to Step-8 are followed when different orders are recieved on different intervals of time**

Our implementation works for all the packages and orders we recieved on our End.
Thank you for reading the Documentation page.
I have been very careful in dding all the links wherever it is needed.

We Worked hard for the last few weeks to get this implementation working
		
		Regards,
		Tushar Kanti Jaiswal
		Team VB#0602

