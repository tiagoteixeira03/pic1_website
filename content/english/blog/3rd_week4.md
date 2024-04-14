---
title: "Week 4 (3rd Period) - Website Development and 3D Mapping"
meta_title: ""
description: "meta description for week 4 blog post"
date: 2024-03-10T13:28:00Z
image: "/images/Blog/3rd_week4/A-LOAM_DATASET.jpeg"
categories: ["3rd Period - Weekly Progress"]
author: "António Morais"
tags: ["website", "mapping"]
draft: false
---

#### Website development
<div style="text-align: justify;">

During the first week since the start of the 2<sup>nd</sup> semester and along with it, the ElectroCap Challenge, the team focused on launching the current website this is written on. As of now, it is still a very early version of the website and we already have feedback to start changing how it looks and it's contents.
</div>

#### Mapping

##### → A-LOAM

<!-- Regarding the Mapping module, the team planned to implement the SLAM algorithm [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) and test it in simulation. At first there were a few set backs, the requirements of the algorithm itself: -->
<!-- In the context of the Mapping module, our team's objective was to deploy the [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) algorithm, and subject it to comprehensive testing in a simulated environment. However, our initial endeavors were met with challenges primarily stemming from the specific requirements inherent to the algorithm: -->

<!-- - [Ubuntu 18.04](https://ubuntu.com/18-04).
- ROS [Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu) or [Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu). -->

<!-- This was a set back because the team works with [Ubuntu 20.04](https://releases.ubuntu.com/focal/) and [ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu). For that reason António Morais has the same setup on his personal computer and had to find a solution. Fortunatly the authors of the algorithm also provide [Docker](https://docs.docker.com/get-started/overview/) support which is a very handy tool for cases like this. -->
<!-- The encountered setback arose from the team's reliance on [Ubuntu 20.04](https://releases.ubuntu.com/focal/) and [ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu) environments. Consequently, António Morais, operating under the same system configuration on his personal computer, was compelled to seek a resolution. Fortunately, the algorithm's developers had foreseen such scenarios and offered [Docker](https://docs.docker.com/get-started/overview/) support, proving to be an invaluable asset in circumventing compatibility challenges. -->

<!-- António Morais proceeded to learn the basics of Docker and tried to run the algorithm with a dataset (provided by the authors) after exporting the roscore from Docker to his local machine but on [Rviz](http://wiki.ros.org/rviz) it wasn't showing the data gathered from the environment. The problem ocurring was that on the code of the algorithm, there were lines regarding `.frame_id`'s that had to be changed due to differences between the ROS's versions at stake: -->
<!-- António Morais subsequently undertook the task of familiarizing himself with Docker's fundamentals. He then endeavored to execute the algorithm using a dataset provided by the authors. Despite successfully exporting the roscore from Docker to his local machine, an unforeseen issue arose during visualization in [Rviz](http://wiki.ros.org/rviz), where the gathered environmental data failed to display.  -->
<div style="text-align: justify;">

Thinking about Week 3 problems encountered the team studied more in depth the algorithm and found that the anomaly stemmed from discrepancies in the algorithm's code, particularly in the handling of `.frame_id` parameters, necessitating adjustments to accommodate variations across different versions of ROS.
</div>

```cpp 
// As an example
laserOdometry.header.frame_id = "/camera_init"; // ROS Melodic or Kinetic
laserOdometry.header.frame_id = "camera_init"; // ROS Noetic
```

<!-- With this changed across the code it was possible to run the algorithm with the dataset (`nsh_indoor_outdoor.bag`) obtaining the following 3D map: -->
<div style="text-align: justify;">

With these modifications implemented throughout the codebase, the algorithm successfully processed the dataset (`nsh_indoor_outdoor.bag`), culminating in the generation of the subsequent 3D map:
</div>

{{< image 
    src="/images/Blog/3rd_week4/A-LOAM_DATASET.jpeg" 
    caption="Figure 1 - Map obtained utilizing the A-LOAM algorithm alongside one of the datasets provided by the authors" 
    alt="alter-text" 
    height="300px" 
    width="500px" 
    position="center" 
    command="fill" 
    option="q100" 
    class="img-fluid" 
    title="image title"  
    webp="false" 
>}}

<!-- After this the team aimed towards running the algorithm with the TIAGo's simulation developed by SocRob@Home. For this to happen it was only needed to give the data gathered by the Ouster LiDAR in simulation as input to the algorithm, so give the topic where the data of the Ouster is being published: -->
<div style="text-align: justify;">

Subsequently, the team directed its efforts towards executing the algorithm within the TIAGo's simulation environment developed by SocRob@Home. Easing this transition merely required supplying the algorithm with the data acquired by the Ouster LiDAR in simulation. To accomplish this, we identified the [topic](http://wiki.ros.org/rostopic) where the Ouster data is published:
</div>

```cpp 
// File path: A-LOAM/src/scanRegistration.cpp
ros::Subscriber subLaserCloud = nh.subscribe<sensor_msgs::PointCloud2>("/velodyne_points", 100, laserCloudHandler); // No changes
ros::Subscriber subLaserCloud = nh.subscribe<sensor_msgs::PointCloud2>("/ouster/points", 100, laserCloudHandler); // With changes
```
<div style="text-align: justify;">

Following these adjustments, we successfully generated a map of the simulation environment:
</div>

{{< image 
    src="/images/Blog/3rd_week4/A-LOAM_Simulation.jpeg" 
    caption="Figure 2 - Simulation environment (left); Map of the simulation environment obtained with A-LOAM (right)" 
    alt="alter-text" 
    height="" 
    width="" 
    position="center" 
    command="fill" 
    option="q100" 
    class="img-fluid" 
    title="image title"  
    webp="false" 
>}}

<!-- The team also managed to dive into the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) algorithm and got to test it with one of the datasets (`walking_dataset.bag`) provided by the authors as there were already Github issues on the repository solving  the problems of compilation for ROS Noetic. -->
<!-- The team further delved into exploring the LIO-SAM algorithm, and conducted testing using one of the datasets (walking_dataset.bag) provided by the authors. Notably, we encountered existing GitHub issues addressing compilation challenges specific to ROS Noetic, facilitating our implementation efforts.

{{< image src="/images/Blog/week2/LIO-SAM_DATASET.jpeg" caption="Figure 1 - Map obtained utilizing LIO-SAM alongside one of the datasets provided by the authors" alt="alter-text" height="300px" width="500px" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}} -->

