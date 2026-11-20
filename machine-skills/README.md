# Machine skills

Store machine command sets, operating procedures, and skill instructions here. For each skill, state the supported machine and software versions, required setup, input format, expected output, and safety limits. Review commands before running them on physical equipment.

> **Note:** This project is currently simulation-based. The skills below are software procedures.
## Skill 1: Run the Symbolic Kinematics Script

| Item | Detail |
|---|---|
| **Purpose** | Compute position, velocity, acceleration, and gripping force of the gripper tip vs. input angle θ₁ |
| **Supported software** | MATLAB (version: 2026b) + Symbolic Math Toolbox |
| **Required setup** | Open the script in `software/` and set the link parameters |
| **Input format** | Link lengths (mm): l₂ = 31, l₃ = 22, l₄ = 31, l_g = 32.919; pivot O₄ = (−8.25, 20.891) mm; offset = −6.6°; θ₁ range = −20° to 90°; T_in = 10 N·mm |
| **Command** | Run the script in the MATLAB command window |
| **Expected output** | 4 plots (position, velocity, acceleration, force) and a trajectory animation |
| **Safety / limits** | Software only. Keep θ₁ within −20° to 90°. Force spikes near θ₁ ≈ 2°–3° (toggle position) |

## Skill 2: Run the Simulink / Simscape Multibody Model

| Item | Detail |
|---|---|
| **Purpose** | Simulate the gear-driven parallel gripper and record the tip trajectory |
| **Supported software** | MATLAB Simulink + Simscape Multibody (version: 2026b) |
| **Required setup** | Open the `.slx` model in `simulation/`, check World Frame and Solver Configuration |
| **Input format** | Sine wave → Saturation block → Revolute joint (Gear right) |
| **Expected output** | Tip trajectory plot, velocity and acceleration vs. input angle |
| **Safety / limits** | Software only. The Saturation block causes acceleration spikes at the limits, so do not use these values directly as real motor loads |

