---
title: "Week 7 (3rd Period) - Test"
meta_title: ""
description: "meta description for week 7 blog post"
date: 2024-03-31T13:28:00Z
image: "/images/Blog/3rd_week7/cover.png"
categories: ["3rd Period - Weekly Progress"]
author: "António Morais"
tags: ["mapping"]
draft: false
---

#### 3D Mapping

##### → LIO-SAM

<div style="text-align: justify;">

During this week, the team delved into testing the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) algorithm, but a problem arose from the need for synchronization of the Inertial Measurement Unit (IMU) and LiDAR. This process involves determining matrices and parameters to synchronize both components so that the algorithm works properly. The synchronization process is explained in detail on the [Github repository of LIO-SAM](https://github.com/TixiaoShan/LIO-SAM), but it can also be understood by viewing the following images provided by the authors.
</div>

{{< image 
  src="/images/Blog/3rd_week7/imu-transform.png" 
  caption="Figure 1 - IMU and LiDAR axis synchronization (TixiaoShan/LIO-SAM: LIO-SAM: Tightly-coupled Lidar Inertial Odometry via Smoothing and Mapping.” Accessed: Apr. 14, 2024.)" 
  alt="alter-text" 
  height="400px" 
  width="850px" 
  position="center" 
  command="fill" 
  option="q100" 
  class="img-fluid" 
  title="image title"  
  webp="false" 
>}}

{{< image 
  src="/images/Blog/3rd_week7/imu-debug.gif" 
  caption="Figure 2 - IMU debug (TixiaoShan/LIO-SAM: LIO-SAM: Tightly-coupled Lidar Inertial Odometry via Smoothing and Mapping.” Accessed: Apr. 14, 2024.)" 
  alt="alter-text" 
  height="300px" 
  width="800px" 
  position="center" 
  command="fill" 
  option="q100" 
  class="img-fluid" 
  title="image title"  
  webp="false" 
>}}

<div style="text-align: justify;">

<!-- In simulation the students had some setbacks as they thought they would need to make changes in it to perform what is ilustrated above. So it was decided to try the algorithm on the TIAGo robot, but another problem was discovered as the IMU that is was initially thought to be of use isnt compatible with the algorithm itself. The SLAM method in discussion needs a 9 degrees of freedom IMU and the one availabe on TIAGo only has 6 degrees of freedom.

Following the problem discovered, the team found a solution and started to work with the [Jackal robot](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) from the Institute of Robotics and Systems (ISR) to test the algorithm. The choice was made because the robot has an IMU with 9 degrees of freedom and even a [Velodyne LiDAR](https://velodynelidar.com/products/puck/) - which is the LiDAR that the author of the algoithm made development with. -->
In simulation, the students encountered some setbacks as they initially believed they would need to make changes to perform the process illustrated above. Consequently, they decided to attempt implementing the algorithm on the TIAGo robot. However, another issue surfaced when it was discovered that the IMU initially considered for use is not compatible with the algorithm itself. The SLAM method under discussion requires a 9 degrees of freedom IMU, whereas the IMU available on the TIAGo only has 6 degrees of freedom.

Following this discovery, the team identified a solution and began working with the [Jackal robot](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) from the Institute For Robotics and Systems (ISR) to test the algorithm. This decision was made because the robot features a 9 degrees of freedom IMU and even a [Velodyne LiDAR](https://velodynelidar.com/products/puck/), which is the LiDAR used by the author of the algorithm during development.
</div>

{{< image 
  src="/images/Blog/3rd_week7/jackal.jpeg" 
  caption="Figure 3 - Jackal robot from ISR" 
  alt="alter-text" 
  height="600px" 
  width="500px" 
  position="center" 
  command="fill" 
  option="q100" 
  class="img-fluid" 
  title="image title"  
  webp="false" 
>}}

<div style="text-align: justify;">

Subsequently, the team attempted to synchronize the components but did not succeed, and did not make much further progress this week.
</div>