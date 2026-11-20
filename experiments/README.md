# Experiments

Organize experiment procedures, raw data, and results. Record the objective, setup, equipment, calibration status, conditions, units, date, operator, and analysis method. Preserve raw measurements and label processed results separately.

> **Note:** This project is simulation-based, so the experiments below are "virtual experiments" run in MATLAB.



## EXP-01: Symbolic Kinematics (MATLAB Symbolic Math Toolbox)

| Item | Detail |
|---|---|
| **Objective** | Find the position, velocity, acceleration, and gripping force of the gripper tip vs. input motor angle θ₁ |
| **Setup / Equipment** | MATLAB + Symbolic Math Toolbox |
| **Parameters** | l₂ = 31 mm, l₃ = 22 mm, l₄ = 31 mm, l_g = 32.919 mm, O₄ = (−8.25, 20.891) mm, offset = −6.6° |
| **Input range** | θ₁ = −20° to 90°, step 1° |
| **Input torque** | T_in = 0.01 N·m (10 N·mm) |
| **Units** | Position: mm, Velocity: mm/rad, Acceleration: mm/rad², Force: N, Angle: deg |
| **Calibration / Verification** | DOF check = 1 (3(7−1) − 2(8) − 1) |
| **Analysis method** | v = dG/dθ₁, a = d²G/dθ₁², F_grip = abs(T_in / v_gx) |
| **Operator** | Suphasan Rodphai, Suraphum Changlek |

**Raw data:** `raw/`
**Processed results:** `processed/` (plots and tables)

**Key findings**
- Fully open at θ₁ ≈ 2°–3°, fully closed at θ₁ = 90°
- Toggle effect (v_gx → 0) near θ₁ ≈ 2°–3°, so the force spikes there

## EXP-02: Simulink / Simscape Multibody Simulation

| Item | Detail |
|---|---|
| **Objective** | Check the gripper motion in a multibody model and compare the tip trajectory with EXP-01 |
| **Setup / Equipment** | MATLAB Simulink + Simscape Multibody |
| **Input** | Sine wave → Saturation block → Revolute joint (Gear right) |
| **Gear transmission** | Common Gear Constraint (Gear right ↔ Gear left) |
| **Measurement** | Tip frame on the right gripper jaw |
| **Units** | Velocity: m/s, Acceleration: m/s², Angle: deg |
| **Calibration / Verification** | Tip trajectory compared with the EXP-01 path |
| **Analysis method** | Plot velocity and acceleration vs. input angle |
| **Operator** | Suphasan Rodphai, Suraphum Changlek |

**Raw data:** `raw/`
**Processed results:** `processed/`

**Key findings**
- The trajectories from EXP-01 and EXP-02 match
- Acceleration spikes near 0°–5° and 105°–110° because of the Saturation block (hard clipping)

**Known issues / future work**
- Use a smoother input or a rate limiter instead of hard saturation
- Plot against time instead of input angle

