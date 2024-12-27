https://github.com/user-attachments/assets/68e5645b-6a8d-4acb-bc46-a7026b05421c


# Robot Localization Using Particle Filters

This project implements a **robot localization algorithm** using **particle filters**, a probabilistic approach to tracking the position and orientation of a robot in a 2D environment. The robot navigates within a predefined map, simulates noisy sensor readings, and continuously updates its belief about its position using particle filter-based estimation.

## **Overview**

Robot localization is a critical problem in robotics, where the robot needs to estimate its pose (**x**, **y**, and **θ**) within a given environment. This project uses **particle filters** to solve this problem, which is particularly suited for scenarios involving:
- Non-Gaussian noise.
- Complex, nonlinear motion and sensor models.
- Computational feasibility for real-time robotics applications.

The program simulates a robot navigating a 2D map and visualizes:
- The robot's true position.
- A cloud of particles representing hypotheses about the robot's position.
- The most likely position estimated from the particles.

---

## **Algorithm Details**

### 1. **Initialization**
The particle filter begins by initializing a **cloud of particles**:
- Each particle represents a possible robot pose \((x, y, θ)\).
- The particles are uniformly distributed across the map initially.

### 2. **Robot Movement**
The robot can move forward, backward, and rotate left or right, with each movement modeled as:
- **Translation**: The robot moves in the direction of its current heading.
- **Rotation**: The robot updates its orientation by a given angle.

Both translation and rotation are affected by **Gaussian noise**, simulating real-world uncertainty in movement.

### 3. **Particle Update**
When the robot moves, the particles are also moved according to the robot's control inputs (e.g., forward, backward, turn) with added noise. The particles' positions are clipped to ensure they stay within the map boundaries.

### 4. **Sensing and Weight Calculation**
The robot periodically takes a simulated **sensor reading**, which measures the intensity value from the map at its current location. Each particle computes an expected sensor reading based on its own position. A **weight** is assigned to each particle based on the error between the robot's sensor reading and the particle's expected value:
- Particles with smaller errors receive higher weights, representing higher likelihoods of the robot being at those positions.

### 5. **Resampling**
The particle cloud is resampled using **stochastic universal sampling**:
- Particles with higher weights are more likely to be selected, focusing the distribution on areas with higher likelihood.
- Low-weight particles are discarded.

### 6. **Adding Noise**
To maintain diversity in the particle set and prevent particle deprivation, **random noise** is periodically added to the particles after resampling. This step ensures robustness in tracking even with sensor or motion model inaccuracies.

### 7. **Visualization**
The robot's true position, particle cloud, and the estimated position (mean of the particle distribution) are displayed in a 2D graphical interface. The map dynamically resizes to fit the display window while maintaining aspect ratios.

---

## **Features**

- **Particle Filter Implementation**: Tracks the robot's pose using probabilistic estimation.
- **Dynamic Resizing**: Ensures the entire map is visible in the display window regardless of size.
- **Realistic Noise Models**:
  - Gaussian noise for motion and sensor readings.
  - Particle noise to simulate uncertainty in predictions.
- **User Controls**:
  - `W`: Move forward.
  - `S`: Move backward.
  - `A`: Rotate left.
  - `D`: Rotate right.
  - `Q`: Exit the simulation.
- **Visualization**:
  - Particles are drawn in blue, representing hypotheses about the robot's location.
  - The robot's true position is displayed in green.
  - The estimated position (mean of particles) is displayed in red.

---

## **Technical Details**

### **Environment**
- **Map**: A 2D grayscale image where pixel intensity represents terrain features (e.g., walls or open space).
- **Particles**: Each particle tracks \((x, y, θ)\), the robot's position and orientation in the map.
- **Robot Movement Model**:
  - **Translation**: \[
    x_t = x_{t-1} + (\text{step size} + \mathcal{N}(0, \sigma_\text{step})) \cdot \cos(θ_{t-1})
  \]
  - **Rotation**: \[
    θ_t = θ_{t-1} + (\text{turn angle} + \mathcal{N}(0, \sigma_\text{turn}))
  \]
- **Sensor Model**:
  - Measures the intensity value of the map at the robot's current position.
  - Adds Gaussian noise to simulate sensor uncertainty.

### **Key Algorithms**
1. **Particle Movement**:
   - Moves particles based on the robot's motion model.
   - Clips particles to the map boundaries.

2. **Weight Computation**:
   - Uses sensor readings to calculate the likelihood of each particle's pose.
   - Weights are scaled by cubing to increase sensitivity.

3. **Resampling**:
   - Resamples particles based on their weights using a probabilistic approach.

4. **Noise Addition**:
   - Adds random perturbations to particles after resampling to maintain diversity.

---

## **How to Run**

1. **Setup**:
   - Install required dependencies:
     ```
     pip install numpy opencv-python
     ```
   - Place a grayscale image (`map.png`) in the project directory.

2. **Run the Program**:



3. **Controls**:
- Use `W`, `A`, `S`, `D` to control the robot.
- Press `Q` to quit the simulation.

---

## **Applications**

- **Autonomous Navigation**:
- Particle filters are widely used in robotic navigation systems such as **SLAM** (Simultaneous Localization and Mapping).
- **Sensor Fusion**:
- Combines data from multiple noisy sensors to improve accuracy.
- **Real-World Robotics**:
- Examples include robot vacuums, drones, and self-driving cars.

---

## **License**
This project is for educational and research purposes only. Contributions to the codebase credit but with a twist from Coursera’s guided project on robotics and localization techniques.
