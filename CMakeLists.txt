cmake_minimum_required(VERSION 2.8.3)
project(rviz_mesh_display)

## Find catkin and any catkin packages on which
## this package depends at build time
find_package(catkin REQUIRED COMPONENTS roscpp rospy roslib std_msgs shape_msgs geometry_msgs
  # vigir_interactive_marker_server_custom
  rviz pluginlib class_loader
  cv_bridge)

set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

## This plugin includes Qt widgets, so we must include Qt like so:
find_package(Qt5 COMPONENTS Widgets Core REQUIRED)

find_package(OpenGL REQUIRED)

## I prefer the Qt signals and slots to avoid defining "emit", "slots",
## etc because they can conflict with boost signals, so define QT_NO_KEYWORDS here.
add_definitions(-DQT_NO_KEYWORDS)

catkin_package(
  LIBRARIES
    rviz_mesh_display
    ${OPENGL_LIBRARIES}
  INCLUDE_DIRS
    rviz_mesh_display/src
    ${OPENGL_INCLUDE_DIR}
  CATKIN_DEPENDS
    roscpp
    rospy
    roslib
    std_msgs
    shape_msgs
    geometry_msgs
    rviz
    pluginlib
    class_loader
    cv_bridge
)

include_directories(
  rviz_mesh_display/src
	${catkin_INCLUDE_DIRS})

include_directories(SYSTEM
                    ${OPENGL_INCLUDE_DIR}
                    ${QT_INCLUDE_DIR})

link_directories(${catkin_LIBRARY_DIRS})

add_subdirectory(rviz_mesh_display)

install(FILES
  mesh_display_custom_plugin_description.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})

#install(DIRECTORY icons DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
