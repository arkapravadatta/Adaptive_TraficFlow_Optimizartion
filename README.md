# 🚦 Adaptive Traffic Flow Optimization using Reinforcement Learning

## 📌 Objective
This project aims to develop and compare **Reinforcement Learning agents** — specifically **Deep Q-Network (DQN)** and **Actor-Critic (AC)** — to optimize highway traffic flow and dynamically regulate vehicle speed. The agents are trained to adaptively control the speed and lane changes of a selected vehicle to improve traffic efficiency, reduce congestion, and enhance safety.

---

## 🧑‍🔬 Reinforcement Learning Setup

### 🔢 State Space (8 features):
1. Vehicle Speed (`v_Vel`) [m/s]  
2. Vehicle Acceleration (`v_Acc`) [m/s²]  
3. Lane Position (`Lane_ID`)  
4. Distance to Preceding Vehicle (`Space_Headway`) [m]  
5. Time Gap to Preceding Vehicle (`Time_Headway`) [s]  
6. Vehicle Class (`v_Class`)  
7. Global X Position (`Global_X`)  
8. Global Y Position (`Global_Y`)  

### 🎮 Action Space (5 discrete actions):
| Action | Description               | Condition                                                  |
|--------|---------------------------|-------------------------------------------------------------|
| 0      | Maintain current speed    | No change                                                   |
| 1      | Increase speed (+2 m/s)   | If `Space_Headway ≥ 15 m`                                 |
| 2      | Decrease speed (-2 m/s)   | If `Space_Headway < 10 m`                                   |
| 3      | Change lane to the left   | If lane exists, unoccupied, and `Space_Headway ≥ 15 m`     |
| 4      | Change lane to the right  | If lane exists, unoccupied, and `Space_Headway ≥ 15 m`     |

### 🌟 Reward Function
```
R = (10 − |Vt − Voptimal|) − Pcollision
```
Where:
- `Vt` = Current vehicle speed
- `Voptimal` = 27 m/s (recommended highway speed)
- `Pcollision` = 20 if `Space_Headway < 5m`, otherwise 0

---

## 📊 Dataset
- **File:** `DQN_DDQN_Actor_Critic_dataset.csv`
- **Frequency:** 10 Hz (i.e., one frame every 0.1 seconds)
- **Content:** Vehicle trajectory data for simulating realistic highway traffic conditions

---

## ⚙️ Project Workflow

1. **Data Loading**  
   ✔ Dataset is loaded and inspected for relevant features. *(Preprocessing not yet implemented)*

2. **Environment Design**  
   ✔ Custom traffic control environment using OpenAI Gym style API

3. **Action Definitions**  
   ✔ MaintainSpeed, IncreaseSpeed, DecreaseSpeed, ChangeLaneLeft, ChangeLaneRight

4. **Reward Function**  
   ✔ Implements collision risk and speed deviation penalty logic

5. **Replay Buffer (DQN)**  
   ✔ Experience memory system for efficient training

6. **DQN Agent**  
   ✔ Deep neural network with experience replay and target updates

7. **Actor-Critic Agent**  
   ✔ Policy (actor) and value (critic) networks trained concurrently

8. **Training and Plotting**  
   ✔ Graphs for average rewards across episodes for DQN and Actor-Critic

9. **Comparison Summary**  
   ✔ Analysis analysis comparing performance, stability, and decision quality

---

## 📈 Expected Outcomes
- Demonstrate how RL improves vehicle behavior in dynamic traffic
- Visual reward comparison between DQN and Actor-Critic
- Provide insights into the pros and cons of value-based vs. policy-gradient methods
