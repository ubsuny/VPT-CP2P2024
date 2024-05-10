# Introduction
Video Particle Tracking is a passive micro rheological approach used to study the Brownian motion
of probe particles added to a sample in order to analyze the rheological properties. In Passive microrheology, 
particles movement is due to thermal motion, which allows to measure various properties likes viscosity, 
elasticity, etc.Bead particles mixed in sample are labeled with fluorescent markers so that their
random movement is recorded with video microscopy. Particles must refrain from interacting with each
other or with the sample they’re suspended in to ensure their motion remains unaffected by 
interactions[^1]. To understand how this movement reflects the material’s rheological characteristics,
each particle’s path is followed. Once the motion of these particles is captured, their positions in 
each video frame are determined by finding the center of their brightness, 
and then these positions are connected to trace their paths over time.

Mean Square Displacement(MSD) calculated as a function of lag time is a statistically relevant 
result that can be estimated from the motion of bead particles collected over numbers of frames
in a VPT experiment. MSD measures how much a particle’s position changes over time compared to its 
starting point[^2]. It is commonly used to quantify the spatial extent of random mobility and a way 
to study the dynamical properties of the system.

We  will determine the viscosity of 70% glycerol solution by observing and tracking the motion of bead particles 
measuring 4.22 micrometers in diameter using video microscopy. The recorded 
movements of the bead particles will be  enhanced through optimization techniques such as 
tracking, filtering, and linking in ImageJ software, with specific parameters tailored to the 
analysis. We  will collect three different videos with different number (16, 19, & 23) of tracks for 
analysis. The trajectories of particles will be graphically analyzed using python software tools. 
Plot of MSD as a function of time allows us to determine the diffusivity constant, from which 
the viscosity of 70% glycerol solution will be estimated using Stoke Einstein’s relation.

# Physics used for the project
Video Particle tracking analysis to estimate the viscosity of glycerol solution is based on the diffusive motion of bead particles in the glycerol solution. Trajectories of bead particles are observed and analyzed based on various techniques; The movement of the center of mass of bead particles are determined by calculating the position vector R at each time interval based on the velocities of the individual particles[^3].
<img width="783" alt="Equation_1" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/9c3255bb-a74b-4d06-b41a-d7aca3046605">
Where $R_0$ is the initial center of mass vector calculated by averaging the coordinates of all the beads in the first frame (k = 1),
$v\_k$ is the mean velocity of all the particles in frame k, 
$v_{i,k}$ is the velocity of particle in frame k in units of μm/frame,
and $N_k$ is the number of particles in frame k and ∆k is the frame difference.


Calculation of ensemble average and time average of the mean square displacement of beads
as a function of lag time is based on equation 2[^2],[^3].
<img width="826" alt="Equation_2" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/2106d9c8-f514-42b0-8270-2150c150b298">
where x(t) and y(t) are the coordinates of the bead at time t, and ∆t is the time interval also called lag time. Further to extract the diffusion coefficient of the beads MSD plot is fitted using equation 3[4].
<img width="1020" alt="Equation_3" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/288d79cf-cd75-4af7-a2af-1a4c7ba37bbb">
where $\tau$ is the lag time, D is the diffusion coefficient and $\alpha$ known as diffusivity exponent gives the nature of diffusion, $\alpha = 1$ represents normal diffusion,and N is the noise factor.
Using the value of diffusion coefficient estimated by fitting the MSD plot, viscosity η can be evaluated from Stokes Einstein relation given by equation 4[^4],[^5].
<img width="893" alt="Equation_4" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/9f93f44b-6768-4bd9-b894-3f88084cad04">

Where R is the particle radius, $k_B$ is the Boltzmann coefficient, and T is the temperature in Kelvin.
# Sample Preparation

Sample was prepared by adding 1μl of buffer solution formed by adding equal amount of Nacl, DTT and Mops.  0.5μl of 1000X diluted beads of size 0.2μm are added to the solution. To form condensates single stranded DNA molecules of 90 nucleotides chain of volume 0.80μl is added to the buffer and bead solution, on which RGRGG_5 polypeptides of volume 0.63μl is added to it. Finally 2.07μl of water is added and all the solution is mixed well. The solution prepared is transfered to cover slip covered with glass slide with three layer of spacer inorder to prevent sample from wetting the glass surface. Further mineral oil is added to it so that the sample won't evaporate. 
The sample is then observed under epifluorescence microscope under 100X objective lens with immesrsion oil and the motion of beads particles are tracked. I tracked 972 frames for 100s and these tracked particles are further filtered using the trackmate tools of ImageJ.
# Tracking and Filtering using ImageJ
The image scale is set to 0.0688μm per pixel. A Difference of Gaussian (DoG)
detector with a 0.4μm object diameter and a quality threshold of 2 is applied
to identify local maxima as detection spots. These spots are filtered based
on quality and proximity, with a signal to noise ratio threshold. A median
filter is used to mitigate extreme pixel intensities while retaining image details.
Particle-linking consists of two stages; link particles to form track segments
between frames, then closing gaps between segments[^6]. Finally, the trajectory
data is saved in an XML format for further analysis using Python tools.
# Results And Discussion
Condensates which are formed by liquid liquid phase seperation of multivalent proteins in association of nucleic acid shows viscous nature. To analyze the viscosity of these condensates we employ video particle method and tracked the motion of bead particles in the condensates. The bead particles exhibit brownian motion and on plotting the mean square displacemnt as a function of lag time and fitting the msd plot we can estimate the viscosity value of the condensates taken for study. First we observe the trajectories of the bead particles tracked which cleary shows random brownian motion.

![T90-RG5 PK_1_MMStack_Pos0_Tracks_1individual track](https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/4486120b-3c8f-4b15-ada8-148a317caddb)

Further we observe the trajectories from X and Y com of central of mass vector of the tracked bead particles. These plots are used to demonstrate how the motion of bead particles can captured by increasing frame. It involves locating the central of brightness of bead particles in a frame and the process is repeated for successive frame. By doing so the particles in one frame can be tracked in successive frame with the position coordinates indicaticating the central of mass vector of the bead in successive frame. The two plots gives the trajectory for X component and Y component of central of mass vector for bead plotted with increasing frame.

![T90-RG5 PK_1_MMStack_Pos0_Tracks_1Xcom](https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/81e16ec4-4d28-4a3c-8865-aac762afd392)![T90-RG5 PK_1_MMStack_Pos0_Tracks_1Ycom](https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/7465ff2e-c8fd-476e-a503-3beef7bf45c2)

The trajectories for all the bead particles tracked are given by the plot below:

![T90-RG5 PK_1_MMStack_Pos0_Tracks_1tracks](https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/5f5bf535-8057-4bf9-bfb2-0838e124a8a5)

Mean Square displacement calculated from the position of bead particles at different time interval is used to analyze the motion of bead particles and to calculate the diffusion coefficient values. The MSD plot for all the tracked beats shows linear nature which shows that the motion of the bead particles is brownian. Further the fitted plot of MSD as a function of lag time gives the value of diffusion coefficient and diffusibility constant value. We observe that the value of diffusion coefficient is found to be 

# References
[^1]: [J. A. McGlynn, N. Wu, and K. M. Schultz, Journal of Applied Physics 127, 201101 (2020)] (https://pubs.aip.org/aip/jap/article- pdf/doi/10.1063/5.0006122/15245133/201101 1 online.pdf .)
[^2]: [D. Frenkel and B. Smit,Understanding Molecular Simulation, Vol. 1 (Elsevier Science Technology, United States, 2001).]
[^3]: [H. Qian, M. P. Sheetz, and E. L. Elson, Biophys. J. 60, 910 (1991).]
[^4]: [I. Alshareedah, G. M. Thurston, and P. R. Banerjee, Biophys. J. 120, 1161
(2021).]
[^5]: [I. Alshareedah, T. Kaur, and P. R. Banerjee, in Methods in Enzymology, Methods in enzymology (Elsevier, 2021) pp. 143–183.
[^6]:[J.-Y. Tinevez, N. Perry, J. Schindelin, G. M. Hoopes, G. D. Reynolds, E. La-
plantine, S. Y. Bednarek, S. L. Shorte, and K. W. Eliceiri, Methods 115, 80
(2017).]






