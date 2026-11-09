---
title: NASA Ames Research Center, Aeropulse
role: Concept Design Intern, Aviation Systems Division
dates: June – August 2025
skills: Systems design, UAS routing, airspace integration
summary: Our team of six designed Aeropulse, a concept that moves organs, lab samples, and urgent medicine between hospitals with hybrid VTOL drones and stair-climbing robots.
thumbnail: /assets/img/nasa/thumb_cad.jpg
permalink: /projects/nasa-ames-aeropulse/
images:
- src: /assets/img/nasa/fig04.jpg
  alt: Map of the modeled route from San Francisco General Hospital to Santa Clara Valley Medical Center
  caption: Modeled route (map data © Google)
  w: 1.24
- src: /assets/img/nasa/fig13_hubs.jpg
  alt: Map of proposed drone hubs and trauma centers around the San Francisco Bay
  caption: Proposed drone hubs (imagery © Google)
  w: 2.09
- src: /assets/img/nasa/cad_robot.jpg
  alt: CAD render of the team's tracked hospital robot with two red payload lids
  caption: Robot CAD model (from the memo)
  w: 1.33
what:
- Our team of six designed **Aeropulse**, a concept that moves organs, lab samples, and urgent medicine between hospitals with hybrid VTOL drones and stair-climbing robots, with no manual handoffs
- I was one of 36 students picked from about 800 applicants for the Aviation Systems Division's Concept Design Experience
how:
- I was responsible for drone routing and urban airspace integration
- Examined routing constraints, airspace rules (UTM, geofencing, detect-and-avoid), and trade-offs between the drones and the ground robots
- Conceptualized route planning for both vehicles, with 3-D occupancy-grid routing, GPS, and SLAM for the drones and A* and Dijkstra path planning for the robots
- Planned for operations below 400 ft AGL under **Part 107** with BVLOS waivers
results:
- In our model, a donor heart gets from San Francisco General to Santa Clara Valley Medical Center in about 37 min, compared with 70 to 90+ min today
- Presented the design to 50+ NASA staff
- Co-authored NASA/TM-20250009029 with the rest of the team
---

## The concept

{% include figure.html src="/assets/img/nasa/fig02.png" alt="Concept strip: Hospital A, robot, drone, robot, Hospital B" caption="A robot carries the payload out of Hospital A, rides the drone, and takes it to the right room in Hospital B (from the memo)" %}

## Route planning (my focus area)

Before takeoff, the drone plans its whole route from Hospital A to Hospital B. It takes in the start and end points, altitude limits, the weather forecast, no-fly zones, and open UTM airspace. From those it builds a 3-D occupancy grid and finds the lowest-cost path around obstacles and restricted airspace. Then it asks UTM for emergency priority clearance.

{% include figure.html src="/assets/img/nasa/fig11.png" width="620px" alt="Pre-flight route optimization: define mission, enter input data, map 3-D occupancy grid, plan global route path, request airspace clearance" caption="Pre-flight route planning (from the memo)" %}

In the air, it keeps updating that map. It tracks its position by fusing GPS, IMU, odometry, camera, and LiDAR data with SLAM and a Kalman filter. When something changes, like the weather or another aircraft getting in the way, it replans and sends the new route back through UTM. If it can't continue safely, it can loiter, land somewhere low-risk, return to base, or deploy a parachute.

{% include figure.html src="/assets/img/nasa/fig12.png" width="620px" alt="In-flight route optimization: assess environment, localize, assign speeds and times, fly, detect and avoid obstacles, replan if needed" caption="In-flight route planning (from the memo)" %}

{% include figure.html src="/assets/img/nasa/aero_timing.png" width="620px" alt="Bar chart: Aeropulse about 37 minutes door to door against 70 to 90+ minutes today" caption="Modeled heart transfer, San Francisco General to Santa Clara Valley Medical Center" %}

## Links

- [Read the memo (PDF)](/assets/pubs/NASA-TM-20250009029.pdf)
- [NASA/TM-20250009029 on the NASA Technical Reports Server](https://ntrs.nasa.gov/citations/20250009029)
