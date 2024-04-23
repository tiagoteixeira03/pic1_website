---
title: "Week 5 (3rd Period)"
meta_title: ""
description: "meta description for week 5 blog post"
date: 2024-03-17T13:28:00Z
image: "/images/Blog/3rd_week5/cover.png"
categories: ["3rd Period - Weekly Progress"]
authors:
  - "António Morais"
  - "Catarina Caramalho"
  - "Tiago Teixeira"
tags: ["localization", "mapping", "path planning"]
draft: false
---
#### 3D Mapping

##### → A-LOAM

<div style="text-align: justify;">

<!-- This week the team gathered real data from the robot's Ouster LiDAR to then test [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) with it. To do so the team wrote a launch file (on a personal laptop) that saves what is being published on the rostopic `/ouster/points` (where the real data from the Ouster gets published). After ensuring it was working with the simulation we transfered the file to the real robot and started to gather data with it: -->
This week, the team collected real data from the robot's Ouster LiDAR to conduct testing with [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM). To achieve this, a launch file was created on a personal laptop to record data published on the rostopic `/ouster/points`, where the data from the Ouster LiDAR is published. After confirming its functionality with the simulation, the file was transferred to the real robot, and data collection commenced.
</div>

{{< image 
  src="/images/Blog/3rd_week5/teleop.gif" 
  caption="Figure 1 - Teleoperating the real robot to gather real data" 
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

<div style="text-align: justify;">

<!-- After building a dataset with real data, the team proceded to test A-LOAM with it. Following is presented the obtained map: -->
After assembling a dataset with real data, the team proceeded to test A-LOAM with it. Below is the map obtained from the testing:
</div>

<div class="image-slider-container">
    <div class="slider-wrapper">
        {{< slider 
            dir="images/aloam-gallery-bad" 
            class="max-w-[600px] ml-auto mr-auto" 
            height="400" 
            width="400" 
            webp="true" 
            command="Fit" 
            option="" 
            zoomable="true" 
        >}}
    </div>
    <p class="caption" style="color: #7f7f7f; font-size: 14px;">Figure 2 - Map of the laboratory of systems and robotics (where the testbed is located), using A-LOAM with real data aquired from the robot's Ouster</p>
</div>

<div style="text-align: justify;">

<!-- As one can see the result does not look promissing but it was not the algorithm's fault. Later we figured it was due to the fact that we teleoperated the robot too fast and because of that the data aquired doesn't even make sense. -->
As one can observe, the result does not appear promising. However, this outcome was not attributed to the algorithm's performance. Subsequently, we determined that the issue stemmed from teleoperating the robot at excessive speeds, resulting in nonsensical data acquisition.

<!-- To improve the dataset quality the team repeated the process a few more times. But instead of trying to get a rosbag of the whole laboratory, the team started to gather firstly one of the testbed: -->
To enhance the quality of the dataset, the team repeated the process several times. However, rather than attempting to capture a rosbag of the entire laboratory, the team initially focused on gathering data from the testbed.
</div>

<div class="image-slider-container">
    <div class="slider-wrapper">
        {{< slider 
            dir="images/aloam-gallery-testbed" 
            class="max-w-[600px] ml-auto mr-auto" 
            height="400" 
            width="400" 
            webp="true" 
            command="Fit" 
            option="" 
            zoomable="true" 
        >}}
    </div>
    <p class="caption" style="color: #7f7f7f; font-size: 14px;">Figure 3 - Map of the testbed using A-LOAM with real data aquired from the robot's Ouster</p>
</div>

<div style="text-align: justify;">

<!-- One can see that the result is much more conclusive as it now looks like the testbed itself, but it still detects some non whishible points (it is possible to see some kind of reflection of the testbed due to the reflection of light caused by the windows - this happens because of the LiDAR technology). -->
As evident, the result is considerably more conclusive as it now closely resembles the testbed itself. However, some non-desirable points are still detected, notably the reflection of the testbed caused by light reflecting off the windows — a common occurrence with LiDAR technology.

<!-- Subsequently the team made a rosbag of the whole laboratory and now getting a good result besides a disturbance caused by a dynamic obstacle (a person walking) as we may see in the upcoming images: -->
Subsequently, the team created a rosbag of the entire laboratory and achieved a satisfactory result, despite a disturbance caused by a dynamic obstacle (a person walking), as depicted in the forthcoming images:
</div>

<div class="image-slider-container">
    <div class="slider-wrapper">
        {{< slider 
            dir="images/aloam-gallery-good" 
            class="max-w-[600px] ml-auto mr-auto" 
            height="400" 
            width="400" 
            webp="true" 
            command="Fit" 
            option="" 
            zoomable="true" 
        >}}
    </div>
    <p class="caption" style="color: #7f7f7f; font-size: 14px;">Figure 4 - Map of the laboratory of systems and robotics (where the testbed is located), using A-LOAM with real data aquired from the robot's Ouster</p>
</div>

<div style="text-align: justify;">

<!-- Note that the red points that seem that they are representing some kind of lower floor are also due to light reflections on the floor due to the varnished floor. -->
Note that the red points, which appear to represent a lower floor, are also a result of light reflections on the varnished floor

<!-- Aditionally, the team converted the simulation map obtained in Week 4 to a `.pcd` file with the [pcl_ros](http://wiki.ros.org/pcl_ros) package, which will be of use for the Localization team. -->
Additionally, the team utilized the [pcl_ros](http://wiki.ros.org/pcl_ros) package to convert the simulation map obtained in Week 4 into a `.pcd` file, which will be of use for the Localization team.

<!-- With this in mind we can consider A-LOAM ready and we may focus primarly on LIO-SAM going forward. Eventually it will be interesting to make a rosbag with no dynamic disturbances and noise caused by light reflections. -->
With this in mind, we can consider A-LOAM ready, and our primary focus moving forward will be on [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM). Eventually, it will be advantageous to create a rosbag without dynamic disturbances and noise caused by light reflections and use it with A-LOAM.
</div>

#### 3D Localization

##### → AMCL3D
<div style="text-align: justify;">

During the first few weeks, the team concentrated on studying the [AMCL3D](https://github.com/catec/amcl3d) algorithm, as mentioned in Week 2. However, there were some setbacks when attempting to test the algorithm. 

It was discovered that the algorithm was not compatible with [ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu) and [Ubuntu 20.04](https://releases.ubuntu.com/focal/), as it was developed for ROS [Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu) and [Ubuntu 16.04](https://ubuntu.com/16-04). Furthermore, the GitHub repository lacked a [Docker](https://docs.docker.com/get-started/overview/) file to get around this issue. As a result, the team had to search for new alternative solutions. 

Nevertheless, changing algorithms had its benefits since AMCL3D was designed for a drone and utilized input data from different technologies than what the team was using, making adaptation more challenging. The new alternatives have optional input data to facilitate the adaptation.

The mistake was starting to study the algorithm before testing it, as it is common to find numerous errors during the compilation of the algorithm, which can impede progress.
</div>

##### → New Algorithm Alternatives
<!-- The HDL Localization algorithm uses a 3D LiDAR (Velodyne HDL32). Utilizing Unscented Kalman Filter-based pose estimation, this package incorporates input data from an IMU (Inertial Measurement Unit) to estimate pose. However, the utilization of IMU data remains optional, and the team is currently evaluating whether to incorporate it or not. Despite its promising capabilities, this algorithm does not generate TFs (Transforms).
- <a style="color: white;" href="https://github.com/koide3/hdl_localization?tab=readme-ov-file">HDL Localization</a>
<div style="display: flex; align-items: flex-start;">
    <div style="flex: 1; color: #b4afb7; margin-top: 3%; margin-right:8%; text-align: justify;">
       The HDL Localization algorithm uses a 3D LiDAR (Velodyne HDL32). Utilizing Unscented Kalman Filter-based pose estimation, this package incorporates input data from an IMU (Inertial Measurement Unit) to estimate pose. However, the utilization of IMU data remains optional, and the team is currently evaluating whether to incorporate it or not. Despite its promising capabilities, this algorithm does not generate TFs (Transforms).
    </div>
    <div style="flex: 1;">
        <div style="width: 80%;">
        {{< image src="/images/Blog/week5/mcl3d.gif" caption="Figure 2 - Simulation environment (left); Map of the simulation environment obtained with A-LOAM (right)" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
        </div>
    </div>
</div>

- <a style="color: white;" href="https://github.com/NaokiAkai/mcl3d_ros/tree/main">MCL3D</a>
<div style="display: flex; align-items: flex-start;">
    <div style="flex: 1; color: #b4afb7; margin-top: 3%; margin-right:8%; text-align: justify;">
        MCL3D is based on a fusion approach that combines <a href="https://www.mathworks.com/help/nav/ug/monte-carlo-localization-algorithm.html#:~:text=Product%20Updates-,Monte%20Carlo%20Localization%20Algorithm,-Overview">Monte Carlo localization</a> (MCL) and <a href="https://bluebotics.com/differences-natural-navigation-scan-feature/#:~:text=by%20ANT).-,HOW%20SCAN%20MATCHING%20WORKS,-With%20scan%20matching">scan matching</a> (SM) through <a href="https://builtin.com/articles/importance-sampling#:~:text=IMPORTANCE%20SAMPLING%20DEFINITION">importance sampling</a>. This fusion method seamlessly integrates the strengths of MCL and SM while mitigating their limitations, offering a comprehensive solution for 3D localization tasks. Notably, this fusion method achieves accurate results with fewer particles, leading to computational efficiency without sacrificing accuracy. 
    </div>
    <div style="flex: 1;">
        <div style="width: 80%;">
        {{< image src="/images/Blog/week5/mcl3d.gif" caption="Figure 3 - Simulation environment (left); Map of the simulation environment obtained with A-LOAM (right)" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
        </div>
    </div>
</div> -->
###### HDL Localization

<div style="text-align: justify;">

The [HDL Localization](https://github.com/koide3/hdl_localization) algorithm uses a 3D LiDAR (Velodyne HDL32). Utilizing Unscented Kalman Filter-based pose estimation, this package incorporates input data from an IMU (Inertial Measurement Unit) to estimate pose. However, the utilization of IMU data remains optional, and the team is currently evaluating whether to incorporate it or not. Despite its promising capabilities, this algorithm does not generate TFs (Transforms).
</div>

{{< image 
    src="/images/Blog/3rd_week5/hdl.gif" 
    caption="Figure 5 - HDL Localization tested with a dataset as input" 
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

###### MCL3D

<div style="text-align: justify;">

[MCL3D](https://github.com/NaokiAkai/mcl3d_ros) is based on a fusion approach that combines [Monte Carlo localitazion](https://www.mathworks.com/help/nav/ug/monte-carlo-localization-algorithm.html) (MCL) and [scan matching](https://bluebotics.com/differences-natural-navigation-scan-feature/#:~:text=by%20ANT) (SM) through [importance sampling](https://builtin.com/articles/importance-sampling). This fusion method seamlessly integrates the strengths of MCL and SM while mitigating their limitations, offering a comprehensive solution for 3D localization tasks. Notably, this fusion method achieves accurate results with fewer particles, leading to computational efficiency without sacrificing accuracy. 
</div>

{{< image 
    src="/images/Blog/3rd_week5/mcl3d.gif" 
    caption="Figure 6 - MCL3D alongside one of the datasets provided by the authors" 
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

#### 2D Path Planning 
<div style="text-align: justify;">

In the fifth week, the team made significant progress in leveraging the point cloud generated by the Ouster for local and global path planning within the simulation environment.

To accomplish this, we made modifications to certain launch files, which were previously utilized to transmit the point cloud from the RGBD camera on the robot's torso to the pointcloud_to_laserscan node. Given that we already had a ROS topic in the simulation where the Ouster points were being published, our task primarily involved developing the code necessary to relay these points to the node mentioned previously.

As shown in Figure 8, the robot is now capable of detecting the obstacles in its surroundings using the information provided by the Ouster.
</div>

<div class="image-container">
    <div class="image">
        {{< image 
            src="/images/Blog/3rd_week5/simulation_environment.png" 
            caption="Figure 7 - Simulation Environment" 
            alt="HDL Localization" 
            height="" 
            width="" 
            position="center" 
            command="fill" 
            option="q100" 
            class="img-fluid" 
            title="HDL Localization"  
            webp="false" 
        >}}
    </div>
    <div class="image">
        {{< image 
            src="/images/Blog/3rd_week5/ouster_laserscan.png" 
            caption="Figure 8 - Ouster Points (Red) and Laserscan (Pink)" 
            alt="MCL3D" 
            height="" 
            width="" 
            position="center" 
            command="fill" 
            option="q100" 
            class="img-fluid" 
            title="MCL3D"  
            webp="false" 
        >}}
    </div>
</div>

<div style="text-align: justify;">

However, the current configuration of the node assumes a fixed maximum height for obtaining points, which doesn't account for potential changes in the robot's height. To address this limitation, we need to modify the node's code to enable dynamic adaptation to variations in the robot's height. Consequently, we obtained the source code for the node from GitHub, and moving forward, we will need to manually compile it.

For the upcoming week, our objective is to successfully implement the necessary adjustment to the node.
</div>
