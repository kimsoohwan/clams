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

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

rosbuild_add_library(${PROJECT_NAME}
  src/high_res_timer.cpp
  src/lockable.cpp
  )
rosbuild_link_boost(${PROJECT_NAME} thread)
target_link_libraries(${PROJECT_NAME} rt)

rosbuild_add_gtest(test_hrt src/test_hrt.cpp)
rosbuild_add_gtest_build_flags(test_hrt)
target_link_libraries(test_hrt ${PROJECT_NAME})

rosbuild_add_gtest(test_lockable src/test_lockable.cpp)
rosbuild_add_gtest_build_flags(test_lockable)
target_link_libraries(test_lockable ${PROJECT_NAME})

