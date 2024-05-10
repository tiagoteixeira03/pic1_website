---
title: "Week 2 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-04-28T13:28:00Z
image: "/images/Blog/4th_week2/cover.png"
categories: ["4th Period - Weekly Progress"]
authors: 
  - "António Morais"
  - "João Carranca"
tags: ["mapping", "path planning"]
draft: false
---

#### 3D Mapping

##### → LIO-SAM

<div style="text-align: justify;">

<!-- Following last weeks advancements the algorithm still requires some parameters that represent the transformation of the system LiDAR-IMU (inertial measurement unit). This transformation was presented in Week 7's post (3<sup>rd</sup> Period). These will be an input to the `LIO-SAM/config/params.yaml` file: -->
Following last week's advancements, the algorithm still requires parameters representing the transformation of the LiDAR-IMU system (inertial measurement unit). This transformation was presented in the post from Week 7 (3<sup>rd</sup> Period). These parameters will serve as input to the `LIO-SAM/config/params.yaml` file.
</div>

```yaml
# Extrinsics: T_lb (lidar -> imu) - not changed
extrinsicTrans: [0.0, 0.0, 0.0]
extrinsicRot: [-1, 0, 0,
               0, 1, 0,
               0, 0, -1]
extrinsicRPY: [0, -1, 0,
               1, 0, 0,
               0, 0, 1]
```

<div style="text-align: justify;">

<!-- To obtain these parameters a package is refered on issue [#335](https://github.com/TixiaoShan/LIO-SAM/issues/335) of the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) GitHub repository. The package is called [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) which calibrates the temporal offset and extrinsic parameter between LiDARs and IMUs. -->
To obtain these parameters, a package referenced in issue [#335](https://github.com/TixiaoShan/LIO-SAM/issues/335) of the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) GitHub repository is utilized. The package is known as [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init), designed to calibrate the temporal offset and extrinsic parameters between LiDARs and IMUs.

<!-- The student responsible for mapping delved into this package and configurated it using [Docker](https://www.docker.com/) once again. To set up the environment it is first needed to `git clone` the GitHub repository and then build the [Docker](https://www.docker.com/) image: -->
The student in charge of mapping explored this package and configured it using [Docker](https://www.docker.com/) once again. Setting up the environment involves first `git clone` of the GitHub repository and then building the [Docker](https://www.docker.com/) image:
</div>

```bash
$ cd ~/catkin_ws/src/LiDAR_IMU_Init/docker
$ docker build -t <repo_name>:<tag>
```
<div style="text-align: justify;">

Then enter the command below in the local terminal to enable [Docker](https://www.docker.com/) to communicate with Xserver on the host:
</div>

```bash
$ xhost +local:docker
```

<div style="text-align: justify;">

With this done one can now run the container of the package with the following command:
</div>

```bash
$ dockerdocker run --privileged -it \
   --volume=${LiDAR_IMU_Init_repo_root}:/home/catkin_ws/src \
   --volume=/tmp/.X11-unix:/tmp/.X11-unix:rw \
   --net=host \
   --ipc=host \
   --shm-size=1gb \
   --name=${docker container name} \
   --env="DISPLAY=$DISPLAY" \
   ${docker image name} /bin/bash
```

<div style="text-align: justify;">

<!-- A terminal inside the container should open up and now the the package needs to be compiled, then is needed to source the environment and run the actual package. The following commands do all the steps mentioned. -->
A terminal inside the container should open up. Now, the package needs to be compiled. Then, it's necessary to source the environment and run the actual package. The following commands perform all the mentioned steps.
</div>

```bash
$ catkin_make
$ source devel/setup.bash
$ roslaunch lidar_imu_init <filename>.launch
```

<div style="text-align: justify;">

<!-- Similarly to other packages/algorithms used the team firstly checked if the method was working with the authors provided datasets. The one tested is called `VLP16_IMU.bag` and is available to download in the [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) GitHub repository. This one is specially important to test because the LiDAR is the same as the one that the team is using with the [Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) robot and also contains data from an external IMU (same situation as the team's). -->
Similarly to other packages and algorithms used, the team initially checked if the method was working with the authors' provided datasets. The one tested is called `VLP16_IMU.bag` and is available for download in the [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) GitHub repository. This dataset is particularly important to test because the LiDAR is the same as the one that the team is using with the [Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) robot and also contains data from an external IMU, mirroring the team's setup.
</div>

{{< image 
  src="/images/Blog/4th_week2/lidar_imu_init.gif" 
  caption="Figure 1 - Process of running the VLP16_IMU.bag dataset." 
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

<!-- One can see from the video above that the package seems to be working fine as during the play of the dataset as it detected the degree of excitation of each axis, then does an online refinement for to play the the [FAST-LIO](https://github.com/hku-mars/FAST_LIO) algorithm to verify that the parameters determined by the synchronization are fine. This is also noticed by watching the map being constructed. -->
From the video above, it appears that the package is functioning properly. During the dataset playback, it successfully detects the degree of excitation of each axis. Additionally, it performs an online refinement to apply the [FAST-LIO](https://github.com/hku-mars/FAST_LIO) algorithm, verifying the accuracy of the parameters determined by the synchronization process. This can also be observed by observing the construction of the map.

<!-- Further real tests with the [Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) robot were performed this week but they are not documented here as they were not conclusive in a way that no important results were achieved. -->
Further real tests were conducted with the [Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) robot this week. However, the outcomes were inconclusive as no significant results were achieved.
</div>

### 2D Path Planning/Guidance

<div style="text-align: justify;">

<!-- During week 2, we tested both nodes of our code in simulation to verify whether or not the code we have developed has the impact we expect. 

For this, we designed specific tests to properly evaluate both the dynamic adjustments of the robot's height and the dynamic adjustment of its footprint. 

For the footprint, for example, we tested situations where the extension of the robot's arm would have an impact on its course and decision to take specific paths or not. One of these tests, for example, involved putting the simulated robot in front of an entry point that would be traversable with the arm in its contained state but not while fully spread out. We would expect, in such a setting, that in the first case, the robot would advance without issue, while halting its progress in the second case due to it realizing that a collision would occur. This is indeed what we observed in simulation, proving that the footprint adjustment works in practical scenarios that involve interactions with the simulated environment. 

For the height adjustment node, we used a similar approach, using an obstacle that would be insignificant if the robot's height was small enough but that would become an obstacle after a certain height limit is reached and surpassed. Similarly to the footprint case, we observed that in the first scenario, the robot progresses without issue, while in the second scenario, it halts its progress in order to avoid collisions. 

With these tests and other similar ones, we were able to verify that, in a simulated environment, we achieve the expected results, confirming the validity of the developed code. -->
During this week, the team conducted tests on both nodes of the code in simulation to assess their impact as intended. Specific tests were devised to evaluate the dynamic adjustments of the robot's height and footprint.

For the footprint adjustments, scenarios were designed to assess situations where the extension of the robot's arm would affect its path selection. One test involved placing the simulated robot in front of an entry point that was traversable with the arm in a contained state but not when fully extended. The simulation demonstrated that the robot advanced smoothly in the former case but halted in the latter to avoid a collision, validating the effectiveness of the footprint adjustment in practical scenarios.

Similarly, for the height adjustment node, tests were conducted using obstacles that were insignificant at lower heights but became obstacles at higher elevations. The simulation revealed that the robot progressed unhindered at lower heights but stopped to avoid collisions when surpassing the height limit.

Through these tests and others, the team confirmed in the simulated environment that the code achieved the expected results, validating its effectiveness.
</div>
