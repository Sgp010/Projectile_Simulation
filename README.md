#PROJECTILE MOTION SIMULATOR
1. The question that started the simulator-
The goal was not to memorize the standard projectile-motion equations. The goal was to predict where an object would be after some amount of time using only basic physics that was already understood: vectors, gravity, velocity, and simple algebra.

The first useful question was therefore: “What is gravity actually doing to the object’s velocity?”
Important distinction
Gravity is not “adding downward distance.” Gravity changes the object’s velocity. That change in velocity accumulates as time passes.

2. Start by separating the motion into components
Treat the launch velocity as a vector. Resolve it into horizontal and vertical components using the launch angle. For a launch speed v at angle θ:
vₓ = v cos θ        and        vᵧ = v sin θ
This immediately gives two different stories for the same projectile: horizontal motion and vertical motion.

3. The key discovery: interpret g·t instead of memorizing i
A useful conceptual breakthrough was looking at the term g·t by itself. The first instinct might be “the effect of gravity increases with time.” A more precise interpretation is: gravity provides the same acceleration every second, and the changes in velocity accumulate over the elapsed time.

Δvᵧ = -g t

Because acceleration has units of m/s², multiplying by time gives m/s — the units of a velocity change. Therefore the vertical velocity after time t is:

vᵧ(t) = vᵧ₀ - g t

Read equations as sentences
The term g·t is the total change in vertical velocity caused by gravity over t seconds. The equation says: current vertical velocity = initial vertical velocity − accumulated gravitational change.

4. Getting vertical position without simply using the textbook formula
This was the clever part of the original reasoning. Instead of immediately recalling the displacement equation, reason about the velocity over the whole interval.
At the beginning of the interval, the vertical velocity is vᵧ₀. At the end, it is vᵧ₀ − gt. Because the acceleration is constant, the velocity changes uniformly, so the average vertical velocity over that interval is the average of the starting and ending velocities:

vᵧ,avg = [vᵧ₀ + (vᵧ₀ - g t)] / 2

Then use the basic idea that displacement equals average velocity multiplied by time:

Δy = vᵧ,avg · t

Substituting the average velocity and simplifying gives:

Δy = vᵧ₀ t - ½ g t²

What was actually derived
The standard kinematic displacement equation was not memorized. It emerged naturally from (1) how gravity changes velocity, (2) average velocity, and (3) distance = average velocity × time.

5. Finding the apex by reasoning, not hunting for a formula
At the apex, the vertical velocity is zero. That fact provides the condition needed to locate the top of the trajectory.

vᵧ = 0

Combine that condition with the vertical-velocity relationship. This gives the time at which the projectile reaches maximum height. The same style of reasoning can be reused whenever an unknown time can be identified by a physically meaningful condition.

6. The horizontal component is intentionally simpler
In ideal projectile motion with no air resistance, there is no horizontal acceleration. Therefore horizontal velocity does not change.

vₓ = constant

So horizontal displacement is simply the horizontal velocity accumulated over the time interval:

Δx = vₓ t

This is why the vertical component required the deeper reasoning while the horizontal component did not.

7. From equations to a simulation
The most important computational insight is that a simulator does not need to know the entire trajectory in advance. It only needs to determine what happens during the next small interval of time, then repeat.
State → physics → update
At every tiny step, the simulator knows the current position and velocity, computes the acceleration from the physical rules, updates the velocity, and then updates the position.

Conceptually:
current state
    ↓
calculate acceleration
    ↓
change velocity a little
    ↓
move using the updated velocity
    ↓
repeat

This is the computational version of the same reasoning used above. Making the time step smaller makes each straight-line approximation cover less of the curved path, so the numerical path approaches the continuous trajectory.

9. A practical build sequence
Build the ideal case first: Gravity only. No air resistance, no bouncing, no wind.
Resolve the launch velocity: Use the angle to obtain horizontal and vertical components.
Update vertical velocity: Let gravity accumulate a change in vᵧ over time.
Update position: Use the current velocity to advance the position.
Plot the trajectory: Record successive positions and connect them.
Check a known case: Compare the simulation with a simple textbook case to detect sign or timestep errors.
Only then add complexity: Air resistance, wind, collisions, and other forces should each be added as separate models.

10. Common traps this approach avoids
Formula-first thinking — Starting from a memorized equation can hide why the terms are there. Rebuilding the equation from the physics makes it easier to adapt the model.
Mixing quantities with different units — Acceleration cannot be added directly to velocity. Acceleration must act over time first, producing a velocity change.
Trying to find the entire path at once — A simulation can instead predict the next small state and iterate.
Treating every complication as one giant equation — Separate physical effects—gravity, drag, collision response—can be modeled independently and combined later.
Confusing numerical error with bad physics — A correct physical model can still look wrong when the time step is too large.

12. Extensions that are left unfinished
The original exploration naturally ran into harder topics:
Air resistance — Drag depends on the object’s velocity relative to the air. A realistic model also involves air density, cross-sectional area, and drag coefficient.
Wind — The relevant speed is the projectile’s velocity relative to the moving air, not simply its ground velocity.
Bouncing — A collision changes the velocity abruptly. Elasticity and ground friction are separate effects and should not be lumped into one “energy loss” constant.
Orbital mechanics — Once gravity is allowed to point in changing directions, the same update philosophy can generate an orbit instead of a parabola.
