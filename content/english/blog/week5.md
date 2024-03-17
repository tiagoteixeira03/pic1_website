---
title: "Week 5 - Localization"
meta_title: ""
description: "meta description for week 5 blog post"
date: 2024-03-17T13:28:00Z
image: "/images/Blog/week4/A-LOAM_DATASET.jpeg"
categories: ["Weekly Progress"]
authors:
  - "António Morais"
  - "Catarina Caramalho"
tags: ["localization"]
draft: false
---

#### 3D Localization

##### → AMCL3D
During the first few weeks, the team concentrated on studying the AMCL3D algorithm, as mentioned in week 2. However, there were some setbacks when attempting to test the algorithm. 

It was discovered that the algorithm was not compatible with ROS Noetic and Ubuntu 20.04.2, as it was developed for ROS Kinetic and Ubuntu 16. Furthermore, the GitHub repository lacked a Docker file to get around this issue. As a result, the team had to search for new alternative solutions. 

Nevertheless, changing algorithms had its benefits since AMCL3D was designed for a drone and utilized input data from different technologies than what the team was using, making adaptation more challenging. The new alternatives have optional input data to facilitate the adaptation.

The mistake was starting to study the algorithm before testing it, as it is common to find numerous errors during the compilation of the algorithm, which can impede progress.

##### → New Algorithm Alternatives
<!-- The HDL Localization algorithm uses a 3D LiDAR (Velodyne HDL32). Utilizing Unscented Kalman Filter-based pose estimation, this package incorporates input data from an IMU (Inertial Measurement Unit) to estimate pose. However, the utilization of IMU data remains optional, and the team is currently evaluating whether to incorporate it or not. Despite its promising capabilities, this algorithm does not generate TFs (Transforms). -->
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
        {{< image src="/images/Blog/week5/mcl3d.gif" caption="Figure 2 - Simulation environment (left); Map of the simulation environment obtained with A-LOAM (right)" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
        </div>
    </div>
</div>