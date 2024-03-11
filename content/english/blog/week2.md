---
title: "Week 2 - 3D Mapping"
meta_title: ""
description: "meta description for week 2 blog post"
date: 2024-02-25T13:28:00Z
image: "/images/Blog/week2/LIO-SAM_DATASET.jpg"
categories: ["Weekly Progress"]
author: "António Morais"
tags: ["updates", "mapping"]
draft: false
---

#### Mapping

##### → A-LOAM

<!-- Regarding the Mapping module, the team planned to implement the SLAM algorithm [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) and test it in simulation. At first there were a few set backs, the requirements of the algorithm itself: -->
In the context of the Mapping module, our team's objective was to deploy the [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) algorithm, and subject it to comprehensive testing in a simulated environment. However, our initial endeavors were met with challenges primarily stemming from the specific requirements inherent to the algorithm:

- [Ubuntu 18.04](https://ubuntu.com/18-04).
- ROS [Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu) or [Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu).

<!-- This was a set back because the team works with [Ubuntu 20.04](https://releases.ubuntu.com/focal/) and [ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu). For that reason António Morais has the same setup on his personal computer and had to find a solution. Fortunatly the authors of the algorithm also provide [Docker](https://docs.docker.com/get-started/overview/) support which is a very handy tool for cases like this. -->
The encountered setback arose from the team's reliance on [Ubuntu 20.04](https://releases.ubuntu.com/focal/) and [ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu) environments. Consequently, António Morais, operating under the same system configuration on his personal computer, was compelled to think of a solution.

##### → LIO-SAM

Keeping this in mind the team chose to explore (although not planned to do so) the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) algorithm while thinking of a solution for the A-LOAM algorithm. 

Notably, we encountered existing GitHub issues ([#206](https://github.com/TixiaoShan/LIO-SAM/issues/206))addressing compilation challenges specific to ROS Noetic, facilitating our implementation efforts. We then successfully conducted testing using one of the datasets (`walking_dataset.bag`) provided by the authors. 

{{< image src="/images/Blog/week2/LIO-SAM_DATASET.jpg" caption="Figure 1 - Map obtained utilizing LIO-SAM alongside one of the datasets provided by the authors" alt="alter-text" height="300px" width="500px" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}
