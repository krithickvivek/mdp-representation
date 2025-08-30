# MDP REPRESENTATION

## AIM:
To simulate a cleaning robot that navigates a grid, avoids obstacles, cleans dirt, and optimizes actions using reinforcement learning to maximize rewards.

## PROBLEM STATEMENT:
A robot vacuum cleaner moves around a house to clean dust. The house has 
several rooms, and each room may or may not have dust. The robot’s goal is to 
clean all rooms while using the least baƩery power possible.

### State Space
- **Robot Position** – Where the robot is right now (living room, kitchen, bedroom, etc.).
- **Dust Status** – Dust in each room whether the room is CLEAN or DIRT.
- **Battery Level** – Low, Medium, High.
- **Obstacle** – Furniture, Walls, Objects, None.
 

### Sample State
- Position of the robot is in kitchen or bedroom or different rooms.
- Dust Status on each room kitchen, bedroom, living room, etc.
- The battery level is medium.
- There is a furniture at the pathway.


### Action Space
- **Clean** – Suck and clean the dirt.
- **Charge** – Go to charging station if the battery is about to die.
- **Avoid Obstacles** – Move left, right, front, and back if an obstacle is observed to avoid it and move on.
- **Movements** – Move forward, rotate, left, right, etc.

### Sample Action
- Clean the room.
- Avoid obstacles and move towards dirt to clean it.

### Reward Function
- Cleaning the dirty room => +10 points.
- Crashes on any obstacles => -5 points.
- Being in a clean block without cleaning => 0 point.

### Graphical Representation
<img width="877" height="863" alt="image" src="https://github.com/user-attachments/assets/5a085c36-baf9-4651-b1e8-7e8ef01e5152" />

## PYTHON REPRESENTATION:
```python
import random

# Define grid cells
cells = {i: f"Cell {i}" for i in range(25)}  # 5x5 grid (0-24)
battery = ["High", "Medium", "Low"]

# Define dirt presence (1 for dirt, 0 for clean)
dirt_status = {i: random.choice([0, 1]) for i in range(25)}  

# State Space (Position, Battery)
states = [(pos, bat) for pos in cells.keys() for bat in battery]

# Actions
actions = {0: "Left", 1: "Right", 2: "Up", 3: "Down", 4: "Clean", 5: "Charge"}

# Reward Function
def get_reward(state, action):
    pos, bat = state
    reward = 0

    # Cleaning dirt
    if action == 4 and dirt_status[pos] == 1:
        reward = 10
        dirt_status[pos] = 0  # Cleaned
    # Charging at station (Cell 0)
    elif action == 5 and pos == 0:
        reward = 5
    # Obstacle penalty (example: obstacle cells 4,6,13,20,24)
    elif pos in [4, 6, 13, 20, 24] and action in [0, 1, 2, 3]:
        reward = -5
    else:
        reward = 0
    return reward

# Example simulation
state = (0, "High")  # Starting from charging station
print("Initial State:", state)

for step in range(10):  # Run 10 steps
    action = random.choice(list(actions.keys()))
    reward = get_reward(state, action)
    print(f"Step {step+1}: Action: {actions[action]}, Reward: {reward}")
```

## OUTPUT:
<img width="431" height="265" alt="image" src="https://github.com/user-attachments/assets/a0c2c63f-5c7b-4ffe-b9b1-495a61e9d395" />


## RESULT:
The Robotic Vacuum Cleaner problem was successfully represented as a Markov Decision Process (MDP). The state space, actions, rewards, and transitions were defined, and Python simulation showed environment interaction for optimal cleaning policy.
