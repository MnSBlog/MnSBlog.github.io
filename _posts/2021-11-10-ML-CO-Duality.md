---
date: 2021-11-10 21:28:00
layout: post
title: Duality Problem
subtitle: Understaning the Duality problem in Convex Optimization
description: Understaning the Duality problem in Convex Optimization
image: https://drive.google.com/uc?export=view&id=1LKfMFdMPxpp3evElh4F8YlL4mZbrs2o9
category: Machine Learning
tags:
  - Machine Learning
  - Optimization
  - Convex Optimization
  - Analytically method
  - Deviation
math: true
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

`Objective function` = `Convex function` 이면서 `Constraints` = `Convex Set` 이여야 합니다. 다시 말하면 `Convexity function` 으로 정의되며 `Constraints` 은  `Feasible` 영역안에 들어오는지 한다는 얘기입니다. 그러니 사전 지식으로서 필요한 `Convex function` 인지 확인하는 `Convexity test` 를 통하여, 복습을 하겠습니다.

##  Convex Function


$$
\text{Convex Function:}\\
f(ax+(1-a)y) \le af(x) + (1-a)f(y)\\
\\
\text{Concave Function:}\\
f(ax+(1-a)y)\ge af(x)+(1-a)f(y)\\
\\
\forall\ x, y, 0\le a\le 1
$$



`Convex, Concave` 에 대한 기본이 되는 구분식입니다. **우변**이 의미하는 바는 두 지점(a로서 갈리는)의 합을 의미하는 데요. 두 지점의 합은 결국 임의의 두 지점의 중간 부분을 얘기하게 됩니다. **결론적으로 임의의 두 점을 잇는 직선의 가운데 지점과 동일한 f(x)의 값이 작으면 Convex 크면 Concave** 입니다. Convex는 아무래도 Cup 모양이고, Concave는 Cap 모양이라 직선을 그어 판단할 수 있죠. **같다는 의미가 빠지면 Strictly Concave / Convex 있으면 그냥 Concave / Convex** 입니다.  

[이미지 Convex Concave 선 그리기]

### Second-order gradient(twice differentiable real function)

직선을 그어 두 지점을 로나로나 땅!땅! 해버리면, 편하겠지만 Function 자체가 다변량(Multiple variables)으로 구성되어 있으면 막막합니다. `Seperable programming` 으로 나뉘어 보면 `Convex function`의 성질은 아래와 같습니다.
$$
\text{Convex / Concave function = Concave(or Convex) + ... + Convex(or Concave)}
$$
`Hessian matrix` 를 이용하여 P.D(Positive Definite) 혹은 P.SD(Positive Semi-Definite) 조건을 생성해 직선의 조건을 대체하겠습니다.
$$
\begin{array}{l}
\text{Convex Function:}\\
0 \le \frac{\partial^2 f(x_1,\dots,x_n)}{\partial x_a^2}\\
\\
\text{Concave Function:}\\
0\ge \frac{\partial^2 f(x_1, \dots, x_n)}{\partial x_a^2}\\
\\
\text{and}\ \det(H) \ge 0\\
\\
1\le a\le n
\end{array}
\\
$$
이제 a를 통해 임의의 직선을 그려 그 중간을 비교하는 것이 아닌, `Hessian matrix` 를 직선으로 대체했습니다. 기존 비교대상인 f(x)는 0으로 바꿔버렸구요. 가벼운 예시 하나를 풀어보겠습니다.
$$
\begin{array}{l}
\text{Convexity test}\\
f(x)=(2x_1-3x_2)^3=8x_1^3-36x_1^2x_2+54x_1x_2^2-27x_2^3\\
\end{array}
$$

$$
\frac{\partial f(x_1, x_2)}{\partial x_1}=24x_1^2-72x_1x_2+54x_2^2\\
\frac{\partial f(x_1, x_2)}{\partial x_2}=-36x_1^2+108x_1x_2-91x_2^2\\
\nabla^2f(x)=
\begin{bmatrix}
\frac{\partial^2f(x_1,x_2)}{\partial x_1^2} & \frac{\partial^2f(x_1,x_2)}{\partial x_1\partial x_2} \\
\frac{\partial^2f(x_1,x_2)}{\partial x_2\partial x_1} & \frac{\partial^2f(x_1,x_2)}{\partial x_2^2}
\end{bmatrix}
=
\begin{bmatrix}
48x_1-72x_2 & -72x_1+108x_2\\
-72x_1+108x_2 & 108x_1-182x_2
\end{bmatrix}\\
det(\nabla^2f(x))=
(48x_1-72x_2)(108x_1-182x_2)-(-72x_1+108x_2)^2
$$

눈치 빠른 분들은 이걸 풀지 않으셨겠죠. 3차식은 두번의 변곡점이 생기기에 `Convex function`  을 보장해주지 않습니다. 그래서 두 번 미분을 하더라도 다변량 함수로서 남아있죠. 그래서 $$ 48x_1-72x_2 $$부터 늘 음수인지 양수인지 보장할 수 없습니다. 이제 진짜 올바른 예제를 보시죠.
$$
\begin{array}{l}
\text{Convexity test}\\
f(x)=(2x_1-3x_2)^2=4x_1^2-12x_1x_2+9x_2^2\\
\end{array}
$$

$$
\frac{\partial f(x_1, x_2)}{\partial x_1}=8x_1-12x_2\\
\frac{\partial f(x_1, x_2)}{\partial x_2}=-12x_1+18x_2\\
\nabla^2f(x)=
\begin{bmatrix}
\frac{\partial^2f(x_1,x_2)}{\partial x_1^2} & \frac{\partial^2f(x_1,x_2)}{\partial x_1\partial x_2} \\
\frac{\partial^2f(x_1,x_2)}{\partial x_2\partial x_1} & \frac{\partial^2f(x_1,x_2)}{\partial x_2^2}
\end{bmatrix}
=
\begin{bmatrix}
8 & -12\\
-12 & 18
\end{bmatrix}\\
det(\nabla^2f(x))=
(8)(18)-(-12)^2= 0
$$

**8은 양수**이니 `Strictly Convex`, **18도 양수**라 `Strictly Convex`, det(H)는 0이기에 `Convex or Concave` 입니다. 고로 해당 함수는 `Convex function`이 맞습니다.

## Convex Sets

`Function` 이 선을 그어주는 것이라면 `Set` 은 면적을 얘기합니다. 굳이 얘기하자면 `Function` 이 경계선이고 그 경계선 안에 옹기종기 모여사는 것이죠.
$$
\forall\ x, y\in C\ \cap\ 0 \le a \le 1\\
ax+(1-a)y \in C
$$
그런 이유로 임의의 두 선의 중간지점은 집합 안에 들어있어야 한다는 것이 `Convex Set`의 정의입니다.

`Convex set` 은 여러가지 방법으로 설명할 수 있습니다.

#### Preserve convexity

변환하여 알 수 있는 방법들로는 `Intersection`, `Affine functions`, `Perspective function`, `Linear-fractional functions` 가 있죠. 

- **Intersection:**

- **Affine function:**
- **Perspective function**
- **Linear-fractional function**

#### Simple Convex Set

- **Hyperplane:** 

$$
\text{Set of the form }\{x|a^Tx=b\}(a\ne0)\\
$$

- **Hyperspace: **

$$
\text{Set of the form}\{x|a^Tx\le b\}(a\ne0)
$$

선과 면의 차이는 `Homogeneous` , `Inequality` 로 표현하는차이밖에 없습니다. `Hyperplane` 은 a개 만큼의 `Affine` 변환이고, `Hyperspace` 는 `Affine` 변환에  의한 바운더리로서 모두 `Convex set` 입니다.

- **Polyhedra:**

  완벽한 구를 깎아내서 만들 수 있는 볼록 다면체류(`Uniform Plyhedra`)는 모두 `Convex set`입니다. 모두 선형결합으로서 만들어낼 수 있죠.

- **Norm ball and cone:**

$$
\begin{array}{l}
\text{Norm ball}: &\{x| \abs \ x-x_c\ \abs \le r\}\\
\text{Euclidean ball}: &\{x|\abs{\abs{x-x_c}}_2 \le r\}\\
\text{Ellipsoid}: &\{x|(x-x_c)^TP^{-1}(x-x_c)  \le 1\}\\
\text{Norm cone}: &\{(x,t)|\abs{\abs{x}}\le t\}\\
\end{array}
$$

 해당 수식을 그림으로 그릴 수 있다면, 아래 `Conic combination` 내용은 넘어가셔도 됩니다.

- **Conic combination:**

$$
x=\theta_1x_1+\theta_2x_2\\
x_1, x_2 \gt 0 \text{ and } \theta_1, \theta_2 \ge 0
$$

x값이 커질수록 조건을 만족하는 조합들은 무궁무진합니다. x가 0이되면 조합의 수가 적어지죠. 이러한 조합들을 촘촘하게 3D plot으로 표현하면 Cone형태가 됩니다.

[이미지 Convex Cone 그리기]

# <span style="color:#2E64FE">Duality Problem</span>

- `Primal problem(기존 문제)` 가 `Convex` 하지 않아도, `Duality problem` 은 늘 `Convex` 합니다.
- `Duality problem` 의 변수들의 수는 `Primal problem` 의 제약식의 수와 동일합니다.
- `Duality problem` 의 `Maximum value` 는 `Primal problem` 의 `Minimum value(Optimal value)` 입니다.

## Lagrangian

$$
\begin{array}{l}
\text{Primal Problem}\\
\min & f(x)\\
s.t.\ & g_i(x) \le 0, & i=1,\dots,m\\
&h_i(x)=0, & i = 1,\dots,q
\end{array}
\implies
\begin{array}{l}
\text{Duality Problem}\\
\mathcal{L}(x,\lambda,\nu)=f(x)+\underset{i=1}{\overset{m}{\sum}}\lambda_ig_i(x)+\underset{j=1}{\overset{q}{\sum}}\nu_jh_j(x)\\
g_i(x)\le0, \lambda \ge 0\\
h_j(x)=0
\end{array}
$$



위 식은 `Primal problem` 에서 `Duality problem` 으로 변환입니다. lambda와 nu(called Dual variables)를 이용하여 제약식을 다 `Lagrangian` 변환 했습니다.

예제를 볼까요.
$$
\begin{array}{l}
\text{Primal problem}\\
\max & f(x)= &3x_1+ &5x_2\\
s.t. & & x_1 & &\le 4\\
	& & & 2x_2 & \le 12\\
	& & 3x_1+&2x_2&\le18\\
	&x_1,x_2\ge0
	\end{array}
	\quad = \quad
\begin{array}{l}
\text{Primal problem}\\
\min & f(x)= &-3x_1 &-5x_2\\
s.t. & & x_1 & &-4 \le 0\\
	& & & 2x_2 &-12 \le 0\\
	& & 3x_1+&2x_2&-18\le0\\
	&x_1,x_2\ge0
\end{array}
$$

$$
\begin{array}{l}
\text{Dual Problem}\\
\mathcal{L}_P(x, \lambda)&= (-3x_1-5x_2)+\lambda_1(x_1-4)+\lambda_2(2x_2-12)+\lambda_3(3x_1+2x_2-18)\\
&=-3x_1-5x_2+\lambda_1x_1-4\lambda_1+\lambda_2x_2-12\lambda_2+3\lambda_3x_1+2\lambda_3x_2-18\lambda_3\\
&=x_1(\lambda_1+3\lambda_3-3)+x_2(+\lambda_2+2\lambda_3-5)-4\lambda_1-12\lambda_2-18\lambda_3
\end{array}
$$

끝으로, `Primal problem` 이 원래 `Maximize` 문제이기에 전부 다 음수를 취해줍니다.
$$
\begin{array}{l}
\mathcal{L_D(x,\lambda)} & = -1 *\mathcal{L}_P(x,\lambda)\\
&=-x_1(\lambda_1+3\lambda_3-3)-x_2(+\lambda_2+2\lambda_3-5)+4\lambda_1+12\lambda_2+18\lambda_3
\end{array}
$$
그럼 이를 다시 정리하면
$$
\begin{array}{l}
\min &4\lambda_1+12\lambda_2+18\lambda_3\\
s.t. & -\lambda_1-3\lambda_3-3 &\le 0\\
&-2\lambda_2-2\lambda_3+5&\le0\\
&-4\lambda_1-12\lambda_2-18\lambda_3&\le0\\
\lambda_1,\lambda_2\lambda_3\ge0
\end{array}
$$

## Lagrangian Dual Function

---

`Duality problem` 의 `Maximum value` 는 `Primal problem` 의 `Minimum value(Optimal value)` 입니다.

---

앞에서 설명한 윗 내용을 알기 위하여 한 단계 더 나아가겠습니다. x를 제거한 형태를 `Lagrangian Dual Function` 이라고 부릅니다.
$$
\begin{array}{l}
\mathcal{L}_D(\lambda,\nu)&=\underset{x}{\inf} \mathcal{L(x,\lambda,\nu)}\\
&=\underset{x}{\inf}f(x)+\underset{i=1}{\overset{m}\sum}\lambda_ig_i(x)+\underset{j=1}{\overset{q}\sum}\nu_jh_j(x)
\end{array}
$$
`inf` 는 하한으로 수렴한다는 의미인 infimum입니다. x가 하한으로 수렴하게 되면, `Dual problem(Maxmimize)` 의 값은 `Primal problem(Minimize)` Optimal value 보다 항상 작음을 알 수 있습니다. 

lambda에 붙는 g(x)는 0보다 작거나 같고, nu에 붙는 h(x)는 0이라는 제약을 늘 함께하고 있습니다. 그러니 h(x)는 뭘 넣어도 0이겠죠.
$$
\sum_{i=1}^m\lambda_ig_i(x)+\sum_{j=1}^q\nu_jh_j(x)\le0\\
\sum_{i=1}^m\lambda_ig_i(x)\le0
$$
그렇다면, `Lagrangian function` 과 `Primal function` 은 아래처럼 비교가능합니다.
$$
\mathcal{L}(x,\lambda,\nu)=f(x)+\underset{i=1}{\overset{m}{\sum}}\lambda_ig_i(x)+\underset{j=1}{\overset{q}{\sum}}\nu_jh_j(x)\le f(x)
$$
 `Lagrangian dual function` 은 하한으로 x를 수렴하기 때문에 기존 `Lagrangian function` 보다 작습니다.
$$
\mathcal{L}_D(\lambda,\nu)=\inf_x\mathcal{L}(x,\lambda,\nu)\le\mathcal{L}(x,\lambda,\nu)\le f(x)
$$

### Practice

저명한 예제들을 통해 `Lagrangian dual function` 변환 연습을 해보겠습니다.
$$
\text{Linear problem}:\\
\begin{array}{l}

\min & c^Tx\\
s.t. & Ax\le b\\
x\ge0
\end{array}
$$

$$
\begin{array}{l}
\mathcal{L}(x,\lambda)=c^Tx+\lambda^T(Ax-b)=c^Tx+Ax^T\lambda-b^T\lambda=(c+A^T\lambda)^Tx-b^T\lambda\\
\end{array}
$$

$$
\text{Dual problem}:\\
\begin{array}{l}
\max & -b^T\lambda\\
s.t. &A^T\lambda+c\ge0\\
\lambda\ge0
\end{array}
$$

여기까지가 `Lagrangian function` 입니다. 선형 문제는 쉬워서 따로 `inf` 를 설명하기 부족하니 여기서 정리하겠습니다.
$$
\mathcal{L}_D(\lambda)=-b^T\lambda+\inf_x\ (A^T\lambda+c)^Tx
$$
이 감을 살려서 `Quadratic problem` 을 하겠습니다.
$$
\text{Quadratic problem}:\\
\begin{array}{l}

\min & x^TPx\\
s.t. & Ax\le b\\
&Cx=d
\end{array}
$$

$$
\begin{array}{l}
\mathcal{L}(x,\lambda,\nu)&=x^TPx+\lambda^T(Ax-b)+\nu^T(Cx-d)\\&=x^TPx+Ax^T\lambda-b^T\lambda+Cx^T\nu-d^T\nu\\
&=(x^TP+A^T\lambda+C^T\nu)^Tx-b^T\lambda-d^T\nu
\end{array}
$$

$$
\begin{array}{l}
\mathcal{L}_D(\lambda,\nu)&=-b^T\lambda-d^T\nu+\inf\ (x^TP+A^T\lambda+C^T\nu)^Tx\\
\nabla_x\mathcal{L}(x,\nu)&=2x^TP+A^T\lambda+C^T\nu=0\\
\end{array}
$$

`inf` 를 통해서 x를 구하겠습니다.
$$
\\x=-\frac{1}{2}P^{-1}(A^T\lambda-C^T\nu)\\
\mathcal{L}(x,\lambda,\nu)=(x^TP+A^T\lambda+C^T\nu)^Tx-b^T\lambda-d^T\nu
$$

$$
\mathcal{L}(x,\lambda,\nu)=((-\frac{1}{2}P^{-1}(A^T\lambda-C^T\nu))^TP+A^T\lambda+C^T\nu)^T(-\frac{1}{2}P^{-1}(A^T\lambda-C^T\nu))-b^T\lambda-d^T\nu\\
=\frac{1}{2}(A^T\lambda+C^T\nu)^T(-\frac{1}{2}P^{-1}(A^T\lambda-C^T\nu))-b^T\lambda-d^T\nu\\
=-\frac{1}{4}\lambda^TAP^{-1}A^T\lambda-b^T\lambda
$$

위 설명중에서 nu, h(x)는 `inf` 과정에서 0으로 처리되어 생략가능한데요. 가급적 계산하고자 했습니다. 복잡한 부분에서 불필요했기에 제거했으나, 처음부터 제거하셔도 됩니다. 끝으로 정리하겠습니다.
$$
\text{Dual problem}\\
\begin{array}{l}
\max\quad -\frac{1}{4}\lambda^TAP^{-1}A^T\lambda-b^T\lambda\\
s.t. \quad \lambda\ge0
\end{array}
$$
