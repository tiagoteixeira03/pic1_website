---
title: "Week 6 (4th Period)"
meta_title: ""
description: "meta description for week 1 blog post"
date: 2024-05-26T12:00:00Z
image: "/images/Blog/4th_week6/cover.png"
categories: ["4th Period - Weekly Progress"]
authors: 
    - "António Morais"
    - "João Carranca"
tags: ["general"]
draft: false
---

#### Final Tests

<div style="text-align: justify;">

<!-- Final tests on the robot continued although TIago's torso issues still heavily limit the amount of time we can spend on tests on any given day. Due to the malfunctions, the robot's autonomy is very reduced and after less than an hour of testing it shuts down, becoming innoperable for the rest of the day.
 When functioning properly, however, we have been able to carry out some of the planned tests successfully, with the robot being able to navigate and avoid collisons without obstacles, with static obstacles, with dynamic obstacles and smaller sized static obstacles. 
As dynamic obstacles, we used people and verified not only the robot's ability to properly avoid moving people but its high reaction time as well. We used a bin for our first test with smaller static obstacles, which also succeeded. 
Replicating tests has proven difficult given the aformentioned issues but the results we have obtained when free from these constraints have been encouraging. -->
Final tests on the robot continued despite TIAGo's torso issues, which heavily limit the amount of testing time each day. Due to these malfunctions the robot's autonomy is significantly reduced and after less than an hour of testing it shuts down and becomes inoperable for the rest of the day.

<!-- However, when functioning properly, some of the planned tests have been successfully carried out. The robot has been able to navigate and avoid collisions in scenarios without obstacles, with static obstacles, with dynamic obstacles, and with smaller-sized static obstacles. For dynamic obstacles, people were used, and the robot's ability to properly avoid moving individuals, as well as its high reaction time, was verified. A bin was used for the first test with smaller static obstacles, which also succeeded. -->
However, when functioning properly some of the planned tests have been successfully carried out. The robot has been able to navigate and avoid collisions in scenarios without obstacles, with static obstacles and with dynamic obstacles. The robot's ability to properly avoid moving individuals as well as its high reaction time was verified. 

Replicating tests has proven difficult due to the aforementioned issues, but the results obtained when free from these constraints have been encouraging.

Next, the robot is shown moving without obstacles, using only a known map of the testbed.
</div>

{{< image 
  src="/images/Blog/4th_week6/no_obstacles_nav_in_testbed.gif" 
  caption="Figure 1 - TIAGo robot moving in the testbed without obstacles, only with a known map." 
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

For tests with static and dynamic obstacles, the team had to perform them in an outer area of the testbed, specifically the hall of the laboratory of mobile robotics (LMR). This was necessary because tests were not successful in the testbed for reasons that are still unknown to the team.

The first test consisted of a route with only static obstacles, and the robot successfully passed the test in all five trials that were performed.
</div>

{{< image 
  src="/images/Blog/4th_week6/cadeiras_2.gif" 
  caption="Figure 2 - TIAGo robot moving in the LMR along a route with only static obstacles." 
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

Next, the difficulty of the tests was increased. The team maintained the static obstacles but introduced a dynamic obstacle (a person). This test was also successfully passed in all five trials.
</div>

{{< image 
  src="/images/Blog/4th_week6/cadeiras_mais_pessoa_obstaculo_dinamico.gif" 
  caption="Figure 3 - TIAGo robot moving in the LMR along a route with static and dynamic obstacles." 
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

Consequently, the test that is the primary motivation behind this entire project was performed. For this test, a chair and a suspended board were used to construct an environment where the robot would collide with a 2D-sensor-based navigation system, but avoid collisions with a 3D-sensor-based navigation system. The results of this test are as follows:
</div>

{{< image 
  src="/images/Blog/4th_week6/cadeira_com_tabua.gif" 
  caption="Figure 4 - TIAGo robot moving in the LMR along a route with static objects (a chair and a suspended board on it)." 
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

As evident from the video above the test was successful, and the team is proud to state that it was surpassed in all five trials.

In the following table, the final results of all tests performed are compiled:
</div>

{{< image 
    src="/images/Blog/4th_week6/table1.png" 
    caption="Figure 5 - Results of all tests." 
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

<div style="text-align: justify;">

Let us now recall a solution requirement proposed by the team regarding the robot's decision time, which is better described in the Project section of this website:

> Therefore, for a maximum velocity of 0.5m/s and an arbitrary distance of 1.5m, the decision time is 0.5 seconds

In the tests performed, a velocity of 0.3 m/s instead of 0.5m/s was used to ensure greater safety, as the students did not want to be responsible for any crashing situations. Considering Figure 3, students measured the distance from the robot to the chair on the right and the distance from the robot to the person walking.

- Distance from the robot to the chair ~ 1 meter.
- Distance from the robot to the person walking ~ 15 centimeters.

From the graphs showed in the Project section one can also get a solution requirement for 0.3m/s:
</div>

{{< image 
    src="/images/Blog/4th_week6/requirement.png" 
    caption="Figure 6 - Solution requirement for a velocity of 0.3m/s." 
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

<div style="text-align: justify;">

Solution requirements for a velocity of 0.3m/s:

- For a distance of approximately 1 meter the decision time should be around 1.8 seconds.
- For a distance of approximately 15 centimeters the decision time is determined to be 0 seconds which means there should be a collision.

According to the various tests performed in an environment with two static obstacles and a dynamic obstacle (visible in Figure 3), it can be observed that for a distance of approximately 1 meter (from the robot to the chair on the right), the cost map (the cyan-purple stains on the map) is updated almost instantly, as is the path calculated by the robot considering new obstacles. Although the team was not able to obtain a specific value for this requirement, it can be approximately stated that the team's solution meets the requirement.

Regarding the ~15 centimeter requirement the team's expectation was for a collision, but as demonstrated in Figure 3 this does not occur. Thus, it can be inferred that this requirement was also met.

##### → Next week

Next week, the team intends to increase the number of trials performed for each test and use test environments that are more congruent with each other to ensure the increase in difficulty of each test. 

The team will also need to prepare the final documents to be submitted for evaluation (Poster, Video and Final Pitch).
</div>