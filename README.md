Vehicle Parameters
The vehicle's physical characteristics and hydrodynamic properties are defined at the beginning of the code. These parameters are critical for accurately modeling how the vehicle interacts with its environment (water) and how it responds to control inputs.
--------------------------------------
Fluid Density (rho): The density of the water surrounding the AUV, which affects buoyancy and drag.
Reference Area (Af): The cross-sectional area of the vehicle, used in drag calculations.
Buoyancy (B) and Weight (W): The forces acting on the vehicle due to its displacement in water and its mass, respectively.
Moments of Inertia (Ix, Iy, Iz): These describe how the vehicle's mass is distributed around its center of gravity, affecting its resistance to rotational motion.
Mass (m): Derived from the vehicle's weight (W), this is used in calculating the vehicle's dynamics.
Center of Gravity (xG, yG, zG) and Center of Buoyancy (xB, yB, zB): These points are critical for calculating moments due to buoyancy and weight.
Hydrodynamic Coefficients (X_du, Y_dv, etc.): These coefficients describe how the vehicle interacts with the water, including drag forces and added mass effects (where water moving with the vehicle effectively increases its mass).
The AUV Function
The AUV function is the heart of the simulation, calculating the time derivatives of the vehicle's state variables based on its current state and control inputs.
----------------------------------------
Inputs:
states: A list containing the current state of the vehicle. The state variables include:
u, v, w: Linear velocities along the vehicle's x, y, and z axes, respectively.
p, q, r: Angular velocities (rates of rotation) around the x, y, and z axes, respectively.
phi, theta, psi: Euler angles representing the vehicle's orientation (roll, pitch, and yaw).
inputs: A list containing control inputs, typically:
dele_ac: Elevator deflection angle (affects pitch).
delr_ac: Rudder deflection angle (affects yaw).
Hydrodynamic Drag:
Drag Coefficient (Cd): This is computed based on the speed in the forward direction (u). The drag force opposes the vehicle's motion and is calculated as Xuau.
Inertia Matrix (M):
The inertia matrix represents how the vehicle's mass and distribution affect its motion. This matrix is a combination of the vehicle's mass, moments of inertia, and hydrodynamic coefficients. It's a critical part of the simulation as it links forces and moments to accelerations.
Forces and Moments (F1 to F6):
F1 to F6 represent the forces and moments acting on the vehicle in six degrees of freedom (3 linear and 3 rotational). These forces and moments are derived from:
Buoyancy and Weight: The gravitational force and buoyant force, which depend on the orientation and position of the vehicle.
Hydrodynamic Forces: Including drag, lift, and added mass effects, which depend on the vehicle's velocity and control inputs.
Control Inputs: The effects of rudder and elevator deflections on the vehicle's motion.
-------------------
Solving the Equations of Motion:
M_inv: The inverse of the inertia matrix, used to solve for the accelerations (S1) from the forces and moments.
x_dot, y_dot, z_dot: These represent the translational velocities of the vehicle in the global coordinate system, derived from the local velocities (u, v, w).
phi_dot, theta_dot, psi_dot: These represent the rates of change of the vehicle's orientation (roll, pitch, yaw), derived from the angular velocities (p, q, r).
Output (X_dot):
The function returns X_dot, a vector that contains the time derivatives of all the state variables. This output can be integrated over time to simulate the vehicle's motion.
Application
--------
The code is typically used in simulations where the goal is to predict the behavior of an AUV over time. For instance, in a control system, this function would be called repeatedly within a loop to update the state of the vehicle based on its current state and the control commands being issued. This is useful for tasks like path planning, navigation, and autonomous operation of the AUV in various underwater environments.

--------
In summary, this Python code models the complex interactions between an AUV and its environment, providing a way to simulate and predict the vehicle's behavior under different conditions. It's an essential tool for developing control systems, testing different scenarios, and ensuring the safe and efficient operation of AUVs in real-world missions.
