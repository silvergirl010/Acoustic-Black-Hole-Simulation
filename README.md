# Fluid Dynamic Analogue of a Black Hole (Acoustic Black Hole)

## Project Overview
As a Mechanical Engineering student, I realized that the core principles of fluid mechanics and classical thermodynamics share beautiful mathematical dualities with general relativity and quantum field theory. This project is an interactive Python simulation of an **Acoustic Black Hole (Sonic Black Hole)** inside a converging nozzle, demonstrating how fluid dynamics can model a gravitational event horizon.

## The Physics & Engineering Concept
In a fluid medium, sound waves (phonons) propagate at a characteristic speed of sound ($c_s$). If the fluid itself accelerates and exceeds the speed of sound ($Mach > 1$), a **Sonic Event Horizon** is formed. 

According to the continuity equation for an incompressible fluid:
$$v(x) = \frac{Q}{A(x)}$$

Where:
* $Q$ is the constant volumetric flow rate.
* $A(x)$ is the cross-sectional area of the nozzle, which decreases along the axial position $x$.

The kinematic equation governing a sound wave attempting to propagate upstream (against the fluid flow) is:
$$\frac{dx}{dt} = v(x) - c_s$$

* **Subsonic Region ($v < c_s$):** The wave's propagation speed is greater than the fluid's velocity, allowing it to escape upstream ($x \to 0$).
* **Event Horizon ($v = c_s$):** The fluid velocity perfectly matches the speed of sound. The wave becomes frozen at this boundary.
* **Supersonic Region ($v > c_s$):** The fluid moves faster than the speed of sound. Even though the wave propagates backward, it is dragged downstream by the powerful fluid current ($x \to \infty$).
