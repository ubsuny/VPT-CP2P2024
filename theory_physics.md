# Introduction
Video Particle Tracking is a passive micro rheological approach used to study the Brownian motion
of probe particles added to a sample in order to analyze the rheological properties. In Passive microrheology, 
particles movement is due to thermal motion, which allows to measure various properties likes viscosity, 
elasticity, etc.Bead particles mixed in sample are labeled with fluorescent markers so that their
random movement is recorded with video microscopy. Par- ticles must refrain from interacting with each
other or with the sample they’re suspended in to ensure their motion remains unaffected by 
interactions[1]. To understand how this movement reflects the material’s rheological characteristics,
each particle’s path is followed. Once the motion of these particles is captured, their positions in 
each video frame are determined by finding the center of their brightness, 
and then these positions are connected to trace their paths over time.

Mean Square Displacement(MSD) calculated as a function of lag time is a statistically relevant 
result that can be estimated from the motion of bead particles collected over numbers of frames
in a VPT experiment. MSD measures how much a particle’s position changes over time compared to its 
starting point[2]. It is commonly used to quantify the spatial extent of random mobility and a way 
to study the dynamical properties of the system.

We determine the viscosity of 70% glycerol solution by observing and tracking the motion of bead particles 
measuring 4.22 micrometers in diameter using video microscopy. The recorded 
movements of the bead particles were enhanced through optimization techniques such as 
tracking, filtering, and linking in Im- ageJ software, with specific parameters tailored to the 
analysis. We collected three different videos with different number (16, 19, & 23) of tracks for 
analysis. The trajectories of particles were graphically analyzed using python software tools. 
Plot of MSD as a function of time allows us to determine the diffusivity constant, from which 
the viscosity of 70% glycerol solution was estimated using Stoke Einstein’s relation.


