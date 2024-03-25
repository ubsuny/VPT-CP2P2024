# Introduction
Video Particle Tracking is a passive micro rheological approach used to study the Brownian motion
of probe particles added to a sample in order to analyze the rheological properties. In Passive microrheology, 
particles movement is due to thermal motion, which allows to measure various properties likes viscosity, 
elasticity, etc.Bead particles mixed in sample are labeled with fluorescent markers so that their
random movement is recorded with video microscopy. Particles must refrain from interacting with each
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

# Physics used for the project
Video Particle tracking analysis to estimate the viscosity of glycerol solution is based on the diffusive motion of bead particles in the glycerol solution. Trajectories of bead particles are observed and analyzed based on various techniques; The movement of the center of mass of bead particles are determined by calculating the position vector R at each time interval based on the velocities of the individual particles[3].
<img width="783" alt="Equation_1" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/9c3255bb-a74b-4d06-b41a-d7aca3046605">
Where $R_0$ is the initial center of mass vector calculated by averaging the coordinates of all the beads in the first frame (k = 1),
$v\_k$ is the mean velocity of all the particles in frame k, 
$v_{i,k}$ is the velocity of particle in frame k in units of μm/frame,
and $N_k$ is the number of particles in frame k and ∆k is the frame difference.


Calculation of ensemble average and time average of the mean square displacement of beads
as a function of lag time is based on equation 2[2, 3].
<img width="826" alt="Equation_2" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/2106d9c8-f514-42b0-8270-2150c150b298">
where x(t) and y(t) are the coordinates of the bead at time t, and ∆t is the time interval also called lag time. Further to extract the diffusion coefficient of the beads MSD plot is fitted using equation 3[4].
<img width="1020" alt="Equation_3" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/288d79cf-cd75-4af7-a2af-1a4c7ba37bbb">
where $\tau$ is the lag time, D is the diffusion coefficient and $\alpha$ known as diffusivity exponent gives the nature of diffusion, $\alpha = 1$ represents normal diffusion,and N is the noise factor.
Using the value of diffusion coefficient estimated by fitting the MSD plot, viscosity η can be evaluated from Stokes Einstein relation given by equation 4[4, 5].
<img width="893" alt="Equation_4" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/9f93f44b-6768-4bd9-b894-3f88084cad04">

Where R is the particle radius, $k_B$ is the Boltzmann coefficient, and T is the temperature in Kelvin.





