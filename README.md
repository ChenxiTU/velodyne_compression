## Requirement
ROS,PCL,OpenCV

## Description
Point cloud compression module usded for Autoware:

https://github.com/CPFL/Autoware/tree/master/ros/src/sensing/drivers/lidar/packages/velodyne

The compression/decompression are real-time and almost lossless(intensity are lossless while x,y,z may have a small error/bias which less than 1 cm)

## Purpose
Compressing/decompressing the data in /velodyne_packets topic(which is the raw data of velodyne Lidar sensor and can be converted into point cloud after calibration)
Support data from HDL64E,HDL64ES2,HDL64ES3,HDL32E and VLP_16 sensor.

## Theory
https://www.researchgate.net/publication/312248026_Compressing_continuous_point_cloud_data_using_image_compression_methods
Not 100% same, but similar idea.

## Steps to Test or Reproduce

Compression:
 Start compression node
`rosrun compression compress2png`
Then play your file which should have /velodyne_packets topic:
`rosbag play yourfile.bag`
Compression node will compress packet data into a new topic /velodyne_packets_compressed
You can use 
`rosbag record /velodyne_packets_compressed`
to get the compressed data.

Decompression:
Start decompression node
`rosrun compression recon2packet`
Then play the compressed data which should have /CompressedPacket topic:
`rosbag play compresseddata.bag`
Then a reconstructed  /velodyne_packets will be built 

