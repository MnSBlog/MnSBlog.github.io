---
date: 2021-11-07 21:28:00
layout: post
title: Duality Problem
subtitle: Understaning the Duality problem in Convex Optimization
description: Understaning the Duality problem in Convex Optimization
image: https://res.cloudinary.com/dm7h7e8xj/image/upload/v1559825145/theme16_o0seet.jpg
optimized_image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559825145/theme16_o0seet.jpg
category: Machine Learning
tags:
  - Machine Learning
  - Optimization
  - Convex Optimization
  - Analytically method
  - Deviation
author: 안상현
---

# ReadMe

 대부분 `Machine Learning(ML)` 문제들은 `목적함수(Objective function)` 를 `최소화(Minimize)` 하는 것에 대해 파라미터를 설정합니다. `Parameter` 를 찾는 게임이죠. 이 글은 `Convex Optimization` 은 완전한 `Convex function` 만이 아니며 `Concave function` 도 포함하고 이를 `Convex problem` 이라고 정의할 수 있는 사전 지식을 요구합니다.

# <span style="color:#2E64FE">Acquire Knowledge</span>

## Standard Form of Convex Optimization

먼저, `Duality Problem`에 접근하기 전에 `Convex Optimization` 에서의 표준 표현식을 보겠습니다.


$$
\begin{array}{l}
\min &f(x)\\
s.t. &g_i(x) \le 0,\ i=1,\dots,m\\
		 &h_i(x) = 0,\ i=1,\dots,q\\
		 \\
		 &x\in R^n\text{ is optimization variable}
\end{array}
$$


여기서 표현하는 $$ g_i(x) $$ 는 `Inequality constraints` 이며, $$ h_i(x) $$ 는 `Homologous or Equality constraints` 입니다. 각 m개와 q개 만큼 제약 조건이 존재합니다. 그러나 이런 모습을 갖췄다고 `Convex Problem`  이라 하지 않습니다.

## Satisfied conditions

`Objective function` = `Convex function` 이면서 `Constraints` = `Convex Set` 이여야 합니다. 다시 말하면 `Convexity function` 으로 정의되며 `Constraints` 은  `Feasible` 영역안에 들어오는지 한다는 얘기입니다. 그러니 결국 

