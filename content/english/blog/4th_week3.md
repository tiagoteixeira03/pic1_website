---
title: "Week 3 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-05-05T13:28:00Z
image: "/images/Blog/4th_week3/cover.png"
categories: ["4th Period - Weekly Progress"]
authors: 
    - "António Morais"
    - "Tiago Teixeira"
tags: ["mapping", "general"]
draft: false
---

#### 3D Mapping

##### → LIO-SAM

<div style="text-align: justify;">

Following last weeks updates the team made tests with the [Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) robot and the [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) package. To begin this tests an important step was to export the `roscore` of the robot to the [Docker](https://www.docker.com/) container previously built with the following command:
</div>

```bash
export ROS_MASTER_URI=http;//${JACKAL_IP}:11311/
```

<div style="text-align: justify;">

<!-- With this done tests started. But unfortunaly after one straight week of insistent tests, contacting the author of the package and other colleagues at the Institute of Systems and Robotics (ISR), there was no achivement regarding the synchronizatyion of the system LiDAR+IMU (Inertial Measurement Unit). -->
With the preliminary setup completed, testing commenced. However, despite a week of persistent efforts, including reaching out to the package author and consulting colleagues at the Institute of Systems and Robotics (ISR), no progress was made in synchronizing the LiDAR and IMU (Inertial Measurement Unit) system.

<!-- The main problem resides on the initialization of the synchronization where when it is supposed to detect the degree of excitation of the system, when doing the slightest movement of it all the percentages of the axis get to 100% which leads to incorrect parameters. -->
The primary issue lies in the synchronization initialization process. When attempting to detect the system's degree of excitation, even the slightest movement causes all axis percentages to reach 100%, resulting in inaccurate parameters.

<!-- After insisting many times, the team decided to persue other options to the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) algorithm. After some research and suggetions from a coleague at ISR, the team decided to invest their time with a method called [FAST-LIO](https://github.com/hku-mars/FAST_LIO) which authors are the same as the [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) packge. -->
After making several attempts without success, the team opted to explore alternative options to the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) algorithm. Following research and recommendations from a colleague at ISR, they chose to dedicate their efforts to a method known as [FAST-LIO](https://github.com/hku-mars/FAST_LIO) developed by the same authors as the [LiDAR_IMU_Init](https://github.com/hku-mars/LiDAR_IMU_Init) package.
</div>

##### → FAST-LIO

<div style="text-align: justify;">

<!-- A big advantage of this method is that it doesnt require an external Inertial Measurement Unit (IMU) or one with 9 axis (works with 6 axis IMUs), which means that there is no need for configuration for a LiDAR that has an internal IMU. This is extremely helpfull as the [OS1](https://ouster.com/products/hardware/os1-lidar-sensor)] LiDAR the team is using has an internal IMU. Hence when the algorithm was set up immediate tests started with the sensor in discussion and not with the [VLP-16](https://velodynelidar.com/products/puck/) of the [Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) robot. -->
A significant advantage of this method is its compatibility with 6-axis IMUs, eliminating the need for an external IMU or one with 9 axes. This feature simplifies the setup process, particularly beneficial for LiDARs equipped with internal IMUs, such as the [OS1](https://ouster.com/products/hardware/os1-lidar-sensor) LiDAR used by the team. Consequently, immediate testing commenced with the [OS1](https://ouster.com/products/hardware/os1-lidar-sensor) LiDAR instead of the [VLP-16](https://velodynelidar.com/products/puck/) mounted on the [Jackal](https://clearpathrobotics.com/jackal-small-unmanned-ground-vehicle/) robot.

<!-- But first to setup this algorithm the student responsible decided to use [Docker](https://www.docker.com/) again. To do so the student created a script called `run_docker.sh` used to create a container from an image. First it is needed to `git clone` the GitHub repository to the local machine and then run the file but there is the need to make it executable first: -->
Before setting up this algorithm, the responsible student opted to utilize [Docker](https://www.docker.com/) once again. To achieve this, a script named `run_docker.sh` was created for creating a container from an image. Initially, the student cloned the GitHub repository to their local machine and then made the file executable before running it.
</div>

```bash
$ sudo chmod +x <your_custom_name>.sh
```

<div style="text-align: justify;">

The script's main functionalities are described in the following bullet points:

- **Create Workspace Directory:** Creates a directory named `docker_ws` in the user's home directory to serve as the workspace for the [Docker](https://www.docker.com/) container.

- **Allow X Server Access:** Enables access to the X server from the local machine, allowing GUI applications to be displayed.

- **Run Docker Container:** Starts a [Docker](https://www.docker.com/) container named `fastlio2` in interactive mode with the following configurations:
    - **User and Network Configuration:** Runs the container with specific user privileges and network settings.
    - **Volume Mounting:** Mounts certain directorys from the host machine to inside the container, providing easy data exchange between the host and container.
    - **Environment Configuration:** Sets environment variables to enable GUI applications to interact with the X server.
    - **Image Selection:** Uses the [Docker](https://www.docker.com/) image `kenny0407/marslab_fastlio2:latest`, which contains the necessary dependencies and configurations for running [ROS Kinetic](https://wiki.ros.org/kinetic) with GUI support.
    - **Container Shell Access:** Launches a shell inside the container for further interaction and configuration.

After this the user is now able to run the script with:
</div>

```bash
$ ./run_docker.sh
```

<div style="text-align: justify;">

<!-- that will create the container and display a terminal inside it. Then to get to the workspace all is needed is to do the following commands inside the container: -->
Once the container is created and a terminal is displayed inside it, users can navigate to the workspace (and set it up) by executing the following commands within the container:
</div>

```bash
$ cd home/mars_ugv/catkin_ws/
$ source devel/setup.bash
```

<div style="text-align: justify;">

<!-- After this the team started to test with a dataset provided by the authors to make sure everything was working properly. This dataset is called `outdoor_Mainbuilding_10hz_2020-12-24-16-38-00.bag` and it uses a Livox LiDAR.  -->
After this, the team began testing with a dataset provided by the authors to ensure everything was working properly. This dataset, named `outdoor_Mainbuilding_10hz_2020-12-24-16-38-00.bag`, utilizes a [Livox](https://www.livoxtech.com/avia) LiDAR.
</div>

{{< image 
  src="/images/Blog/4th_week3/dataset_fastlio.gif" 
  caption="Figure 1 - Process of running the outdoor_Mainbuilding_10hz_2020-12-24-16-38-00.bag dataset." 
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

<!-- With it working with the dataset mentioned it was time to test with the [OS1](https://ouster.com/products/hardware/os1-lidar-sensor) LiDAR integrated in the TIAGo robot, which means test with real data. For this the team had to develop straightfoward `.launch` and `.yaml` files regarding the parameters of the team's sensor that were then copied to the [Docker](https://www.docker.com/) container. -->
With the algorithm functioning correctly with the mentioned dataset, it was time to test it with the [OS1](https://ouster.com/products/hardware/os1-lidar-sensor) LiDAR integrated into the TIAGo robot, which involved testing with real data. To accomplish this, the team developed straightforward `.launch` and `.yaml` files related to the parameters of the team's sensor. These files were then copied to the [Docker](https://www.docker.com/) container.

<!-- Several datasets were constructed but the one that is shown here was considered the best (the one that produced the best map) and that was decided to be of use in the Localization task. The following gifs are from the same dataset but one shows the building process of the testbed and the other of the all laboratory of mobile robotics. -->
Several datasets were constructed, but the one shown here was considered the best, as it produced the most accurate map. This dataset was chosen for use in the Localization task. The following gifs are from the same dataset, with one showing the construction process of the testbed and the other depicting the entire laboratory of mobile robotics.
</div>

{{< image 
  src="/images/Blog/4th_week3/fastlio_testbed.gif" 
  caption="Figure 2 - Process of running the dataset built of real data (only the testbed) - resolution of 5cm." 
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

{{< image 
  src="/images/Blog/4th_week3/fastlio_all_lab.gif" 
  caption="Figure 3 - Process of running the dataset built of real data (all laboratory of mobile robotics) - resolution of 5cm." 
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

<!-- One can now compare the maps built with the [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) algorithm that were shown in Week 5 (3<sup>rd</sup> Period) and the ones of the figures above. In Robotics map comparison is subjective which means one can intuitively look at both and decide based on visual appearence wich one is better. Doing so we can infer that [FAST-LIO](https://github.com/hku-mars/FAST_LIO) is much better than [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) -->
One can now compare the maps built with the [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) algorithm shown in Week 5 (3<sup>rd</sup> Period) with the ones depicted above. In robotics, map comparison is subjective, allowing one to intuitively assess both and decide based on visual appearance which one is better. From this comparison, it can be inferred that [FAST-LIO](https://github.com/hku-mars/FAST_LIO) outperforms [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM).
</div>

#### Demo-Day Presentation Materials

##### → Poster

<div style="text-align: justify;">

For the Demo-Day the team needs to develop a poster of their project and this week the team started to think about the layout of the poster:
</div>

{{< image 
  src="/images/Blog/4th_week3/poster.png" 
  caption="Figure 4 - Initial layout of the poject poster." 
  alt="alter-text" 
  position="center" 
  command="fill" 
  option="q100" 
  class="img-fluid" 
  title="image title"  
  webp="false" 
>}}

<div style="text-align: justify;">

<!-- The teams idea was to give an introduction in the project in the "Abstract" section, enuntiate the "Problems with 2D-Sensor Based Navigation" and then what the solution that the team is presenting solves regarding the problems ("3D-Sensor Based Navigation"). Then talk about "How the solution was tested" and finally show the "Results". However, the team has had some feedback on this layout and is planning to change it in the upcoming weeks.  -->
The team's plan was to provide an introduction to the project in the "Abstract" section, outline the "Problems with 2D-Sensor Based Navigation," and then present the solution that the team is proposing to address these problems ("3D-Sensor Based Navigation"). Following this, they intended to discuss "How the solution was tested" and conclude with the presentation of the "Results." However, the team has received some feedback on this layout and is planning to make changes in the upcoming weeks.
</div>

##### → Video

<div style="text-align: justify;">

<!-- The team members assigned to create the demo-day video have begun planning its structure. They have agreed on the following elements: -->
The team members tasked with creating the Demo-Day video have commenced planning its structure. They have collectively agreed upon the following elements:

<!-- - **Introduction**: Clearly explain the problem we are addressing, emphasizing that it involves three main aspects: mapping, localization, and planning. -->
- **Introduction**: This segment will provide a clear explanation of the problem being addressed, highlighting its three main aspects: mapping, localization, and planning.

<!-- - **Demonstrations**: For each of these three aspects (mapping, localization, and planning), include simulation videos that compare older approaches with our own. This will highlight the differences and the value our improvements bring to the robot's navigation system. -->
- **Demonstrations**: Each of the three aspects (mapping, localization, and planning) will be illustrated with simulation videos that compare older approaches with the team's improvements. These comparisons will effectively showcase the differences and the value added by the enhancements to the robot's navigation system.

<!-- - **Validation**: Showcase videos of the real robot performing tests that were outlined as validation metrics in our project proposal. These tests will demonstrate the enhanced navigation system, which integrates all three aspects. -->
- **Validation**: The video will feature footage of the real robot executing tests outlined as validation metrics in the project proposal. These tests will serve to demonstrate the effectiveness of the integrated navigation system, encompassing all three aspects.

<!-- Additionally, since the video will be playing on a loop at the demo-day without sound, we plan to include subtitles. These subtitles will use simple language to explain our demonstrations, ensuring that everyone can easily understand the content. -->
Furthermore, recognizing that the video will be playing on a loop at the demo-day without sound, the team plans to incorporate subtitles. These subtitles will utilize simple language to explain the demonstrations, ensuring that the content is easily understandable to all viewers.
</div>
