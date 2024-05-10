---
title: "Week 1 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-04-21T13:28:00Z
image: "/images/Blog/4th_week1/cover.png"
categories: ["4th Period - Weekly Progress"]
authors:
   - "António Morais"
   - "Tiago Teixeira"
tags: ["path planning", "mapping"]
draft: false
---

#### 2D Path Planning/Guidance

During week #7 of the third period, we completed the first of our two main tasks for 2D Path Planning/Guidance. This involved modifying an existing node to dynamically adjust to changes in the robot's height when converting the 3D point cloud acquired by the Ouster sensor into obstacles on a 2D map.

Moving forward into this week, we transitioned to our next task, which involves calculating an accurate footprint for the robot that updates in real time in response to changes in the robot's arm position. Previously, the robot's footprint was a simple circle, which was adequate enough when the arm was retracted but became inaccurate as its position changed.

To address this, we developed a new ROS package containing a single Python node responsible for calculating and updating the footprint on both the global and local costmaps at a specified frequency. Here's an overview of the steps involved in successfully implementing this:

1. Adding virtual point coordinates forming a circle to a set of points.
2. Calculating the projection on the xz plane of the transform of all robot's frames to the base frame and adding these coordinates to the previous set of points.
3. Adding four virtual points around each point from the robot's arm to simulate thickness.
4. Utilizing the alphashape module to calculate the coordinates for the polygon formed around this set of points.
5. Updating the footprint parameters in the global and local costmaps using the calculated polygon.

In Figure 1 we can see that the robot's footprint (green line on the ground) updates in real time when we move the robot's arm around.

<div class="image-container">
    {{< image 
        src="/images/Blog/4th_week1/footprint.gif" 
        caption="Figure 1 - Robot's Footprint Updating in Real Time." 
        alt="Dynamic Footprint" 
        height="" 
        width="" 
        position="center" 
        command="fill" 
        option="q100" 
        class="img-fluid" 
        title="Dynamic Footprint"  
        webp="false" 
    >}}
</div>

#### 3D Mapping

##### → LIO-SAM

<div style="text-align: justify;">

<!-- Following Week 7's updates the team proceeded to find some intrinsic parameters of the inertial measurement unit (IMU) that are required to be of input in the `LIO-SAM/config/params.yaml` file of the algorithm: -->
Following the updates in Week 7 (3<sup>rd</sup> Period), the team proceeded to find some intrinsic parameters of the Inertial Measurement Unit (IMU) that are required as inputs in the `LIO-SAM/config/params.yaml` file of the algorithm.
</div>

```yaml
# IMU Settings - the following numbers are examples
imuAccNoise: 3.9939570888238808e-03   
imuGyrNoise: 1.5636343949698187e-03
imuAccBiasN: 6.4356659353532566e-05
imuGyrBiasN: 3.5640318696367613e-05
```

<div style="text-align: justify;">

<!-- To find these parameters the team made research about these, such as searching through the documentation of the IMU but did not find such parameters or anything similar. Thankfully there were other people that came across this problem and suggested a package to find these parameters. The team then dove into the so called [`imu_utils`](https://github.com/gaowenliang/imu_utils) package but had some setbacks with errors of the code itself but not of this particular package but of a dependencie of it, another package called [`code_utils`](https://github.com/gaowenliang/code_utils) from the same author of the other one. -->
To identify these parameters, the team delved into researching various resources, including the documentation of the IMU. However, despite their efforts, they didn't uncover the specific parameters needed. Fortunately, it was found that others had encountered the same issue and suggested utilizing a package designed for this purpose. This led the team to explore the [`imu_utils`](https://github.com/gaowenliang/imu_utils) package, a tool recommended by fellow users. While diving into this solution, some challenges were encountered. The code itself was error-free, but difficulties arose with one of its dependencies, namely the [`code_utils`](https://github.com/gaowenliang/code_utils) package from the same author.

<!-- The first error came from trying to build the package itself ([`code_utils`](https://github.com/gaowenliang/code_utils)) about an include problem (this is also documented in issue [#12](https://github.com/gaowenliang/imu_utils/issues/12)): -->
The initial error arose when attempting to build the package itself, specifically the [`code_utils`](https://github.com/gaowenliang/code_utils) package, due to an include problem. This issue has also been documented in detail in issue [#12](https://github.com/gaowenliang/imu_utils/issues/12) on the GitHub repository of [`imu_utils`](https://github.com/gaowenliang/imu_utils).
</div>

```cpp
// File path: code_utils/src/sumpixel_test.cpp
include "backward.hpp"  // wrong - insert '#' at the beginning
include "code_utils/backward.hpp"  // corrected - insert '#' at the beginning
```

<div style="text-align: justify;">

<!-- The next errors are documented in issue [#32](https://github.com/gaowenliang/imu_utils/issues/32). Basicaly there are a bunh of MACROS that need to be changed in the files `code_utils/src/mat_io_test.cpp` and `code_utils/src/sumpixel_test.cpp`: -->
The subsequent errors are outlined in issue [#32](https://github.com/gaowenliang/imu_utils/issues/32) on the GitHub repository of [`imu_utils`](https://github.com/gaowenliang/imu_utils). Essentially, there are several macros that need to be modified within the files `code_utils/src/mat_io_test.cpp` and `code_utils/src/sumpixel_test.cpp`.
</div>

```cpp
// Change the ones on the left to the ones on the right
CV_LOAD_IMAGE_GRAYSCALE -> IMREAD_GRAYSCALE
CV_MINMAX -> CV::NORM_MINMAX
CV_LOAD_IMAGE_UNCHANGED -> IMREAD_UNCHANGED
```

And finally an error on the `code_utils/CMakeList.txt` file:

```cmake
set(CMAKE_CXX_FLAGS "-std=c++11")  # wrong
set(CMAKE_CXX_STANDARD14)  # corrected
```

<div style="text-align: justify;">

<!-- With all of these errors taken care of it was now possible to run the package but to do so a dataset was required. This dataset consisted of at least two hours of duration of IMU data which was exactly what was done. -->
With all of these errors taken care of, it became possible to run the package. However, to do so, a dataset was required. This dataset needed to consist of at least two hours of IMU data, which was exactly what was obtained.

<!-- After this it was created a `.launch` file for the IMU being used in which the topic of the IMU data, the name of the IMU and the minimum duration of data collection (in minutes) were changed: -->
Afterward, a `.launch` file was created for the IMU being used. In this file, the topic of the IMU data, the name of the IMU, and the minimum duration of data collection (in minutes) were modified.
</div>

```xml
<launch>
    <node pkg="imu_utils" type="imu_an" name="imu_an" output="screen">
        <param name="imu_topic" type="string" value= "/imu/data_raw"/>  <!-- Changed IMU topic name -->
        <param name="imu_name" type="string" value= "px4"/>  <!-- Changed IMU name -->
        <param name="data_save_path" type="string" value= "$(find imu_utils)/data/"/>
        <param name="max_time_min" type="int" value= "105"/>  <!-- Changed minimum time (in minutes) for collection of data -->
        <param name="max_cluster" type="int" value= "100"/>
    </node>
</launch>
```

<div style="text-align: justify;">

<!-- Once this taken care of one could now run the package for the dataset constructed. After this the team obtained the parameters they needed which were witten: -->
Once these adjustments were made, the package could be executed with the constructed dataset. Following this, the team obtained the necessary parameters:
</div>

```yaml
#  File path: imu_utils/data/px4_imu_param.yaml
%YAML:1.0
---
type: IMU
name: px4
Gyr:
   unit: " rad/s"
   avg-axis:
      gyr_n: 1.8191460790771266e-03  # imuGyrNoise
      gyr_w: 4.5119119003007975e-05  # imuGyrBiasN
   x-axis:
      gyr_n: 1.9496415895800541e-03
      gyr_w: 4.1344704259625771e-05
   y-axis:
      gyr_n: 1.6858078760147014e-03
      gyr_w: 6.7641044580978528e-05
   z-axis:
      gyr_n: 1.8219887716366247e-03
      gyr_w: 2.6371608168419629e-05
Acc:
   unit: " m/s^2"
   avg-axis:
      acc_n: 2.5432491530286979e-02  # imuAccNoise
      acc_w: 7.9166594255487604e-04  # imuAccBiasN
   x-axis:
      acc_n: 3.4098258318774562e-02
      acc_w: 9.3291404872930051e-04
   y-axis:
      acc_n: 2.2888249908200251e-02
      acc_w: 7.7128773939743591e-04
   z-axis:
      acc_n: 1.9310966363886121e-02
      acc_w: 6.7079603953789149e-04
```

<div style="text-align: justify;">

<!-- Next week teams efforts will be towards finding other parameters required for the algorithm in discussion that will be described on next weeks post. -->
Next week, the team's efforts will be focused on finding other parameters required for the algorithm under discussion, which will be described in next week's post.
</div>
