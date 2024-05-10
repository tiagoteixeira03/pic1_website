---
title: "Week 7 (3rd Period)"
meta_title: ""
description: "meta description for week 7 blog post"
date: 2024-03-31T13:28:00Z
image: "/images/Blog/3rd_week7/cover.png"
categories: ["3rd Period - Weekly Progress"]
authors: 
  - "António Morais"
  - "Catarina Caramalho"
  - "João Pinheiro"
  - "Tiago Teixeira"
tags: ["mapping", "localization", "path planning"]
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
  caption="Figure 2 - IMU debug (TixiaoShan/LIO-SAM: LIO-SAM: Tightly-coupled Lidar Inertial Odometry via Smoothing and Mapping.” Accessed: Apr. 14, 2024.)." 
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
  caption="Figure 3 - Jackal robot from ISR." 
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

#### 3D Localization

<!-- ##### Simulation Results -->
<div style="text-align: justify;">

<!-- Ao correr os algoritmos, foi tambem corrido em paralelo um script em python desenvolvido pelos alunos, cujo objetivo é obter os erros face à localização e à orientação de ambos algoritmos, com o fim de comparar numericamente as alternativas.
Os resultados obtidos são os seguintes: -->
<!--During the execution of the algorithms, the students also simultaneously ran a Python script they had developed. -->
After last week advances, the team developed and ran a Python script, during the execution of both algorithms.
The aim of this script is to calculate the localization and orientation errors of both algorithms in order to make a numerical comparison of them. 
The plots of the position errors as a function of time and the orientation errors as a function of time are the following:
</div>

<div class="image-container">
  <div class="image">
    {{< image 
        src="/images/Blog/3rd_week7/position.png" 
        caption="Figure 4 - Position errors as a function of Time." 
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
        src="/images/Blog/3rd_week7/orientation.png" 
        caption="Figure 5 - Orientation errors as a function of Time." 
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

Note that the time does not start at zero seconds, because the time that is counted is the ROS time, and the error script is one of the last to be launched.

<!-- Como se observa nos graficos, o HDL é de facto o melhor algoritmo a utilizar em simualçao, contudo, isto não é uma condição suficiente/necessaria para que seja o melhor algoritmo a implemnetar no robot real. 
Durante um teste real, a imprecisão do IMU é superior à da simulação, o que deverá de melhorar o desempenho do MCL3D. Já o HDL, não tem tanto em conta as condições do ambiente real, e portanto, os resultados teoricos poderão ser o oposto dos reais, daí a importancia de correr ambos os algoritmos num ambiente simulado e real. -->
As can be seen in the plots, the maximum position error for the HDL is 0.35m, which contrasts with the maximum of 6m achieved by the MCL3D. With regard to orientation errors, the highest peak was 0.11rad for the HDL and 3.1rad for the MCL3D. We can therefore conclude that HDL is indeed the best algorithm to use in simulation. However, this is not a sufficient condition for it to be the best algorithm to be implemented on the real robot. 
During a real test, the inaccuracy of the IMU is higher than that of the simulation, which can improve the performance of MCL3D. On the other hand, HDL doesn't take into account the conditions of the real environment as much, so the theoretical results can be opposite to the real ones. This is why it is essential to test both algorithms in simulated and real environments.
</div>

<div style="text-align: justify;">

Also it is important to refer that the result of the plot, was between -2&pi; and 2&pi;, and we had to normalize it to be between 0 and 2&pi;, due to the physical constraints of the robot.
</div>

<div style="text-align: justify;">

After getting the results of the plots, and analyze them carefully, the team decided to experiment both algorithms in the robot, but due to some technical problems, with the robot, we were not able to try them. We are looking forward to do so in the next couple of weeks.
</div>

#### 2D Path Planning/Guidance


Last week, we began modifying the code of the [poincloud_to_laserscan node](https://github.com/ros-perception/pointcloud_to_laserscan), but we ran into some errors that prevented us from calculating the robot's height based on the transform from the head frame to the base frame. Fortunately, we managed to resolve these issues and accurately calculate the height value. The next step was to determine how frequently we wanted to update this value, and we decided on a frequency of 1 Hz for now.

As shown in the gif below, our modifications to the node had the desired effect. As we extended the robot's torso, the value for the maximum_height variable changed in real time.

<div class="image-container">
    {{< image 
        src="/images/Blog/3rd_week7/dynamic height.gif" 
        caption="Figure 6 - Robot's Height Updating in Real Time." 
        alt="Dynamic Height" 
        height="" 
        width="" 
        position="center" 
        command="fill" 
        option="q100" 
        class="img-fluid" 
        title="Dynamic Height"  
        webp="false" 
    >}}
</div>