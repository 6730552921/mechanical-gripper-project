# Simulation

Include model files and scripts with solver settings, assumptions, boundary conditions, material properties, and instructions for reproducing results. Identify the software and version used.

## 1. Software & Environment

* **Software:** MATLAB R2026b
* **Required Toolboxes:**
  * Symbolic Math Toolbox
  * Simulink
  * Simscape & Simscape Multibody

<img width="948" height="707" alt="Screenshot 2026-10-11 234406" src="https://github.com/user-attachments/assets/830bb203-94c3-4763-8e44-cb413e20b6e0" />

## 2. Model Parameters

| Parameter | Value |
|---|---|
| Link lengths | l₂ = 31 mm, l₃ = 22 mm, l₄ = 31 mm, l_g = 32.919 mm |
| Fixed pivot O₄ | (−8.25, 20.891) mm |
| Jaw tip offset angle | −6.6° |
| Input range | θ₁ = −20° to 90° |
| Input torque (symbolic model) | 0.01 N·m (10 N·mm) |

## 3. Assumptions

* Rigid links, no deformation
* Ideal revolute joints, no friction or backlash
* Ideal gear mesh between Gear left and Gear right
* Symmetric left and right linkage, so the right side represents the whole gripper
* No contact with an object (no gripping load)

## 4. Boundary Conditions & Solver Settings (Simulink)

* **Boundary conditions:** Base is fixed to the World Frame; the only input is the motor angle on the Gear right revolute joint
* **Input:** Sine wave → Saturation → Revolute joint (Gear right)
* **Gear transmission:** Common Gear Constraint (Gear right ↔ Gear left, opposite rotation)
* **Solver:** Auto
* **Step size:** Auto

## 5. How to Reproduce

1. Open MATLAB R2026b and set the working folder to this repository.
2. Run the symbolic script in `software/matlabs code` to get the position, velocity, acceleration and force plots.
3. Open the Simulink model (`gripper.slx`), check the World Frame and Solver Configuration, then press **Run**.
4. Compare the tip trajectory from Simulink with the symbolic result.

## 6. Known Limitations

* The Saturation block causes sharp velocity and acceleration spikes at the stroke limits.
* The Simulink plots use input angle on the x-axis, not time.
* Material properties and mass are not set in this model (add them if you need dynamic or force results).
