# Ros2fordumb
my personal nots while learning ros2
enjoy
# Chapter 1
when you want to check if you have already a specific package: ros2 pkg executables <name of the package>\\

when you want to run a executable file from your package: ros2 run <package name> <file name>\\

To list somethings:
-ros2 node list
  
-ros2 topic list\\
  
-ros2 service list\\
  
-ros2 action list\\

rqt-wtf...learn how to use it later (i mean its preaty good when i want to call a service with some params)

REEEEEMAPING
  
 -allows you to reassign default node properties, like node name, topic names, service names, etc., to custom values.

ros2 run turtlesim turtle_teleop_key --ros-args --remap <name/namespace of one robot>/<his topic>:=<second robot>/<same topic>

ex.: ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel

ex.:ros2 run turtlesim turtlesim_node --ros-args --remap __node:=my_turtle

 if you want more info abot the node you chan type ros2 node info /node_name
  
  if you want to know how your nodes and topics are connected you can use rqt_graph
  
To see the data being published on a topic, use:

-ros2 topic echo <topic_name>
  
 to list our topics with messages type we can use:
  
  ros2 topic list -t
  
  to check structure of message we can use:
  
  ros2 interface show <message>
  
ex.:ros2 interface show geometry_msgs/msg/Twist

  
Now that you have the message structure, you can publish data onto a topic directly from the command line using:

ros2 topic pub <topic_name> <msg_type> '<args>'

The '<args>' argument is the actual data you’ll pass to the topic, in the structure you just discovered in the previous section.

It’s important to note that this argument needs to be input in YAML syntax. Input the full command like so:
  ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
  
  --once is an optional argument meaning “publish one message then exit”.
  
  ros2 topic pub --rate 1 /turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"
  
  The difference here is the removal of the --once option and the addition of the --rate 1 option, which tells ros2 topic pub to publish the command in a steady stream at 1 Hz.
  
  or one last introspection on this process, you can view the rate at which data is published using:

ros2 topic hz /turtle1/pose

It will return data on the rate at which the /turtlesim node is publishing data to the pose topic.

# Chapter 2

Ros services:
to list all services with thier messages type:

-ros2 service list -t

if you want to check the type of specyfic service:

-ros2 service type <service_name>

If you want to find all the services of a specific type, you can use the command:

ros2 service find <type_name>


For example, you can find all the Empty typed services like this:

ros2 service find std_srvs/srv/Empty


if you want to know the stractur of message type:

ros2 interface show <message_type>

ex for empty

ros2 interface show std_srvs/srv/Empty

----------


above ----- are request and below are responds


ex


o see the arguments in a /spawn call-and-request, run the command:

ros2 interface show turtlesim/srv/Spawn

Which will return:

float32 x

float32 y

float32 theta

string name # Optional.  A unique name will be created and returned if this is empty
---
string name


The information above the --- line tells us the arguments needed to call /spawn. x, y and theta determine the location of the spawned turtle, and name is clearly optional.


you can call a service using:

ros2 service call <service_name> <service_type> <arguments>

The <arguments> part is optional. For example, you know that Empty typed services don’t have any arguments:

ros2 service call /clear std_srvs/srv/Empty
  
# PARAMS
  
  every node has its own params, we can list them using ros2 param list
  
  params are specific settings for a node
  
  to check a param we can use a getter:
  
  ros2 param get <node> <param>
  
  ex.: ros2 param get /turtlesim background_g
  
To change a parameter’s value at runtime, use the command:

ros2 param set <node_name> <parameter_name> <value>
  
  ex: ros2 param set /turtlesim background_r 150

  !!ATENTION!! 
  setting parameters with the set command will only change them in your current session, not permanently. However, you can save your settings and reload them the next time you start a node.

  SAVING PARAMS TO FILE
You can “dump” all of a node’s current parameter values into a file to save them for later by using the command:

ros2 param dump <node_name>

To save your current configuration of /turtlesim’s parameters, enter the command:

ros2 param dump /turtlesim

Your terminal will return the message:

Saving to:  ./turtlesim.yaml

LOADING PARAMS FROM FILE
 You can load parameters from a file to a currently running node using the command:

ros2 param load <node_name> <parameter_file>

To load the ./turtlesim.yaml file generated with ros2 param dump into /turtlesim node’s parameters, enter the command:

ros2 param load /turtlesim ./turtlesim.yaml


