cmake_minimum_required(VERSION 3.1.0)

project(armcontrol)
project(transform_and_union)

find_package(realsense2 REQUIRED)
find_package(PCL 1.3 REQUIRED)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

add_executable(armcontrol armcontrol.cpp)
add_executable(transform_and_union transform_and_union.cpp)

include_directories(include/dynamixel_sdk)
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
target_link_libraries(armcontrol ${PCL_LIBRARIES} ${realsense2_LIBRARY} -ldxl_x64_cpp -lrt)
target_link_libraries(transform_and_union ${PCL_LIBRARIES})
