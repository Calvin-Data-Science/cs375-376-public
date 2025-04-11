---
title: "Autonomous Vehicles"
author: "Young Kwang Choi"
---


### Background

- NHTSA(National Highway Transportation Safety Administration) [states](https://www.nhtsa.gov/technology-innovation/automated-vehicles-safety) that 94% of serious crashes are due to human error and that automated vehicles have the potential to remove human error from the equation.

### What are autonomous cars

An autonomous car is a vehicle capable of sensing its environment and operating without human involvement; a human passenger is not required to take control of the vehicle at any time, nor a human passenger required to be present in the vehicle at all.

### How does it work

In general, autonomous cars include 4 stages of activity: perception, localization, planning and control. Deep learning is implemented on all 4 sections.

- perception
   - find the environment and obstacles around the car
- localization
   - define position in the world/area with a great accuracy
- planning
   - define a trajectory from A to B, using perception and localization
- control
   - follow the trajectory by controlling the car


### Where we currently are

- 52 different companies that [have been approved to test autonomous vehicles](https://abcnews.go.com/US/companies-working-driverless-car-technology/story?id=53872985#:~:text=Some%20of%20the%2052%20different,%2C%20Nissan%2C%20Intel%20and%20Uber.) on the roads of California.
   - [Tesla](https://www.tesla.com/)
   - Baidu / [Apollo System](https://apollo.auto/)
   - [Argo AI](https://www.argo.ai/)
   - NVIDIA / [DRIVE Orin](https://www.nvidia.com/en-us/self-driving-cars/drive-platform/hardware/)
   - [Waymo](https://en.wikipedia.org/wiki/Waymo#Crashes) (Google)
- We are at [Level 3 (Conditional Driving Automation)](https://www.synopsys.com/automotive/autonomous-driving-levels.html#:~:text=Most%20vehicles%20on%20the%20road,does%20not%20qualify%20as%20automation.) in terms of driving automation.
- To be honest, the autonomous car is still far from being fully autonomous.
   - Watch [a person doing Tesla test](https://www.universalhub.com/2022/if-people-can-barely-navigate-south-boston-street) on "Full Self Driving" mode.
- IIHS(Insurance Institute for Highway Safety) Pedestrian Autobrake Tests
   - [Successful example](https://youtu.be/TJgUiZgX5rE?t=175)
   - [Not so successful example](https://youtu.be/TJgUiZgX5rE?t=201)
- IIHS creates [safeguard ratings for partial automation](https://www.iihs.org/news/detail/iihs-creates-safeguard-ratings-for-partial-automation)

### Potential problems

- Current road systems
   - Some roads are unmarked; the lack of uniformity in road signage and stoplights.
- Weather conditions
   - Sensors simply do not work perfectly in heavy bad weather.
- Hacking
- Transparency
   - Waymo sues the California DMV to keep [driverless crash data secret](https://cleantechnica.com/2022/02/01/waymo-sues-the-california-dmv-to-keep-driverless-crash-data-secret/)
- Accident liability
   - **Who is responsible** for accident?
   - **Trolley Problem**
   - Human drivers may be forgiven for making an instinctive decision in split-second, but programmers of automated cars do not have that luxury as they have time to get it right.

### News

- [Tesla X crash in Mountain View, California](https://abc7news.com/tesla-autopilot-crash-car/5966601/)
- [Tesla on autopilot killed two people](https://www.latimes.com/california/story/2022-01-19/a-tesla-on-autopilot-killed-two-people-in-gardena-is-the-driver-guilty-of-manslaughter)
- [The back-up driver of an Uber self-driving car that killed a pedestrian has been charged with negligent homicide](https://www.bbc.com/news/technology-54175359)
