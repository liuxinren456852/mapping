cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()
#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries

#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)

rosbuild_add_library(octree_pcl src/pcl_to_octree/octree/OcTreePCL.cpp 
                                       src/pcl_to_octree/octree/OcTreeNodePCL.cpp)

rosbuild_add_executable(pcl_to_octree src/pcl_to_octree/pcl_to_octree.cpp)
target_link_libraries(pcl_to_octree octree_pcl)

rosbuild_add_executable(pointcloud_publisher src/pcl_to_octree/pointcloud_publisher.cpp) 

rosbuild_add_executable(octree_client src/pcl_to_octree/octree_client.cpp)
target_link_libraries(octree_client octree_pcl)

rosbuild_add_executable(pcl_to_octree_vanilla src/pcl_to_octree/pcl_to_octree_vanilla.cpp)
rosbuild_add_executable(octree_client_vanilla src/pcl_to_octree/octree_client_vanilla.cpp)
