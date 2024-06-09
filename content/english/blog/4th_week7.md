---
title: "Week 7 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-06-02T12:00:00Z
image: "/images/Blog/4th_week7/cover.png"
categories: ["4th Period - Weekly Progress"]
authors: 
  - "António Morais"
tags: ["General"]
draft: false
---

#### Final Tests

<div style="text-align: justify;">

Last week, the team expressed the intention of performing more trials for each type of test and improving the congruency of the environments.

> Next week, the team intends to increase the number of trials performed for each test and use test environments that are more congruent with each other to ensure the increase in difficulty of each test. 

With this in mind, the team decided to perform 10 trials for each test.

The tests will be denoted as:

- **No obstacles:** Navigation with only a known map.

- **Static obstacles:** Navigation with a known map and two static obstacles.

- **Static obstacles + Static obstacle that 2D-Sensor based Navigation doesn't avoid:** Navigation with a known map, static obstacles, and a suspended object (a board) that the 3D-Sensor-based navigation avoids, but the 2D-Sensor-based navigation would collide with.

- **Static obstacles + Static obstacle that 2D-Sensor based Navigation doesn't avoid + Dynamic obstacle:** Navigation with a known map, static obstacles, a suspended object (a board), and a dynamic obstacle (a person) that the robot needs to detect and calculate another possible trajectory to its destination.

- **Gradually smaller static obstacles:** Navigation with a known map and static obstacles of decreasing sizes that the 2D-Sensor-based navigation has difficulty detecting.

The video demonstrations of each test are presented below.

</div>

{{< image 
  src="/images/Blog/4th_week7/no_obstacles_nav_in_testbed.gif" 
  caption="Figure 1 - Test name: No obstacles." 
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
  src="/images/Blog/4th_week7/cadeiras_2.gif" 
  caption="Figure 2 - Test name: Static obstacles." 
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
  src="/images/Blog/4th_week7/cadeira_com_tabua.gif" 
  caption="Figure 3 - Test name: Static obstacles + Static obstacle that 2D-Sensor based Navigation doesn't avoid." 
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
  src="/images/Blog/4th_week7/cadeiras_tabua_pessoa_para.gif" 
  caption="Figure 4 - Test name: Static obstacles + Static obstacle that 2D-Sensor based Navigation doesn't avoid + Dynamic obstacle." 
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
  src="/images/Blog/4th_week7/little_objects_3.gif" 
  caption="Figure 5 - Test name: Gradually smaller static obstacles." 
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

Finally, the results are compiled in the table below, similar to the one presented on last week's post.
</div>

{{< image 
    src="/images/Blog/4th_week7/table1.png" 
    caption="Figure 6 - Results of all tests." 
    alt="alter-text" 
    height="" 
    width="" 
    position="center" 
    command="fill" 
    option="q100" 
    class="img-fluid" 
    title="image title"  
    webp="false" 
>}}