# tinyxml file
# Note that we use this since urdfdom (ROS) uses this too
# Files come from: http://sourceforge.net/projects/tinyxml/

cmake_minimum_required(VERSION 3.10)
project(tinyxml
		VERSION 0.0.1
		DESCRIPTION "Tinyxml non-ros"
		LANGUAGES CXX)

################################
# Add common source 

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/.")

add_definitions(-DTIXML_USE_STL)

set( tinyxml_srcs src/tinyxml.cpp src/tinyxmlparser.cpp src/tinyxmlerror.cpp src/tinystr.cpp)
set( tinyxml_hdrs include/tinyxml/tinyxml.h include/tinyxml/tinystr.h)

#find_package(catkin REQUIRED COMPONENTS rospy std_msgs)

#catkin_package(
##  INCLUDE_DIRS include
##  LIBRARIES bb_sharp_IR
####  CATKIN_DEPENDS rospy std_msgs
##  DEPENDS system_lib
#)
#
#include_directories(include
#    ${catkin_INCLUDE_DIRS}
#)



################################
# Add targets
set(BUILD_STATIC_LIBS ON CACHE BOOL "Set to ON to build static libraries")
if(BUILD_STATIC_LIBS)
	add_library(tinyxmlstatic STATIC ${tinyxml_srcs} ${tinyxml_hdrs} )
	set_target_properties(tinyxmlstatic PROPERTIES OUTPUT_NAME tinyxml)

	target_include_directories(tinyxmlstatic PUBLIC ./include)
endif(BUILD_STATIC_LIBS)

add_library( tinyxml SHARED ${tinyxml_srcs} ${tinyxml_hdrs} )
set_target_properties( tinyxml tinyxmlstatic PROPERTIES FOLDER ThirdParty/tinyxml )


install( TARGETS tinyxml DESTINATION lib )
install( FILES ${tinyxml_hdrs} DESTINATION include )

#install(PROGRAMS scripts/GP2Y0A21YK0F.py
#  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

