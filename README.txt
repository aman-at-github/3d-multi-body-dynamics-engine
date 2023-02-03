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
Tested to give accurate simulations with marginal deviations in conserved physical-quantities (Energy, Angular Momentum & Linear Momentum). 
Has flexible accuracy scalable at the expense of computation-time. 





The code has not been 'entirely' Revealed by This Author.
However, most of it is available publicly in the file which can be found in the following link : 
      https://github.com/aman-at-github/computer-algebra-system/blob/main/Equationsimplifier2.java
( In the above file, Java-code which is not meant to be revealed has been replaced by "Implementation Not Revealed By Author" )
Following are the Java-classes in this file which contain code more relevant to Multi-Body-Dynamics rather than Computer-Algebra-System : 
      [ MultiBody , Joint_Revolute , Joint , Body , Vector ] 






Links to Animations of some Test-Cases can be found on the main page of this repo : 

    https://www.youtube.com/playlist?list=PLMM3_WmWWwm2HzsFkoO0Uy-5TkCb16fO1


An important thing to notice in these above simulated Test-Cases when compared to other commonly available Multi-Body-Simulations (or examples) on media (say Youtube), is that elsewhere such a free-space simulation is nowhere to be found.

The multi-body examples and simulations found elsewhere always seem to have atleast one of the objects/bodies connected to the ground or wall (ie they do not give a true free-space simulation which is more sophisticated to make).

This limitation does not apply to this Physics Engine, and being free from this limitation was very much intentional.
    Though the gravitational case has not yet been implemented, it can be done without any complications involved to make it happen.
    The Zero-Gravity case is more Generic and more difficult to implement.





Major Sub-Components : 
    (of the code implementing Multi-Body Simulator) 

    Determining if the body contains cyclical connections.
        Then intelligently decides the hinges for which Parametric-Method is to be used (faster but does not support cyclical connections).
        For other hinges which 'complete' a cylical-connection, the method of Constraint-Equations is used (relatively longer but allows existence of cyclical connections).

    Synthesize Equations of Multi-Body in Newtonian-Mechanics.
        (Used to 'Normalize' velocities of Bodies in Initial-Configuration, in case their velocities are not consistent at the hinges)
	(Eg- Two bodies connected may have initial-velocities such that they move in opposite directions as if they are not connected, this is not practically possible since they are connected via a hinge, their velocities have to be appropriately re-normalized)
        Rendering time of Newtonian Mechanics has been found to be much longer hence it is only used for re-normalization of velocities.

    Synthesize Equations of Multi-Body in Langrangian Mechanics.
    
    Determine the solving-variables of Langrangian-Equations.
        This is done in a dynamic manner and eliminates redundant solving-variables, thus speeding up the simulation.

    Determining the Higher-Derivatives of Multi-Body Equations.

    Determining an ideal value of Time-Step for the instantaneous configuration of bodies.
        This speeds up simulation-process in accordance to a specified-standard for accuracy.

    Solving the System of Equations.
        The System of Equations can be 'Over-Determined' (but consistent) so requires some additional processing before solving them linearly.
        This process was intelligently optimized, otherwise it could be time-intensive.




Other Minor Components (Blender & Python) : 

    Creation of Input-Configuration.
        (This includes specifications concerning Moment-Of-Inertia & Velocities of each of the bodies, and the placement of hinges in the multi-body)
        At present only cuboid objects of any specified mass are supported.
        This limitation is only on the Input-Side ie Blender, however the Simulation-Engine (Java Program) supports bodies of any shape, size or mass.

    Reading and Displaying Animation of the Simulation generated by the Simulation-Engine.






APPLICATIONS : 

	Anywhere that requires simulation or prediction of some mechanical system.
	
	If the precise specifications of any Robotic-System is known, then this program can precisely determine how the Robotic-System would move when certain actions are performed by it.
	
	Thus knowing the results of any set of actions, the Robotic-System can better judge what action would be better for a certain goal.
	    This is considerably more intelligent than a trial-and-error method (where many unssuccessful attempts may be made until a task is achieved).
	
	This essentially means making available the power-of-precognition (to a certain degree) to the AI which may be controlling the Robotic-System, to take more intelligent decisions.
	    Perhaps the only scenarios, where such precognition could fail would be, when there is an external interfernce involved which has not been considered (or cannot be considered if its too complex).






Why was Multi-Body Dynamics chosen for this project ?

Consider some of the disciplines of Dynamics (from Mechanics) such as Aerodynamics, Fluid-dynamics, Soft-Body Mechanics, Multi-Body Dynamics.
Among these the most difficult and sophisticated to implement is Multi-Body Dynamics. 
Moreover Soft-Body Dynamics (different from Soft-Body Animation) can be implemented as a special case of Multi-Body Dynamics.
    This can be done by having a single Soft-Body being comprised of multiple-interconnected rigid-bodies.
Also, in Multi-Body Dynamics, the increase in complexity with the increase in number of bodies is non-linear and greater as compared to Aerodynamics & Fluid-Dynamics.
    This is because the interaction between two bodies in Multi-Body Dynamics is more complex than interaction between two particles in Aerodynamics or Fluid-Dynamics.
    Moreover each body/particle in Aerodynamics or Fluid-Dynamics is independent and do not form a chain of complex connections as seen in Multi-Body Dynamics (here any configuration of complex-connections are allowed).

Simulators for Aerodynamics & Fluid Dynamics have been around since long before Multi-Body Dynamics Simulators.
Implementing Multi-Body Dynamics is the biggest impediment in making a truly General-Purpose Motion-Simulator/Predictor, which is why it was chosen for this project in particular.





Yet To Implement : 
    (Alhough the following have not been implemented, these do not pose a major impediment in terms of complexity)

    Two other Fundamental Hinges which are Ball-Socket-Joint & Prismatic-Joint.
    Friction within Hinges/Joints.
    Bodies with Infinite mass.
    Hybrid/Composite Joints/Hinges (these have properties of atleast two of the fundamental joints, eg- Prismatic-Ball-Socket, Prismatic-Revolute, Universal-Joint (ie. Double-Revolute), Planar-Joint, etc.)
    Some advanced-hinges such as Screw-Joint, Gear-Coupling among bodies.
    Spring effect in hinges.
    Pulleys, Gears, Ropes.
    Gravity and Collision among the Bodies.
    Creatiion of bodies with abstract shapes and moment-of-inertia.
    Simplifying the equations used in rendering the animation (this shall significantly improve the rendering-time).
    Optimization of code used in Multi-Body Dynamics to reduce rendering time.





ADDITIONAL NOTES : 

    Langrange's Equations of First Kind is used to synthesize Equations-Of-Motion. 
    The constraint-equations, for which 'a corresponding Langrange-Multiplier 'Y_i' is determined', is based on the kind of hinges used in the Input-Configuration which constrains the relative motion of the connected bodies.
    The higher derivatives of the Equations-Of-Motion are calculated, upto derivative order 'N'.
    As the value set for 'N' is increased, the accuracy of the simulation also increases but at the expense of computation time as well as memory-space.
    The time to synthesize these equations indicates the Static-conterpart within the total computation time.
    From these differential equations, the position of the bodies after a small-time-interval 't' is determined using Taylor's Theorem.
    This process is iterated as many times as the total-time for which the simulation is to be generated.
    The time taken to do this denotes the Variable-conterpart within the total computation time to render the simulation.
    The value of 't' is determined dynamically since an ideal value of 't' changes with time and is typically inversely-proportional to velocities of the bodies.
    (If the values velocities of bodies is large then a smaller value of 't' is an ideal)
    Calculation of 't' is based on Maximum-Desirable-Error in Velocity or Momentum at every time-step-iteration.
    An acceptable value for the above is currently hardcoded in the program, it cannot be changed after execution begins.
    Increasing this value decreases the execution-time but at the expense of accuracy of the simulation. (The decrease in accuracy shows up as deviation in conserved Physical Quantities like Energy and Linear & Angular Momentum).
    Decreasing this value can lead to an unnecessary increase in execution-time with only marginal increase in accuracy (since the simulation may already be quite accurate).
    

    Typically the instantaneous values of higher derivatives of the velocities (linear, angular or parametric) tend to increase as the order-of-derivative increases 
    But for small time-intervals their weightage in taylor-theorem tends to decrease since the value of their coefficient decreases even further. 
    The coefficient for derivative-order 'N' is of the type  "( t ^ N / factorial( N ) )" 
    
    Comments on Langrange's Equations of First Kind : 
    
    These are of the form - 
        d/d(pos)_( L )  =  d/dt( d/d(vel)_( L ) ) 
        where,  L  =  K.E.  +  $SUM_i( Y_i * F_i(pos) ) 
            here, 'F_i(pos)' is the i'th constraint-equation which must not contain any derivatives of position and orientation variables such as velocity or acceleration . 
            and 'Y_i' is an undetermined Langrange-multiplier corresponding to 'F_i(pos)' . 
    
    /// 
    /// 
    The constraint-equations "( F_i(pos) == 0 )" are the additional solving-equations to make up for the additional solving variables 'Y_i' . 
    Also, 'Y_i' is not a constant across time, and 'd/dt( Y_i )' is not to be assumed as 'zero' for higher derivatives of Langrange's Equations . 
    /// 
    
    Practically, it can often happen that all the constraint-equations represented by "( F_i(pos) == 0 )" are not linearly-independent . 
    Only a sub-set of these constraint-equations may be linearly-independent, and only those must be considered in Langrange's Equations . 
    Moreover the subset of constraint-equations, which are linearly-independent, can change with time . 
    To deal with this we set 'Y_i' and all its higher-derivatives to value 'zero' for those 'i' which correspond to constraint-equations which are redundant cause they are not linearly-independent wrt the others at that instance of time . 
    This is so because...
        For 'Y_i' corresponding to redundant constraint-equations,
        consider the time-derivative of "( Y_i * F_i(pos) )"  which is equal to  "(  ( d/dt(Y_i) * F_i(pos) )  +  ( Y_i * d/dt( F_i(pos) ) )  )" . 
            ie,  d/dt( Y_i * F_i(pos) )  =  (  ( d/dt(Y_i) * F_i(pos) )  +  ( Y_i * d/dt( F_i(pos) ) )  ) 
            here, the second-term of RHS ie "( Y_i * d/dt( F_i(pos) ) )" is 'zero' because 'Y_i' is to be set to 'zero' . 
            now, consider the first-term of RHS ie "( d/dt(Y_i) * F_i(pos) )" , 
                here 'F_i(pos)' is the coefficient corresponding to the solving-variable (of that derivative-order) 'd/dt(Y_i)' . 
                coefficient 'F_i(pos)' makes-up for redundancy because this is the same coefficient which made the solving-variable 'Y_i' as redundant in previous derivative-order . 
                This is so because we see that the coefficient of the solving-variables 'Y_i' or its derivatives, is the same across all derivative-orders ie 'F_i(pos)' . 
                Thus the constraint-equations which were redundant in the zero'th derivative-order, remain redundant for all higher derivative-orders . 
                To make up for this we set 'Y_i' and all its higher-derivatives to value 'zero' for all 'Y_i' which correspond to redundant constraint-equations, ie those equations which do not contribute to linear-independence . 
                Also, if "( F_i(pos) == 0 )" corresponds to a redundant constraint-equation, then its derivative is also a redundant equation among the higher-derivatives of constraint-equations, so we set all derivatives of 'Y_i' to value 'zero' . 
    
    To determine redundant equations, we consider the intermediate-equations of position, orientation, moment-of-inertia, along with the constraint-equations "( F_i(pos) == 0 )" . 
    Here the variables , wrt which linear-independence is to be tested for, are '[R_cm]' & '[Eu_xyz]' for independent-bodies, parametric-variables of postion for dependent-bodies, and all the intermediate-variables such as position, orientation, moment-of-inertia , whichever are relevant . 
    
    
    /// 
    
    
    Important Note - 
    In case of compounding of error over time, an 'Inequality'-of-sorts is seen in constraint-equations 
        For example, the 'world-position-of-joint' or 'world-orientation-of-joint-axis' may not be exactly equal when calculated from one body as compared to the other 
        Equality of 'world-position-of-joint' or 'world-orientation-of-joint-axis' as calculated from one body as compared to the other, are 'constraint-equations' 
    To reduce the rate-of-compounding of error, the 'joint-position-wrt-centre-of-mass-in-body-frame' and 'joint-axis-orientation-in-body-frame' should be renomarmalized at regular intervals such that the inequality seen in constraint-equations is minimised 
    
    
    
    Instead of constraint-equations in cyclical case, considering parametric-variables of the joint completing a cyclical connection leads to 
        an additional unique definition of Orientation-and-Centre-of-Mass for the secondary-body of that joint, besides the one it already has.
        This in turn leads to atleast two unique definitions for partial derivatives of Orientation-and-Centre-of-Mass.
        When the partial-derivative ( d/d( POS|VEL )_( ORI|CM ) ) wrt some parametric-variables is zero in one of the definitions but non-zero according 
        to another definition (since there is an additional one due to the joint completing cyclical connection), then then non-zero is considered ,
        and the one which is zero is entirely ignored. 
        However, if the partial-derivative is non-zero wrt a certain parametric-variable for both the unique definitions, then any one of them is considered 
        and the other is entirely ignored. 
        In this case, the values of the partial derivatives would probably mismatch (NOT CONFIRMED) for the two unique definitions.
        This seems to result in an inconsistent/conflicting system of linear-equations (Langrange-Equations), ie they do not have a solution-set,
        ie they do not have a unique intersection. 
        When these equations are tried to solve by eliminating one of the redundant equations and a variable, then the parametric-variable of the 
        cyclical-joint is eliminated. Thus the parametric variable completing the cyclical connection is entirely ignored thereby completely ignoring the 
        joint which completes the cyclical connection, and the simulation moves as if there is no joint forming cyclical connection.
        This seems to occur because the equation '( d/dt( d/d(VEL)_( KE ) )  ==  d/d(POS)_( KE ) )' does not incorporate the constraint of cyclical joint. 
    
    Elaborating on the above 
        The derivatives of a Langragian-Equation corresponding to a particular parametric-variable encode how the parametric-variable would change over time.
        So if no explicit consraint-equations are put in the Langrangian-Equations, then that particular equation would only encode how that 
            parametric-variable would evaluate over time without any constraints (ie the cyclical-joint constraining the bodies is ignored).
        Thus Langrangian-Equations of Second-Kind are equations where the parametric-variables are completely independent of one another.
        However in the cyclical-case the parametric variables are not completely-independent of one another.
        Thus the cyclical case cannot be simulated purely by Langrange-Equations of Second-Kind. 
        Langrange-Equations of Second-Kind are ones without explicit constraint-equations and corresponding parametric-variables. 
    
    
    As for using parametric equations as constraint-equations, they already are so indirectly, if parametric methodology is used in langrangian-equations, 
        even if the explicit constraint equations are not in parametric form. 
        This is beacause the intermediate equations are in parametric form, and the calculated values from these are used in solving constraint equations 
        for that particular time-step-iteration. 
        
        
