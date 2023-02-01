# 3d-multi-body-dynamics-engine



3D Multi-Body Dynamics Simulator 

Designed & implemented from scratch a in JAVA. 
(Uses only a singular external-library which provides solver for System-Of-Linear-Equation-Solver and Matrix SVD & Eigen-Value calculator.)

Blender (Computer-Graphics application) & PYTHON scripts are used to model Input-Configuration as desired by User. 
Input-Configuration is a mechanical-configuration consisting of multiple Rigid-Bodies (any shape, size, mass) connected-via certain Joints/Hinges. 
(At present frictionless Revolute-joint has been implemented. Ball-Socket joint, Prismatic-joint & joints-with-friction are yet to be implemented.)
Input-Configuration must include Velocities of the bodies (otherwise there would be no motion taking place). 

Python Scripts in Blender app make a JSON file which contains information of Input-Configuration.
This JSON file is used by the Java Program which renders the Simulation and outputs a JSON file containing the trajectory of bodies.
The Blender App reads this Output JSON file to show the animation/simulation.

The JAVA code (75,000+ lines) automates a vast & complex procedure which analyzes the input-file to synthesize the Equations-of-Motion in Langrangian-Mechanics. 
Then Solves the Equations in reasonable-time to render an accurate 'free-space' (zero-gravity) simulation. 
Has flexible accuracy scalable at the expense of computation-time.




