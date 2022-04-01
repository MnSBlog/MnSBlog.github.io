---
date: 2022-04-01 13:46:00
layout: post
title: 유니티의 환경에서 강화학습 진행하기 
subtitle: Reinforcement Learning with RLlib in the Unity
description: Reinforcement Learning with RLlib in the Unity
image: https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Major/RL/RLLIB/0401/Title.PNG
category: Major
tags:
  - Basic
  - Reinforcement Learning
  - Unity
  - Ray
author: 안상현
---



# <span style="color:#2E64FE">ReadMe</span>

 아래 내용은 최병규, 강동훈 저서인 **Modeling and Simulation of discrete-event systems**  책의 내용을 주로 다루고 있습니다. 

 해당 시리즈의 목차입니다. (챕터 목차는 제일 아래에 있습니다.)

---

1. [Overview of Computer Simulation](https://mnsblog.github.io/MJ-SM-Chp1-1/) 
2. Basics of Discrete-Event System Modeling and Simulation
3. Input Modeling for Simulation
4. Introduction to Event-Based Modeling and Simulation
5. Parameterized Event Graph Modeling and Simulation
6. Introduction to Activity-Based Modeling and Simulation
7. Simulation of ACD Models Using Arena
8. Output Analysis and Optimization
9. State-Based Modeling and Simulation
10. Advanced Topics in Activity-Based Modeling and Simulation
11. Advanced Event Graph Modeling for Integrated Fab Simulation
12. [Concepts and Applications of Parallel Simulation](https://mnsblog.github.io/MJ-SM-Chp12-1/) (Here)

---

# <span style="color:#2E64FE">INTRODUCTION</span>

 이번 챕터에서 사용하는 대부분의 전공용어들이 `Fujimoto [2000]` 을 참고했습니다만, 병렬 시뮬레이션(*parallel simulation*)은 조금 다르다고 볼 수 있습니다. `Fujimoto` 의 설명을 참고하면, 하나의 방에 있는 컴퓨터 집합에서 실행되는 시뮬레이션이라 했습니다. 반면에 분산 시뮬레이션(*distributed simulation*)은 물리적으로 분산되어 있는  머신들에서 실행되는 것이라 합니다. 이 포스팅에서는 병렬 시뮬레이션

# <span style="color:#2E64FE">Chapter index</span>

---

12.1. [Introduction](https://mnsblog.github.io/MJ-SM-Chp12-1/) (Here)

12.2. [Parallel Simulation of Workflow Management System](https://mnsblog.github.io/MJ-SM-Chp12-2/)

12.3. [Overview of High-Level Architecture/Run-Time Infrastructure](https://mnsblog.github.io/MJ-SM-Chp12-3/)

12.4. [Implementation of a Parallel Simulation with High-Level Architecture/Run-Time Infrastructure](https://mnsblog.github.io/MJ-SM-Chp12-4/)

---

