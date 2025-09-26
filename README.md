# Team Assignment Optimizer 🤖

An interactive visualization tool for optimizing team assignments using Integer Linear Programming. This tool demonstrates how to balance individual task preferences with teammate preferences when assigning people to project teams.

## 🚀 Live Demo

Visit the live demo: **[Team Optimizer Visualization](https://yourusername.github.io/team-optimizer/)**

## 📋 Overview

This project solves a common organizational problem: **How do you assign 29 people to 6 different tasks (4-5 people per task) while maximizing both task satisfaction and team compatibility?**

### The Challenge
- 29 people need to be assigned to 6 tasks
- Each task gets 4-5 people (5 tasks get 5 people, 1 task gets 4 people)  
- Each person has ranked preferences for tasks (1st-6th choice)
- Each person has preferences for teammates (up to 4 people they'd like to work with)

### The Solution
We formulate this as an **Integer Linear Program (ILP)** that optimizes a weighted combination of:
- **Task Satisfaction**: People get their preferred tasks
- **Team Satisfaction**: People work with their preferred teammates
- **Fairness Constraint**: Limit how many people get their worst choices

## 🎮 Interactive Features

### 1. **Alpha (α) Parameter Control**
- α = 0.0: Pure task preference optimization
- α = 0.5: Balanced approach  
- α = 1.0: Pure teammate preference optimization

### 2. **Fairness Constraint**
- Control maximum number of people assigned to their 5th/6th choice tasks
- Hard constraint that ensures fairness in assignments

### 3. **Real-time Metrics**
- **Unhappiest Person**: Most important for fairness
- **Average Happiness**: Overall satisfaction
- **Mutual Connections**: People who chose each other and got teamed up
- **Connection Satisfaction**: Percentage of teammate preferences fulfilled

### 4. **Visual Analytics**
- **Happiness Distribution**: Histogram of individual satisfaction scores
- **Color-coded Task Rankings**: Gradient visualization showing average preference rank per task
- **Team Connection Highlighting**: Visual indicators for mutual (💚) and one-way (💛) teammate preferences

## 🔢 Mathematical Formulation

### Data
- **P = {1..29}** people, **T = {1..6}** tasks (capacity = 4-5 each)
- **rank_task[i][k] ∈ {1..6}** = person i's rank for task k (1 = top choice)
- **pref_team[i]** = list of up to 4 people i wants to work with

### Score Conversion
- **task_score[i][k] = 7 - rank_task[i][k]** (1st→6 points, 6th→1 point)
- **team_score[i][j] = 5 - r** if j is i's r-th teammate choice

### Decision Variables
- **x[i,k] ∈ {0,1}**: 1 if person i assigned to task k
- **s[i,j,k] ∈ {0,1}**: 1 if persons i and j both on task k

### Constraints
- Each person gets exactly one task: **∀i: Σ_k x[i,k] = 1**
- Each task has 4-5 people: **∀k: Σ_i x[i,k] ∈ {4,5}**
- Fairness constraint: **Σ_i I(rank[i] ≥ 5) ≤ max_unhappy**
- Pair variables linked to assignments

### Objective
**Maximize:** (1-α) × Task_Satisfaction + α × Teammate_Satisfaction

## 🛠️ Technical Implementation

- **Frontend**: HTML5/CSS3/JavaScript with real-time optimization
- **Visualization**: Chart.js for metrics, custom CSS for team displays
- **Algorithm**: Constrained greedy optimization with fairness constraints
- **Deployment**: GitHub Pages for easy sharing

## 🎯 Key Insights You Can Explore

1. **Fairness vs. Efficiency Trade-offs**: How constraining worst-case assignments affects overall satisfaction
2. **Social Network Effects**: Impact of teammate preferences on team formation
3. **Task Popularity Patterns**: Which tasks naturally attract people who want to work together
4. **Optimization Sensitivity**: How small changes in α dramatically affect outcomes

## 📊 Sample Data

Includes real preference data from 29 participants across 6 robotics research tasks:
- Fingertip Tactile Sensors
- Real Time RGB-only Teleoperation  
- Motor and Actuation Tower Upgrade
- Robot Playing Jenga with RL
- Digital Twin w/ Gaussian Splatting
- PIP-DIP Coupling for Improving Manipulation Capability

## 🚀 How to Deploy Your Own Version

1. **Fork this repository**
2. **Go to Settings → Pages**
3. **Select "Deploy from a branch" → "main"**
4. **Your site will be live at**: `https://yourusername.github.io/team-optimizer/`

## 🤝 Contributing

Contributions welcome! Areas for improvement:
- Enhanced optimization algorithms
- Additional visualization features
- Mobile responsiveness improvements
- Performance optimizations

## 📄 License

MIT License - feel free to use and modify for your own projects!

---

*This project demonstrates practical applications of optimization theory in organizational settings, showing how mathematical models can solve real-world assignment problems while balancing multiple competing objectives.*