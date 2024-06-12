---
# Banner
banner:
  title: "Indoor 3D-Sensor Based Navigation"
  content: "Welcome to our project! We are a team of six students at Instituto Superior Técnico (IST) within the ElectroCap Program, an initiative from the Department of Electrical and Computer Engineering (DEEC) under the 1st Cycle Integrated Project (PIC1). Along with SocRob@Home at the Institute for Systems and Robotics (ISR) we are working on a TIAGo robot, developing an indoor 3D-sensor based navigation."
  image: "/images/tiago_robot.gif"
  button1:
    enable: true
    label: "Project Proposal"
    link: "https://drive.google.com/uc?export=download&id=1KlvVszPfeou4RQMEsc0svV8N6MLE5lv0"
  button2:
    enable: true
    label: "Mid Pitch"
    link: "https://drive.google.com/uc?export=download&id=1zE3jWg3Sm2TsN3edCNeCnta-G8qGnxKi"
  button3:
    enable: true
    label: "Final Pitch"
    link: "https://drive.google.com/uc?export=download&id=1op122lel-SBj3luwb7RI2G2J5BKqBa1o"


# Features
features:
  - title: "2D sensor-based Navigation"
    image: "/images/Hokuyo.png"
    content: "The project is part of the SocRob@Home team at the ISR. Currently, the team uses Hokuyo sensors (2D LiDARs) to perform navigation. Although this approach works effectively, it has some limitations. This is where the PIC1 team steps in.<br><br> Navigation based on 3D LiDARs offers a much greater level of detail, however, it is more computationally challenging. For this reason, it is not common for indoor robots to use this type of sensor. Therefore, this is an emerging area of research and development, which is of great interest to this project."
    # bulletpoints:
    #   - "Zero JS, by default: No JavaScript runtime overhead to slow you down."
    #   - "Customizable: Tailwind, MDX, and 100+ other integrations to choose from."
    #   - "UI-agnostic: Supports React, Preact, Svelte, Vue, Solid, Lit and more."
    button:
      enable: false
      label: "Get Started Now"
      link: "#"
  - title: "3D sensor-based Navigation"
    image: "/images/ouster.png"
    content: "The transition from 2D to 3D LiDAR-based navigation requires the integration of Ouster OS1. This LiDAR will capture a 3D point cloud, offering substantial advantages, including the Z coordinate data acquisition.<br><br>For this project, it is necessary to adapt the entire navigation module, including mapping, localization and path planning/guidance, to take advantage of this information effectively. As part of the project, sub-teams were set up to deal with each of these tasks.<br><br>To access the list of materials used in this project, download the materials list."
    # bulletpoints:
    #   - "Zero JS, by default: No JavaScript runtime overhead to slow you down."
    #   - "Customizable: Tailwind, MDX, and 100+ other integrations to choose from."
    #   - "UI-agnostic: Supports React, Preact, Svelte, Vue, Solid, Lit and more."
    button:
      enable: true
      label: "List of Materials"
      link: "https://drive.google.com/file/d/1SouI8sfaZyrtQFAuF7zKRp8EEdvZR_NO/view?usp=sharing"
---