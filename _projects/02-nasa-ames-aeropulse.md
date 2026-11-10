---
title: NASA Ames Research Center, Aeropulse
role: Concept Design Intern, Aviation Systems Division
dates: June – August 2025
skills: Systems design, UAS routing, airspace integration
summary: Our NASA Ames team's concept for moving organs and urgent medicine between Bay Area hospitals by drone and robot. I worked out how the drones would route through city airspace.
intro: Organs, lab samples, and urgent medicine usually move between hospitals by courier or ambulance, through traffic and several handoffs. In summer 2025, I was one of 36 students picked from about 800 applicants for the Aviation Systems Division's Concept Design Experience at NASA Ames, and our six-person team designed Aeropulse, a concept that replaces that chain with drones and stair-climbing robots. I was responsible for drone routing and urban airspace integration. Aeropulse is a concept study. Apart from a small 3D-printed model of the robot, nothing was built or flown.
thumbnail: /assets/img/nasa/thumb_skylane.jpg
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
- src: /assets/img/nasa/skylane.jpg
  alt: Sky-Drones SkyLane hybrid VTOL drone parked on grass
  caption: SkyLane hybrid VTOL, the drone we based Aeropulse on (photo © Sky-Drones)
  w: 1.33
---

## The problem

Our memo opens with a UNOS review of about 8,800 organ shipments from 2014 to 2019. Nearly 170 organs were thrown out, and 370 more were near misses, because of transport delays of two hours or more. Helicopters are faster, but they're used in fewer than 3% of transfers because of cost. Most transfers go by road, and every handoff along the way, from courier to vehicle to hospital intake to the operating room or lab, is another chance for a delay or a mistake.

## The concept

{% include figure.html src="/assets/img/nasa/fig02.png" alt="Concept strip: Hospital A, robot, drone, robot, Hospital B" caption="A robot carries the payload out of Hospital A, rides the drone, and takes it to the right room in Hospital B (from the memo)" %}

A ground robot picks up the payload inside Hospital A and takes the elevator to the roof. A hybrid VTOL drone lifts the robot on a tethered hoist, flies it to Hospital B, and lowers it onto the roof, where the robot finishes the trip to the right room. Nobody has to hand anything off.

We based the drone on Sky-Drones' SkyLane. Its petrol engine for cruise gives it more range and better wind tolerance than an all-electric drone, and it can carry the 30 lb robot plus cargo. We also reached out to more than 20 physicians and staff at trauma centers and general hospitals for feedback on the idea.

## My part: routing through city airspace

The drone segment had to fit into crowded airspace over the Bay Area, so I worked on how each flight would be planned and what happens when something changes.

Before takeoff, the drone plans its whole route from Hospital A to Hospital B. It takes in the start and end points, altitude limits, the weather forecast, no-fly zones, and open UTM airspace, builds a 3-D occupancy grid from them, and finds the lowest-cost path around obstacles and restricted airspace. Then it asks UTM for emergency priority clearance.

{% include figure.html src="/assets/img/nasa/fig11.png" width="620px" alt="Pre-flight route optimization: define mission, enter input data, map 3-D occupancy grid, plan global route path, request airspace clearance" caption="Pre-flight route planning, from mission definition to the UTM clearance request (from the memo)" %}

In the air, it keeps updating that map. It tracks its position by fusing GPS, IMU, odometry, camera, and LiDAR data with SLAM and a Kalman filter. If the weather changes or another aircraft gets in the way, it replans and sends the new route back through UTM, and if it can't continue safely, it can loiter, land somewhere low-risk, return to base, or deploy a parachute.

{% include figure.html src="/assets/img/nasa/fig12.png" width="620px" alt="In-flight route optimization: assess environment, localize, assign speeds and times, fly, detect and avoid obstacles, replan if needed" caption="In-flight replanning loop, including detect-and-avoid (from the memo)" %}

We planned for flights below 400 ft AGL under Part 107, with BVLOS waivers. I also looked at the trade-offs between the drone and the ground robots, since the two segments had to hand off cleanly on every roof.

## What came out of it

{% include figure.html src="/assets/img/nasa/aero_timing.png" width="620px" alt="Bar chart: Aeropulse about 37 minutes door to door against 70 to 90+ minutes today" caption="Modeled heart transfer, San Francisco General to Santa Clara Valley Medical Center. Both bars are estimates, not measured trips." %}

In our model, a donor heart gets from San Francisco General to Santa Clara Valley Medical Center in about 37 minutes, compared with 70 to 90+ minutes today. For that estimate we used 110 km/h for the drone instead of its quoted 80-knot cruise, to leave room for airspace restrictions and coordination. It's still a first-order estimate, not a measured flight.

We presented the design to more than 50 NASA staff and published it as NASA/TM-20250009029. All six of us are listed as equal authors.

- [Read the memo (PDF)](/assets/pubs/NASA-TM-20250009029.pdf)
- [NASA/TM-20250009029 on the NASA Technical Reports Server](https://ntrs.nasa.gov/citations/20250009029)
