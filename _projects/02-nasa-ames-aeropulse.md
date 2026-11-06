---
title: NASA Ames Research Center, Aeropulse
dates: June 2025 – August 2025
role: Concept Design Intern, Aviation Systems Division
skills: Systems design, UAS routing, airspace integration
summary: 'Our team of six designed Aeropulse, a concept for moving organs, lab samples, and urgent medicine between hospitals using hybrid VTOL drones and stair-climbing ground robots, with no manual handoffs.'
thumbnail: /assets/img/nasa/thumb.jpg
permalink: /projects/nasa-ames-aeropulse/
---

## Overview

I was one of 36 students selected from about 800 applicants for the Aviation Systems Division's Concept Design Experience. Our team of six designed Aeropulse, a network of hybrid VTOL drones and stair-climbing robots that moves organs and urgent medical supplies between hospitals without hand-offs. The study was published as NASA Technical Memorandum NASA/TM-20250009029.

## Individual responsibilities

- Analyzed drone routing and urban airspace integration (see below)
    - Pre-flight planning around no-fly zones, altitude limits, weather and UTM clearance
    - In-flight detect-and-avoid, re-routing and fallback options for failures
    - Operations under 400 ft AGL under Part 107 with BVLOS waivers
- Evaluated trade-offs between the drone and robot segments of the system
- Presented the design to 50+ NASA staff and co-authored the Technical Memorandum

{% include figure.html src="/assets/img/nasa/fig02.png" alt="Concept strip: Hospital A, robot, drone, robot, Hospital B." caption="The Aeropulse concept: a robot carries the payload out of Hospital A, rides a hybrid VTOL drone, and delivers it inside Hospital B" %}

{% include gallery.html images="/assets/img/nasa/fig04.jpg | /assets/img/nasa/fig16.jpg" alts="Map of the modeled route from San Francisco General Hospital to Santa Clara Valley Medical Center. | The team's sub-scale 3D-printed robot prototype with tracks and a red payload lid." height="290px" caption="(L to R): Modeled delivery route from San Francisco General to Santa Clara Valley Medical Center (map data © Google), the team's sub-scale 3D-printed robot prototype" %}

## My focus area: drone route planning

Before each mission the drone plans its route from Hospital A to Hospital B. The inputs are the start and end coordinates, altitude limits, the weather forecast, no-fly zones and UTM airspace availability. These are compiled into a 3-D occupancy grid, the global path is planned around obstacles and restricted airspace at the lowest cost, and the drone requests emergency priority clearance through UTM.

{% include figure.html src="/assets/img/nasa/fig11.png" width="600px" alt="Pre-flight route optimization: define mission, enter input data, map 3D occupancy grid, plan global route path, request airspace clearance." caption="**Figure 1.** *Pre-flight route optimization, from the memo.*" %}

In flight, the drone keeps its map updated and fuses GPS, IMU, odometry, camera and LiDAR data with SLAM and a Kalman filter to track where it is. If the weather shifts, another aircraft conflicts or a new restriction appears, it replans and resubmits the route through UTM. If it can't continue safely, it can loiter, land at a low-risk site, return to base or deploy a parachute.

{% include figure.html src="/assets/img/nasa/fig12.png" width="600px" alt="In-flight route optimization: assess environment, perform localization, assign speeds and times, initiate flight, detect and avoid obstacles, replan route if needed." caption="**Figure 2.** *In-flight route optimization, from the memo.*" %}

{% include figure.html src="/assets/img/nasa/aero_timing.png" width="560px" alt="Bar chart: Aeropulse about 37 minutes door to door against 70 to 90+ minutes today." caption="**Figure 3.** *Modeled heart transfer, San Francisco General to Santa Clara Valley Medical Center: about 37 min against 70 to 90+ min today.*" %}

## Links

- [NASA/TM-20250009029 on the NASA Technical Reports Server](https://ntrs.nasa.gov/citations/20250009029)
