cmake_minimum_required(VERSION 2.8.3)
project(lidar_euclidean_cluster_detect)


# find_package(autoware_build_flags REQUIRED)

find_package(autoware_msgs REQUIRED)
find_package(catkin REQUIRED COMPONENTS
        pcl_ros
        roscpp
        geometry_msgs
        std_msgs
        sensor_msgs
        tf
        grid_map_ros
        grid_map_cv
        grid_map_msgs
        autoware_msgs
        jsk_rviz_plugins
        )

find_package(OpenMP)
find_package(OpenCV REQUIRED)

set(CMAKE_CXX_FLAGS "-O2 -Wall ${CMAKE_CXX_FLAGS}")

catkin_package(
        CATKIN_DEPENDS
        pcl_ros
        roscpp
        geometry_msgs
        std_msgs
        sensor_msgs
        autoware_msgs
        tf
        grid_map_ros
        grid_map_cv
        grid_map_msgs
        jsk_rviz_plugins
        INCLUDE_DIRS include
)

# Resolve system dependency on yaml-cpp, which apparently does not
# provide a CMake find_package() module.
find_package(PkgConfig REQUIRED)
pkg_check_modules(YAML_CPP REQUIRED yaml-cpp)
find_path(YAML_CPP_INCLUDE_DIR NAMES yaml_cpp.h PATHS ${YAML_CPP_INCLUDE_DIRS})
find_library(YAML_CPP_LIBRARY NAMES YAML_CPP PATHS ${YAML_CPP_LIBRARY_DIRS})
link_directories(${YAML_CPP_LIBRARY_DIRS})

include_directories(
        include
        ${catkin_INCLUDE_DIRS}
        ${autoware_msgs_INCLUDE_DIRS}
        ${OpenCV_INCLUDE_DIRS}
)
link_directories(${OpenCV_LIBRARY_DIRS})

#Euclidean Cluster
add_executable(lidar_euclidean_cluster_detect
        nodes/lidar_euclidean_cluster_detect/lidar_euclidean_cluster_detect.cpp
        nodes/lidar_euclidean_cluster_detect/cluster.cpp)


find_package(Eigen3 QUIET)


target_link_libraries(lidar_euclidean_cluster_detect
            ${OpenCV_LIBRARIES}
            ${catkin_LIBRARIES}
            ${YAML_CPP_LIBRARIES})

add_dependencies(lidar_euclidean_cluster_detect
        ${catkin_EXPORTED_TARGETS}
        )
