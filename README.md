# Ros2fordumb
my personal nots while learning ros2
enjoy
# Chapter 1
when you want to check if you have already a specific package: ros2 pkg executables <name of the package>\\

when you want to run a executable file from your package: ros2 run <package name> <file name>\\

To list somethings:
-ros2 node list\\
-ros2 topic list\\
-ros2 service list\\
-ros2 action list\\

rqt-wtf...learn how to use it later (i mean its preaty good when i want to call a service with some params)

REEEEEMAPING

ros2 run turtlesim turtle_teleop_key --ros-args --remap <name/namespace of one robot>/<his topic>:=<second robot>/<same topic>

ex.: ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel


