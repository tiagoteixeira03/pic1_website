---
title: "Week 1 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-04-21T13:28:00Z
image: "/images/Blog/4th_week1/cover.png"
categories: ["4th Period - Weekly Progress"]
author: "Tiago Teixeira"
tags: ["path planning"]
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
        caption="Figure 1 - Robot's Footprint Updating in Real Time" 
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