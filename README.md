# SpaceRobotics-Boustrophedon-Navigator
ROS2 PD-Controlled Lawnmower Pattern Navigator | Space Robotics and AI
# 🤖 First Order Boustrophedon Navigator (ROS 2) 
**Author:** Vamshikrishna Gadde  

![ROS2](https://img.shields.io/badge/Framework-ROS2-blue)
![Python](https://img.shields.io/badge/Language-Python3-yellow)
![Controller](https://img.shields.io/badge/Type-PD_Controller-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 🛰️ Overview
This ROS 2 project implements a **Boustrophedon (“lawnmower”) navigation pattern** in simulation using the `turtlesim` package.  
A **PD controller** generates smooth linear and angular velocity commands for coverage motion—ideal for aerial or planetary exploration robots.

---

## 🧩 Repository Structure
```
SpaceRobotics-Boustrophedon-Navigator/
├── README.md
├── report/ASSIGNMENT_1_SPACE_ROBOTICS_AND_AI.pdf
├── src/first_order_boustrophedon_navigator.py
└── results/
    ├── trajectory_plot.png
    ├── cross_track_error.png
    └── velocity_profiles.png
```

---

## ⚙️ Software & Libraries
| Component | Description |
|------------|-------------|
| **ROS 2 (Humble or Foxy)** | Robot Operating System for node communication |
| **rclpy** | Python ROS 2 client library |
| **turtlesim** | 2D simulation environment |
| **numpy, math, deque** | Numerical and vector operations |
| **rqt_reconfigure** | Real-time parameter tuning tool |

---

## 🚀 How to Run the Node
```bash
# 1. Source your ROS 2 workspace
source /opt/ros/humble/setup.bash

# 2. Run turtlesim
ros2 run turtlesim turtlesim_node

# 3. Run the controller
python3 src/first_order_boustrophedon_navigator.py
```

---

## 🧠 Algorithm Overview
1. **Waypoint Generation** → Creates a zig-zag path between (2 ≤ x ≤ 9, 3 ≤ y ≤ 8).  
2. **Pose Feedback** → Subscribed from `/turtle1/pose`.  
3. **Cross-Track Error Computation** → 2D projection to measure deviation from path.  
4. **PD Controller** → Linear and Angular velocity adjusted using tuned gains.  
5. **Parameter Callback** → Dynamic runtime gain tuning via `rqt_reconfigure`.

---

### ⚙️ PD Control Equations

**Linear Velocity:**

$$
v = K_p^{(lin)} \cdot d + K_d^{(lin)} \cdot \frac{\Delta d}{\Delta t}
$$

**Angular Velocity:**

$$
\omega = K_p^{(ang)} \cdot \theta_{error} + K_d^{(ang)} \cdot \frac{\Delta \theta}{\Delta t}
$$

---

## 🔧 Tuned PD Parameters
| Parameter | Initial | Final | Effect |
|------------|----------|--------|--------|
| Kp_linear | 10.0 | 8.0 | Reduced overshoot |
| Kd_linear | 0.1 | 0.05 | Smoother motion |
| Kp_angular | 5.0 | 7.0 | Improved cornering |
| Kd_angular | 0.2 | 0.000 | Removed oscillation |
| Spacing | 1.0 | 0.5 | Better coverage |

---

## 📊 Performance Metrics
- **Average Cross-Track Error:** 0.15 units  
- **Maximum Cross-Track Error:** 0.45 units  
- **Smooth motion** and precise cornering achieved  
- **Real-time tuning** enabled through `rqt_reconfigure`

Trajectory Result <img width="472" height="445" alt="Result" src="https://github.com/user-attachments/assets/1ad6b577-89fe-4e8e-ba4f-0ff31ddbaad7" />

Cross-Track Error <img width="861" height="431" alt="Cross Track Error" src="https://github.com/user-attachments/assets/54a14042-c9ef-4b55-a92f-49dd5bfed6ad" />


---

## ⚙️ Tuning Procedure
1. Launch node and monitor `/cross_track_error` topic.  
2. Adjust parameters in `rqt_reconfigure`.  
3. Observe real-time feedback and refine gains.  
4. Continue until oscillations and deviation minimize.

---

## 🧠 Challenges & Solutions
| Issue | Fix |
|--------|-----|
| Oscillations on straight paths | Lowered Kp_linear and Kd_linear |
| Poor cornering | Raised Kp_angular and set Kd_angular = 0 |
| Inconsistent coverage | Reduced line spacing to 0.5 m |

---

## 📚 References
- ROS 2 Documentation – <https://docs.ros.org/en/humble/>  
- rclpy API – <https://docs.ros2.org/latest/api/rclpy/html/>  

---

## Demonstrates:
- **Control Systems Tuning** (PD loops and gain balancing)  
- **Autonomous Coverage Planning** (boustrophedon pattern)  
- **ROS 2 Implementation & Simulation**  
- **Real-time Data Monitoring and Optimization**

---

## 👤 Author
**Vamshikrishna Gadde**  
📧 vgadde5@asu.edu  
🔗 [LinkedIn](https://www.linkedin.com/in/vamshikrishna-gadde9999/)  
💻 [GitHub](https://github.com/GVK-Engine/VAMSHIKRISHNA-GADDE)

---

## 🪪 License
MIT License – Free for educational and research use.
