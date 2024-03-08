For the experiment using video particle tracking I have considered the motion of bead particles in glycerol soolution. Bead particles are used to track motion by using 
fluoescence microscope. Bead of size 1 micro meter are placed in 90 percent glycerol solution and their motion is observed by using microscope under 40X resolution. When 
the beads are allowed to move in glycerol solution their motion is tracked by using ImageJ software for everypixel up to 1000 pixel and their motion is recorded in terms of 
X and Y coordinates along with time elapsed. Here the motion of bead particles execute random/ Brownian motion and to simulate the random motion of bead particles,
we can use built-in functions to generate random numbers that represent the displacement of the particles in each time step. An example of  Python code demonstrating 
how we can generate random motion for the bead particles is shown below:
```python
import numpy as np
import matplotlib.pyplot as plt
def generate_random_displacement(sigma, num_steps):
"""
    Generate random motion for bead particles.

    Args:
        num_particles (int): Number of bead particles.
        num_steps (int): Number of time steps.
        sigma (float): Standard deviation of random displacement.

    Returns:
        tuple: Tuple containing X and Y coordinates for each particle over time.
    """
    return np.random.normal(scale=sigma, size=num_steps)

num_particles = 1  # Number of bead particles
num_steps = 1000  # Number of time steps
sigma = 1  # Standard deviation of random displacement

x_coordinates = np.zeros((num_particles, num_steps)) # Initialize arrays to store X and Y coordinates
y_coordinates = np.zeros((num_particles, num_steps))

for i in range(num_particles):
    x_displacements = generate_random_displacement(sigma, num_steps) # Generate random motion for each particle
    y_displacements = generate_random_displacement(sigma, num_steps)
    
    x_coordinates[i] = np.cumsum(x_displacements)  # Calculate X and Y coordinates
    y_coordinates[i] = np.cumsum(y_displacements)

print("X coordinates for the first few time steps:") # Print the first few coordinates for demonstration.
print(x_coordinates[:, :5])
print("Y coordinates for the first few time steps:")
print(y_coordinates[:, :5])
mu = 0  # Mean of the Gaussian distribution 
x = np.linspace(-5, 5, 1000)
plt.plot(x, 1/(sigma * np.sqrt(2 * np.pi)) * np.exp( - (x - mu)**2 / (2 * sigma**2) ), linewidth=2, color='r') 
plt.title('Plot of Random Displacements with Gaussian Curve') 
plt.xlabel('Displacement')
plt.ylabel('Probability Density')
plt.grid(True)
plt.show()

```
<img width="1078" alt="gaussian_curve" src="https://github.com/ubsuny/VPT-CP2P2024/assets/72980895/618350a4-c3d1-43d2-882b-87f68a7f5fda">

 
 In this code we uses numpy library to generate random numbers which follows a normal distribution with mean 0 and standard deviation sigma (given) for each time step. The function generate_random_displacement generates these random displacements, and the cumulative sum of these displacements gives the coordinates of the particles over time. In the context of simulating particle motion, each displacement value at a particular time step indicates how much the particle has moved from its previous position. Thus, cumulative sum (np.cumsum) is used to add up all the individual displacements encountered by the particle up to that time step.
The code is a basic example of how random motion can be simulated. Depending on the specifics of  experiment and the behavior of the particles, we need to adjust parameters and incorporate additional factors into our simulation for random motion.


