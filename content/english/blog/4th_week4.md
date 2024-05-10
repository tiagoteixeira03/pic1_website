---
title: "Week 4 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-05-12T13:28:00Z
image: "/images/Blog/4th_week4/cover.png"
categories: ["4th Period - Weekly Progress"]
author: "João Carranca"
tags: ["path planning"]
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
