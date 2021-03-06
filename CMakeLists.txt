# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.12)
project(diffdrive_gazebo_plugin)
# Load catkin and all dependencies required for this package

find_package(catkin REQUIRED COMPONENTS gazebo_ros nav_msgs geometry_msgs sensor_msgs)

find_package(Boost REQUIRED COMPONENTS thread)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

find_package(gazebo REQUIRED)

catkin_package(
    DEPENDS Boost
    CATKIN_DEPENDS gazebo_ros nav_msgs geometry_msgs sensor_msgs
    LIBRARIES gazebo_ros_diffdrive_uos
    INCLUDE_DIRS include
)

add_compile_options(${GAZEBO_CXX_FLAGS})

include_directories(${GAZEBO_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS} include)

add_library(gazebo_ros_diffdrive_uos src/gazebo_ros_diffdrive_uos.cpp)
add_dependencies(gazebo_ros_diffdrive_uos ${catkin_EXPORTED_TARGETS})
target_link_libraries(gazebo_ros_diffdrive_uos ${catkin_LIBRARIES} ${Boost_LIBRARIES})

install(TARGETS gazebo_ros_diffdrive_uos LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})

install(DIRECTORY include/${PROJECT_NAME}/ DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
