# Smart Throttle Control System - Final Project Report

## # Project Overview
This project involves the development of a control system for a vehicle's electronic throttle motor. The objective was to transform a slow motor into a high-performance system using PID control and Gain Scheduling to ensure safety and responsiveness across all driving conditions (0-100% throttle).

---

## Phase 1: Motor Plant Modeling
The throttle motor is modeled as a first-order transfer function. 
- **Model Equation:** $G(s) = \frac{k}{Tau*s + 1}$
- **Parameters:** Gain ($K$) = 1, Time Constant ($\tau$) = 0.5 seconds.
- **Transfer Function:** $G(s) = \frac{1}{0.5s + 1}$
- **Observation:** The open-loop response is stable but slow, requiring roughly 2 seconds to reach the target speed.

![Open Loop Response](results/open_loop_response.png)

---

## Phase 2: PID Controller Design
A PID controller was designed and tuned to meet strict automotive performance criteria.
- **Targets:** Rise Time < 1.0s, Overshoot < 10%.
- **Tuned Gains:** $K_p = 5$, $K_i = 10$, $K_d = 0.5$.
- **Measured Metrics:**
    - **Rise Time:** 0.36 s (Target Met)
    - **Overshoot:** 0.81% (Target Met)
    - **Settling Time:** 0.61 s

![PID Response](results/pid_response.png)

---

## Phase 3: Simulink Implementation
![Simulink block diagram](results/Block_Diagram.png) 
- **Setup:** A closed-loop feedback system with a PID Controller and a Step input.
- **Result:** The Scope output perfectly matches the analytical MATLAB results, validating that the block diagram is correct.

![Simulink Scope Response](results/simulink_response.png)

---

## Phase 4: Gain-Scheduled Controller
To optimize the car's performance at different speeds, a Gain-Scheduled controller was implemented with three regions:
- **Zone 1 (0-30%):** Smooth tuning for low-speed parking ($K_p = 2.5$).
- **Zone 2 (30-70%):** Balanced cruising using primary tuned gains ($K_p = 5$).
- **Zone 3 (70-100%):** Aggressive tuning for rapid acceleration ($K_p = 15$).

![Gain Scheduled Response](results/gainscheduled_response.png)

---

## 5. Phase 5: Conclusion & Comparison
The final analysis compares the fixed PID controller against the Gain-Scheduled version. The results demonstrate that while the fixed PID is stable, the **Gain-Scheduled controller** provides a significantly sharper response at high throttle levels (95%), ensuring the vehicle is responsive during overtaking maneuvers.

![Comparison Plot](results/comparison_plot.png)

---

## 6. Project Files & Usage
| File | Description |
| :--- | :--- |
| `plant_model.m` | Initializes the motor transfer function and plots Phase 1. |
| `pid_design.m` | Designs the PID controller and calculates Phase 2 metrics. |
| `throttle_model.slx` | The Simulink block diagram for Phase 3 verification. |
| `gain_scheduled.m` | Implements the multi-zone logic for Phase 4. |
| `comparison.m` | Generates the final performance comparison for Phase 5. |
| `results/` | Folder containing all 5 generated plots required for the report. |