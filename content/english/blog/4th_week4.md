---
title: "Week 4 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-05-12T13:28:00Z
image: "/images/Blog/4th_week4/Algoritmo_HDL_testes_robo.png"
categories: ["4th Period - Weekly Progress"]
authors: 
    - "João Carranca"
    - "Catarina Caramalho"
    - "João Pinheiro"
tags: ["path planning", "localization"]
draft: false
---

### 2D Path Planning/Guidance

<div style="text-align: justify;">

<!-- During week 4, we started testing with the real robot in a real environment to verify if the results we achieved in simulation could be replicated in the real world. For this, we used two different tests, one for each developed node, similar to the simulation. The first test involved a narrow corridor that would be easy to navigate with the robot's arm in its contained position but impossible to navigate if the arm was fully spread out. The test did not go as expected, since the robot was not able to realize, in the second case, that a collision would take place. The robot moved despite this and had to be stopped before any actual collisions took place. However, we believe this doesn't have to do with the quality or reliability of the code and instead relates to the fact that currently, the local path planner used by the SocRob team is not prepared to receive the footprint as a parameter and assumes it to be static, which means it always assumes it to be a circle. This would justify the robot's behavior. For the height adjustment node, we placed a bag tied to the ceiling at a height that would make it an obstacle depending on the robot's height. We observed that at large distances, the behavior went according to our expectations; however, at short distances, the robot stopped detecting the bag. This was due to limitations of the cameras and sensors used that couldn't properly observe the bag at sharp angles. This problem was corrected; however, some issues remain, with some unintended objects being identified as obstacles at times, affecting the projection of the bag and other results. These issues are, however, not directly related to our task and can be resolved. -->

This week, testing with the real robot in a real environment commenced to assess the replication of simulation results in the physical world. Two distinct tests were conducted, one for each developed node, mirroring the simulation setup.

The first test involved navigating a narrow corridor, a task manageable with the robot's arm in a contained position but impossible with the arm fully extended. Unexpectedly, the robot failed to recognize the collision risk in the latter scenario and continued to move forward. It became evident that the local path planner utilized by the SocRob@Home team was not configured to handle dynamic footprints, as it assumed a static circular shape. This limitation likely influenced the robot's behavior.

For the height adjustment node, a bag was suspended from the ceiling at a height that posed an obstacle depending on the robot's elevation. While the robot performed as expected at longer distances, it struggled to detect the bag at closer ranges due to limitations in the cameras and sensors. Although adjustments were made to correct this issue, occasional detection errors persisted, leading to unintended objects being identified as obstacles and impacting the projection of the bag.

While these challenges are not directly attributable to the code's quality or reliability, they hindered the accurate assessment of the height adjustment node's performance. Nevertheless, efforts to resolve these issues are ongoing, ensuring the continued refinement of the system.
</div>

### 3D Localization

<div style="text-align: justify;">

In week 7 of the 3rd period, the tests carried out on the TIAGo robot did not proceed as expected. 
The possible causes were varied and could be related to the performance of the algorithms in a real environment or to the map itself. 
However, with the new approach adopted for mapping, FAST-LIO, the maps undoubtedly acquired much more detail and points, which proved to be a great advantage for localization. Thus, during this week, the final tests for this task were finally completed.

</div>

<div style="text-align: justify;">

Finnaly this week the robot was fixed and we could finally try HDL algorithm and MCL3D algorithm, therefor obtaining results in a real environment.

</div>

#### HDL Algorithm

<div style="text-align: justify;">
We could run the HDL algorithm without any trouble, showing an outstanding performance as we can see in the figure below, the accuracy of the localization is evident. 

To verify it, as explained in the results obtained in the simulation, it can be noted that the pointcloud captured by the sensor in real-time overlaps with the map, denoting the correct pose of the robot. Initially, it is necessary to manually indicate the pose estimate in rviz; however, this is a common problem in robotics and does not represent a significant drawback. Once the pose has been estimated, the robot localizes itself and remains localized throughout its journey.

</div>

{{< image 
  src="/images/Blog/4th_week4/Algoritmo_HDL_testes_robo_gif.gif" 
  caption="Figure 1 - HDL Algorithm tested in a real robot" 
  alt="alter-text" 
  position="center" 
  command="fill" 
  option="q100" 
  class="img-fluid" 
  title="image title"  
  webp="false" 
>}}

#### MCL3D Algorithm

<div style="text-align: justify;">
When we were testing this algorithm, we were with really low expectations due to the fact that in simulation it didn't wen that well. Eventhough we knew that we wanted to try it anyway and obtain the best results possible with it. 

Unfortunately our expectations would became a reality. Just a few seconds after the initial setup in rviz, the algorithm started to estimate its location in a poor manner, also the map and the data from the pointcloud were not alligned at all, and when the robot rotates, there is significant delocalization, as you can see in the image below:

</div>

{{< image 
  src="/images/Blog/4th_week4/Algoritmo_MCL3D_testes_robo.png" 
  caption="Figure 2 - MCL3D Algorithm tested in real robot" 
  alt="alter-text" 
  position="center" 
  command="fill" 
  option="q100" 
  class="img-fluid" 
  title="image title"  
  webp="false" 
>}}

<div style="text-align: justify;">

As we can see the localization is completely wrong and doesn't match in any way the real testbed in ISR.

</div>

<div style="text-align: justify;">

Another important aspect to take into account is that the *Ground truth* that we considered, was done with optitrack cameras that were scattered around the testbed. This cameras do a triangulation, giving us a better estimate of the position.

It is important to note that within the `.launch` files of the algorithms, various parameters are adjustable:

</div>

```cpp 
//HDL Localization - FALTA VER ESTE
<arg name="use_odom" default="false" /> // The use of Odometry is optional, it's value can be "true" or "false"
<arg name="use_imu" default="false" /> // The use of IMU is optional, it's value can be "true" or "false"

//MCL3D
<arg name="use_odom" default="false" /> // The use of Odometry is optional, it's value can be "true" or "false"
<arg name="use_imu" default="false" /> // The use of IMU is optional, it's value can be "true" or "false"
```
Multiple combinations were tested to calculate the errors and determine the optimal configurations.

Throughout this week, the cameras were calibrated and rosbags were generated. We recorded various datasets as the robot moved with the different combinations of parameters for both algorithms. 

However, the robot's data acquisition rate is higher than the optitrack cameras, which means that it will be necessary to synchronize the data, in order to find the moments when both sources were capturing information, to calculate the errors accurately and generate the necessary plots.

</div>

<div style="text-align: justify;">

##### Next Steps

The next steps in this task involve computing the errors associated with the Optitrack cameras, as mentioned in the proposal documentation and project presentation.
Also in the next week we hope to develop two scripts in python in order to analyze closely the estimation of the localization for both algorithms.
The first script is to match the points from the cameras with the points from the scan and the second to make the estimation of the error.

</div>




