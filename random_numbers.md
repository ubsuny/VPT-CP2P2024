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
# Use of Tensorflow 
Tensor flow is the open source machine learning framework used designed to simplify the process of building, training, and deploying machine learning models, particularly deep learning models. It allows users to define and execute computational graphs easily, automatic differentation, helps users visualize and monitor the training process, model architecture, and performance metrics. Although the datas obtained for video particle tracking are computed by using numpy library, tensor flow is used to estimate the mean square displacement of bead particles to see the effectiveness of the tensorflow for my project.

Here is the code that calculates the Mean Squared Displacement (MSD) of particles based on their positions (xpos and ypos) over time, using NumPy for efficient numerical computations.

```python
import numpy as np

# Define a function to calculate the Mean Squared Displacement (MSD) using NumPy
def calculate_msd_numpy(xpos, ypos, frametime, minframe):
    # Initialize an empty list to store MSD values (not used in this function, so could be removed)
    msds = []

    # Calculate the total number of data points
    nData = len(xpos)

    # Determine the number of delta T intervals for which MSD will be calculated, usually half the data length
    numberOfdeltaT = int(nData / 2)

    # Initialize a zero array to store the time intervals and corresponding MSD values
    msd = np.zeros((numberOfdeltaT, 2))

    # Loop over all delta T intervals to calculate MSD for each
    for dt in range(1, numberOfdeltaT + 1):
        # Calculate the difference in x and y positions for particles separated by time interval dt
        deltax = xpos[dt:nData] - xpos[:nData - dt]
        deltay = ypos[dt:nData] - ypos[:nData - dt]

        # Calculate the squared displacement for each pair of points
        sD = deltax**2 + deltay**2

        # Store the current time interval in the first column
        msd[dt-1, 0] = frametime * dt

        # Calculate and store the mean squared displacement for the current time interval in the second column
        msd[dt-1, 1] = np.mean(sD)

    # Return the time intervals and their corresponding MSD values
    return msd[:, 0], msd[:, 1]
```
Futher code implementing TensorFlow operations to efficiently calculate the Mean Squared Displacement (MSD) for a set of particle positions over time, leveraging TensorFlow's computational graph and automatic differentiation capabilities is given below:
```python
import tensorflow as tf

# Assuming xpos and ypos are lists or arrays containing the x and y positions over time
# Convert xpos and ypos to TensorFlow constants to be used in the TensorFlow graph
xpos_tf = tf.constant(xpos, dtype=tf.float32)
ypos_tf = tf.constant(ypos, dtype=tf.float32)

# Define a function to calculate MSD using TensorFlow operations
def calculate_msd_tensorflow(xpos, ypos, frametime, minframe):
    # Get the total number of data points
    nData = tf.size(xpos)
    # Calculate the number of time intervals for MSD calculation, half the number of data points
    numberOfdeltaT = tf.cast(nData / 2, tf.int32)
    # Create a TensorArray to store the MSD calculations for each time interval
    msd = tf.TensorArray(dtype=tf.float32, size=numberOfdeltaT, dynamic_size=False)

    # Define a sub-function to compute squared displacement for each time interval
    def compute_displacement(delta_t, msd):
        # Calculate the difference in positions for the given time interval
        deltax = xpos[1 + delta_t:nData - 1] - xpos[1:nData - 1 - delta_t]
        deltay = ypos[1 + delta_t:nData - 1] - ypos[1:nData - 1 - delta_t]
        # Square the differences to get squared displacement
        squared_displacement = tf.square(deltax) + tf.square(deltay)
        # Average the squared displacement to get the mean squared displacement
        mean_squared_displacement = tf.reduce_mean(squared_displacement)
        # Store the mean squared displacement in the TensorArray
        msd = msd.write(delta_t-1, (frametime * tf.cast(delta_t, tf.float32), mean_squared_displacement))
        # Move to the next time interval
        return delta_t + 1, msd

    # Execute the while_loop to fill the TensorArray with MSD values for each time interval
    _, msd_final = tf.while_loop(
        cond=lambda delta_t, _: delta_t <= numberOfdeltaT,
        body=compute_displacement,
        loop_vars=(tf.constant(1), msd)
    )

    # Extract the results from the TensorArray and stack them into a single tensor
    msd_result = msd_final.stack()
    # Return the final tensor of MSD values
    return msd_result

# Use the function to calculate MSD
msd_tf = calculate_msd_tensorflow(xpos_tf, ypos_tf, frametime, minframe)
# Convert the TensorFlow tensor back to a NumPy array for further analysis or usage
msd_tf = msd_tf.numpy()
```
The code above using NumPy and TensorFlow serve the same purpose of calculating the Mean Squared Displacement (MSD) for a set of particle positions over time. However, they differ significantly in terms of implementation and underlying execution. The TensorFlow code adds several steps and concepts specific to TensorFlow's execution model, such as converting data to TensorFlow constants, using TensorFlow operations, creating a TensorArray for dynamic storage, and leveraging TensorFlow's computational graph for efficient computation and GPU/TPU acceleration.
Further to compare the execution times of the NumPy and TensorFlow versions of the MSD calculation and also to evaluate the differences between their outputs to ensure consistency and accuracy, following code is implemented.
```python
import time

# NumPy version comparison
start_time = time.time()
time_np, msd_np = calculate_msd_numpy(xpos, ypos, frametime, minframe)
numpy_duration = time.time() - start_time
print(f"NumPy version took {numpy_duration:.4f} seconds.")

# TensorFlow version comparison
# Ensure xpos_tf and ypos_tf are TensorFlow tensors
start_time = time.time()
msd_tf = calculate_msd_tensorflow(xpos_tf, ypos_tf, frametime, minframe)
msd_tf = msd_tf.numpy()  # Convert the result back to a NumPy array for comparison
tensorflow_duration = time.time() - start_time
print(f"TensorFlow version took {tensorflow_duration:.4f} seconds.")

# Comparing outputs
# Assuming the first column is time and the second is MSD in both outputs
differences = np.abs(msd_np - msd_tf[:, 1])  # Comparing MSD values directly
print(f"Maximum difference between NumPy and TensorFlow MSD outputs: {np.max(differences)}")
```
It is observed that the NumPy version took 0.0437 seconds, TensorFlow version took 2.3097 seconds.
Maximum difference between NumPy and TensorFlow MSD outputs is 0.001569176552128515.








