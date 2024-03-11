---
title: "Week 3 - 3D Mapping"
meta_title: ""
description: "meta description for week 3 blog post"
date: 2024-03-03T13:28:00Z
image: "/images/Blog/week3/ElectroCap-Challenge.png"
categories: ["Weekly Progress"]
author: "António Morais"
tags: ["updates", "mapping"]
draft: false
---

#### Mapping

##### → LIO-SAM

On Week 2 the team made progress regarding the [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) algorithm about testing it with datasets. This week there was no remarkable progress because of the need to study the code of it in detail which was what the team focused on.

##### → A-LOAM

Last week's problems ecountered were thought carefully and a solution was found. Fortunately, the algorithm's developers had foreseen such scenarios and offered [Docker](https://docs.docker.com/get-started/overview/) support, proving to be an invaluable asset in circumventing compatibility challenges.

<!-- António Morais proceeded to learn the basics of Docker and tried to run the algorithm with a dataset (provided by the authors) after exporting the roscore from Docker to his local machine but on [Rviz](http://wiki.ros.org/rviz) it wasn't showing the data gathered from the environment. The problem ocurring was that on the code of the algorithm, there were lines regarding `.frame_id`'s that had to be changed due to differences between the ROS's versions at stake: -->
António Morais subsequently undertook the task of familiarizing himself with Docker's fundamentals. He then endeavored to execute the algorithm using a dataset provided by the authors. Despite successfully exporting the roscore from Docker to his local machine, an unforeseen issue arose during visualization in [Rviz](http://wiki.ros.org/rviz), where the gathered environmental data failed to display.