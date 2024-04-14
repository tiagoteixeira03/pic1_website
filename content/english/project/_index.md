---
title: "Project"
meta_title: ""
description: "this is meta description"
---

<div style="text-align: justify;">

To better describe the project let's start with the Problem Definition:
</div>
<br>

#### **Install a 3D LiDAR to detect objects in 3 Dimensions to improve 2D Navigation of an autonomous domestic mobile robot.**

<br>
<!-- Install a 3D LiDAR to detect objects in 3 Dimensions to improve 2D Navigation of an autonomous domestic mobile robot. -->
<div style="text-align: justify;">

<!-- The project involves developing a navigation system for domestic robots (students will be using a TIAGo robot) that may help elderly people or individuals with disabilities or illnesses, using 3D sensors instead of traditional 2D ones. While 2D sensors may have limitations, such as not capturing the z coordinate, 3D sensors, like the Ouster OS1 LiDAR, overcome these limitations, enabling more precise and safe indoor navigation. -->
The project involves developing a navigation system for domestic robots (students used a TIAGo robot) using 3D sensors instead of traditional 2D ones. While 2D sensors may have limitations, such as not capturing the z coordinate, 3D sensors, like the Ouster OS1 LiDAR, overcome these limitations, enabling more precise and safe indoor navigation.

Those who might benefit from our project include robot manufacturers seeking to implement this solution/technology. Specifically, other robots encountering similar challenges as those to be further described. Additionally, elderly individuals or those with disabilities or illnesses stand to benefit from the robot's focus on a domestic environment.
</div>

<div style="display: flex; align-items: flex-start;">
    <div style="flex: 1; color: #b4afb7; margin-top: 3%; margin-right:8%; text-align: justify;">
       {{< image src="/images/project/2d_map.png" caption="Figure 1 - 2D Map (Robocup Arena in Bordeaux 2023)" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
    </div>
    <div style="flex: 1; color: #b4afb7; margin-top: 3%; margin-right:0%; text-align: justify;">
        {{< image src="/images/project/3d_map.png" caption="Figure 2 - 3D Map (North Tower Garden - IST)" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
    </div>
</div>

<div style="text-align: justify;">

<!-- As shown in the images above, a map with a 3D point cloud offers significantly more detail and information compared to a 2D map. To better understand what a point cloud is, consider the following example, where a robot captures the legs of a chair and a table using a 2D LiDAR: -->
As demonstrated in the images above, a map with a 3D point cloud provides significantly more detail and information compared to a 2D map. To gain a better understanding of what a point cloud is, consider the following example: a robot captures the legs of a chair and a table using a 2D LiDAR.

</div>

<div style="display: flex; align-items: flex-start;">
    <div style="flex: 1; color: #b4afb7; margin-top: 0%; margin-right:0%; text-align: justify;">
       {{< image src="/images/project/2d_pc.png" caption="Figure 3 - Robot detecting objetcs with a 2D LiDAR" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
    </div>
</div>

<div style="text-align: justify;">

<!-- Navigation using 2D LiDARs in domestic environments generally works well, but quickly comes up against the limitations of this technology. Consider, for example, the one-legged table in the image above; if the top is too large, the robot will collide with it. The same principle applies to various types of furniture, and 3D LiDARs overcome these barriers, making it easier for the robot to navigate autonomously in the face of static and dynamic obstacles, making it more efficient and precise. -->
Navigation using 2D LiDARs in domestic environments generally functions adequately but swiftly encounters the limitations of this technology. Consider, for example, the one-legged table in the image above; if the top is too large, the robot will collide with it. The same principle applies to various types of furniture, and 3D LiDARs overcome these barriers, ensuring easier autonomous navigation for the robot amidst static and dynamic obstacles, thus enhancing efficiency and precision.

<!-- Since the project is part of the SocRob@Home team belonging to the Institute of Systems and Robotics (ISR), it is important to highlight what has already been done and what we are going to do.  -->
Given that the project is part of the SocRob@Home team within the Institute of Systems and Robotics (ISR), it is crucial to emphasize what has already been accomplished and what we intend to undertake with our project.

</div>

<div style="display: flex; align-items: flex-start;">
    <div style="flex: 1; color: #b4afb7; margin-top: 0%; margin-right:0%; text-align: justify;">
       {{< image src="/images/project/pipeline.png" caption="Figure 4 - Pipeline of TIAGo (Adapted from P. U. Lima et al., “SocRob@Home”, KI - Künstliche Intelligenz, vol. 33, no. 4, pp. 343–356, Dec. 2019, doi: 10.1007/s13218-019-00618-w. Adapted with permission.)" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
    </div>
</div>

<div class="image-slider-container">
    <div class="slider-wrapper">
        {{< slider dir="images/feito_e_por_fazer-gallery" class="max-w-[800px] ml-auto mr-auto" height="" width="" webp="true" command="Fit" option="" zoomable="true" >}}
    </div>
    <p class="caption" style="color: #7f7f7f; font-size: 14px;">Figure 5 - What is already done by SocRob@Home and what students will develop</p>
</div>

<div style="text-align: justify;">

<!-- Figures 4 and 5 show that the following navigation tasks will be developed:  -->
Figures 4 and 5 indicate that the subsequent navigation tasks will be developed:

- ##### 3D Mapping

    The current mapping method utilized is called [Gmapping](http://wiki.ros.org/gmapping), a 2D SLAM algorithm that computes a 2D map, as demonstrated in Figure 1. The team is slated to evaluate two 3D SLAM algorithms ([A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) and [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM)), which will generate 3D maps as representations of the environment, akin to the one depicted in Figure 2.

- ##### 3D Localization

    <!-- The 3D localization will be done by researching alternative algorithms to AMCL. Existing algorithms that are capable of capturing a 3D point cloud from the Ouster OS1 LiDAR will be adapted. The aim is to test at least 2 options in simulation and find out which one is the best to proceed with real tests on the robot. -->
    The 3D localization will be achieved by researching alternative algorithms to AMCL. Existing algorithms capable of capturing a 3D point cloud from the Ouster OS1 LiDAR will be adapted. The objective is to test at least two options in simulation and determine which one is optimal for proceeding with real tests on the robot.

- ##### 2D Path Planning/Guidance
<!-- - ##### 3D Path Planning/Guidance -->

</div>

<br>

<div style="text-align: justify;">

<!-- To ensure successful implementation, the robot must exhibit confident movements to guarantee safety for both individuals and objects. Additionally, it should be able to accurately and efficiently sense the 3D environment with at least 5cm (ideally 2.5cm) - with the current 2D navigation method the map has a resolution of 5cm, hence the interest of maintaining this feature.. Furthermore, there should be a favorable balance between the benefits of utilizing a 3D sensor and its associated costs within the application. -->
To ensure successful implementation, the robot must demonstrate confident movements to ensure safety for both individuals and objects. Additionally, it should be capable of accurately and efficiently sensing the 3D environment with a resolution of at least 5cm (ideally 2.5cm). Given that the current 2D navigation method yields a map resolution of 5cm, maintaining this feature is of particular interest. Furthermore, there should be a favorable balance between the benefits of utilizing a 3D sensor and its associated costs within the application.

Another solution requirement is the robot's decision time to react to a dynamic obstacle and avoid a collision, that can is approximated by:

\\[\tau = \frac{d}{v} - \frac{v}{a}\\] 
where:
- <span style="font-size: 130%;">𝜏 </span> - Robot’s decision time in seconds 
- <span style="font-family: 'Times New Roman', Times, serif;">𝑑</span> - Distance between TIAGo and an obstacle in meters (1.5m)
- <span style="font-family: 'Times New Roman', Times, serif;">𝑣</span> - Robot’s velocity in meters per second (limited to 0.5m/s)
- <span style="font-family: 'Times New Roman', Times, serif;">𝑎</span> - Robot's max decelaration in meters per second squared (equal to -0.2m/s<sup>2</sup>)

Having explained this, one can now see how the decision time varies in function of distance and velocity in Figure 6.

<div style="display: flex; align-items: flex-start;">
    <div style="flex: 1; color: #b4afb7; margin-top: 0%; margin-right:0%; text-align: justify;">
       {{< image src="/images/project/graficos_sol_req.png" caption="Figure 6 - Decision time in function of distance and velocity" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
    </div>
</div>

<!-- The graph on the right is an enlargement of the one on the left in the zone of values of greater interest - shorter distances. When the decision time is equal to zero it means that the robot will collide with an obstacle. Hence, for a maximum velocity of 0.5m/s and an arbitrary distance of 1.5m, the decision time is 0.5 seconds. It will be tested if the decision time is obtained for the correpondent velocity and distance values during during the development of the project. -->
The graph on the right is an enlargement of the one on the left in the zone of values of greater interest - shorter distances. When the decision time is equal to zero, it indicates that the robot will collide with an obstacle. Therefore, for a maximum velocity of 0.5m/s and an arbitrary distance of 1.5m, the decision time is 0.5 seconds. It will be tested whether the decision time is obtained for the corresponding velocity and distance values during the development of the project.

<!-- In order to test and validate the metrics, the students will test every module in simulation and in a real environment, on a TIAGo robot as mentioned before. -->
To test and validate the metrics, the students will assess every module both in simulation and in a real environment, utilizing a TIAGo robot as mentioned previously.

<div class="image-slider-container">
    <div class="slider-wrapper">
        {{< slider dir="images/sim_e_testbed-gallery" class="max-w-[800px] ml-auto mr-auto" height="" width="" webp="true" command="Fit" option="" zoomable="true" >}}
    </div>
    <p class="caption" style="color: #7f7f7f; font-size: 14px;">Figure 7 - Testbed simulation and real testbed</p>
</div>

The tests will consist in navigation:
- In the testbed to a random waypoint without dynamic obstacles.
- In the testbed to a random waypoint with a dynamic obstacle (e.g., a person walking).
- In the testbed to a random waypoint with a small obstacle that 2D navigation does not avoid (e.g., sponge).
- From the kitchen to the living room, ensuring the robot avoids complex 2D navigation furniture (e.g., tables with center legs, chairs without back legs).

<!-- The students will repeat each experiment 5 or 10 times, record collisions and successes, and perform a statistical analysis, for the current method and the one developed by the PIC1 team. -->
The students will repeat each experiment 5 or 10 times, record collisions and successes, and conduct a statistical analysis for both the current method and the one developed by the PIC1 team.

It is important to know that the methods currently in use involve the following frequency levels: 
- Localization - 10Hz 
- Path Planning - 2Hz 
- Guidance - 10Hz

Furthermore, the students will compare the frequency levels obtained with the tested methods with those mentioned above.

One final test consists on evaluating the precision of the Localization with a Motion Capture System, based on 12  [OptiTrack PRIME13](https://optitrack.com/cameras/prime-13/) cameras that have a sub-millimeter precision. The error obtained will be compared with the error of the current method used (AMCL - with 0.09 meter accuracy).

<div style="display: flex; align-items: flex-start;">
    <div style="flex: 1; color: #b4afb7; margin-top: 0%; margin-right:0%; text-align: justify;">
       {{< image src="/images/project/optitrack_prime13.png" caption="Figure 8 - OptiTrack PRIME13 (A. David, “The ISRoboNet@Home Testbed,” Institute For Systems and Robotics. Accessed: Jan. 26, 2024.)" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" style="width: 20%;" >}}
    </div>
</div>

</div>

