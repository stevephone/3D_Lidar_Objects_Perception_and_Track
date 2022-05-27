# 3D_Lidar_Objects_Perception_and_Track
使用3d激光雷达数据进行障碍物的聚类感知和跟踪，主要参照autoware.ai和跟踪算法(https://github.com/k0suke-murakami/object_tracking)

## perception

#### autoware_msg
* 使用autoware定义的msg,主要使用DetectedObjectArray.msg来表达障碍物

#### detected_objects_visualizer
* 这个package主要是做聚类结果的可视化

#### lidar_euclidean_cluster_detect
* 主要的感知聚类算法节点，其订阅和输出的topic信息，见~/your_path/lidar_euclidean_cluster_detect/interface.yaml
