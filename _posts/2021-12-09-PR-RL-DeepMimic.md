---
date: 2021-11-10 21:28:00
layout: post
title: Design Luxury reward function in Reinforcement Learning
subtitle: Review paper X. B. Peng's paper 'Deep Mimic' about Reinforcement Learning
description: Review paper X. B. Peng's paper 'Deep Mimic' about Reinforcement Learning
image: https://drive.google.com/file/d/1cviYyQgeBiA9i9dNiDAQ8AMkD8jFr0xw/view?usp=sharing
category: Paper Review
tags:
  - Reinforcement Learning
  - ACM
  - SCI&SCIE
author: 안상현
---



# ReadMe

 강화학습은 `Reward Function`을 잘 설계하는 것이 큰 영향을 줍니다. 이 논문(`Deep Mimic`)은 인간의 행동을 모방하는 모델들에게 보상을 어떻게 주는지, 어떤 결과를 가져오는 지에 대한 설명을 합니다. 결론적으로 `Luxury reward function` 은 `agent` 에게 `valuable experience(or exploration)` 을 제공합니다. 이 포스팅은 논문을 한글로 번역, 재구성했기에 아래 논문의 모든 내용을 **제공하지 않습니다.**

<span style="color:#FF2020">**X. B. Peng, P. Abbeel, S. Levine, and M. van de Panne, “DeepMimic,” *ACM Transactions on Graphics*, vol. 37, no. 4. Association for Computing Machinery (ACM), pp. 1–14, 10-Aug-2018.**</span>

# <span style="color:#2E64FE">SUMMARY</span>

캐릭터 애니메이션의 오랜 목표는 물리 기반의 시스템에서 돌아가는 행동 특징들을 `Data-driven`으로서 합치는 겁니다. 이런 환경은  가능한 운동과 근육들 중에서 가장 좋은 행동이 연속적으로 이뤄집니다. 그래서 이 논문의 목표는 가장 완전한 시퀀스를 찾아 모션을 잘 모방하는 모델을 만드는 것입니다. 우리는 잘 알려진 강화학습 알고리즘을 이용해서, 여러 모션들에 대한 강건한 제어 정책(`policies`)이 만들어지는 것을 보여줍니다. 모션의 종류에는 `walking`, `flip`, `spin` 등으로 다양하게 구성했고 캐릭터 또한 다양하게 `human`, `atlas robot`, `bipedal dinosaur`, `dragon` 으로 구성했니다. 

#physics-based character animation #motion control #reinforcement learning

# <span style="color:#2E64FE">INTRODUCTION</span>

 이 논문에서 강화학습(`RL, Reinforcment Learning`)은 시행착오를 통해 모션을 만들어내는데 쓰입니다. 강화학습의 에이전트(`agent`)에 딥러닝을 적용한 것을 `Deep RL` 이라 불리는데  이를 이용하여 복잡한 행동들에 대한 접근은 기존 연구에도 있습니다. 물리 기반 시뮬레이션에 컨트롤러를 이용한 강화학습은 액션(`action`)과 상태(`state`, `observation`)가 상당히 커서 도전적입니다.

 이상적인 학습 기반 애니메이션 시스템은 `artist`와 `actor` 에게 모션을 참조할 수 있어야하고 목표를 확실히하여 목표지향적으로 설계하고 참조 모션은 물리적인 실제 행동으로서 만들어져야합니다. 그래서 저희는 행동에 대한 지연없이 보상을 제공하고, 별개로 추가적인 목적도 달성했는지에도 보상을 제공합니다. 저희는 모션들의 멀티클립(`multi-clip`)에 대한 컨트롤러 구성으로 세 가지 방법들을 증명했습니다. 첫 번째는 멀티클립 보상을 `max operator` 를 기반으로 학습을 시키는 것이고, 두 번째사용자로부터 반응하는 다양한 스킬들의 성능을 올려주는 `policy`를 학습시키는 것, 마지막은 싱글 클립으로 구성된 멀티플 행동 시퀀스를 가치 함수(`value function`)로 만드는 것입니다.

 이 논문의 중심 `contribution` 은 데이터로 목표지향적 강화학습과 합쳐진 물리기반 캐릭터 애니메이션에 대한 프레임워크입니다. 이는 아마 모션 캡쳐 클립 또는 `keyframed` 애니메이션의 폼으로 제공할 수 있습니다. 

# <span style="color:#2E64FE">RELATED WORK</span>

 로봇제어, 모션제어, 강화학습에 대해 관심있는 분들은 아래 연구들을 참고하셨으면 좋겠습니다.

## Kinematic Models

 운동학(`Kinematic`) 은 캐릭터 애니메이션이 계속 지속되는 특징이 있는만큼 데이터의 규모가 클수록, 효과적입니다. `Kinematic model`은 보통 모션 클립의 데이터셋이 주어지면, 컨트롤러는 상황에 맞는 동작을 위한 적합한 클립을 선택하는 용으로 만들어집니다. 관련 연구로는 `Agrawal and Van de Panne 2016; Lee et al. 2010b; Safonova and Hodgins 2007` 이 있습니다.

 가우시안 프로세스(`GP: Gaussian Process`)를 이용하여 `Eigen value` 형태의 `Orthogonal`한 히든 밸류를 통해 모션들을 통합한 연구도 있습니다. `Levine et al. 2012; Ye and Liu 2010b` 이 연구는 딥러닝 모델을 적용한 확장 연구도 있는데요. 예를 들어, `autoencoder`를 적용한 모델, `phasefunctioned networks`를 생성모델에 적용했습니다. 이는 `Holden et al. 2017, 2016` 을 참고해주세요.

 고품질의 데이터를 이용한 방법론도 있습니다. 새로운 시뮬레이션은 행동들을 통합하는데 있어서 제한적이지만, 행동과 환경들이 복잡한 연속 환경에서는 피저블한 행동들을 빠르게 수집하는 것이 중요합니다. 그래서 사전지식을 이용하여 앞으로의 적절한 행동예측을 만드는 것이 하나의 해결법입니다. 당장 눈에 보이는 모든 데이터들을 다 담는 것보다 좋을 수 있겠죠. `DISCUSSION` 에서 후술하겠습니다.

## Physics-based Models

캐릭터를 제어하는 컨트롤러를 디자인하는 것은 여전히 도전문제로 남아 있습니다. 보통은 전문가들의 역량에 의지하여 구현됩니다. 부분적으로 `Locomotion` 은 강건한 컨트롤러 디자인한 연구성과가 있습니다. 사람 모델을 쓰기도 사람이 아닌 모델도 있죠. `Coros et al. 2010; Ye and Liu 2010a; Yin et al. 2007` 입니다. 궤적 최적화에 대한 연구도 참고해주세요. `Mordatch et al. 2012; Wampler et al. 2014` 저희는 사전에 단일 `model-free` 프레임워크에서 넓은 범위의 모션 스킬들에 접근한 적이 있습니다. 예를 들면 `Walks, Kicks, Flips` 등을 말이죠. 모션을 모방하는 것과 그런 모션에 대한 요구로는 컴팩트하고 빠른 제어를 할 수 있는 `policies` 가 있습니다. 행동에 대한 데이터는 높은 차원의 `state` 와 `observation` 입니다.

## Reinforcement Learning

 캐릭터 애니메이션 컨트롤러를 개발하기 위한 많은 최적화 테크닉으로는 강화학습을 주로 사용합니다. 강화학습의 한 방법인 `Value Iteration`을 이용한 연구는 태스크가 주어지면 컨트롤러를 통해 모션 시퀀스를 만든 연구가 있습니다. `Lee et al. 2010b; Levine et al. 2012` 유사한 접근법으로는 `Coros et al. 2009; Peng et al. 2105`가 있습니다. 근데 이는 최근연구가 아니기에 좀 더 최근으로 다가가면 `Deep neural network` 를 이용한 RL 모델이 있습니다. `Brockman et al. 2016a; Duan et al. 2016; Liu and Hodgines 2017; Peng et al. 2016; Rajeswaran et al. 2017; Teh et al. 2017`을 참고해주세요. 또 다른 강화학습의 한 방법인 `Policy iteration` 혹은 `Policy gradient method` 는  연속 제어 문제에 대한 선택의 알고리즘으로서 생겨났습니다. `Schulman et al. 2015a, 2017; Sutton and Barto 1998` 이를 이용한 연구는 `Merel et al. 2017; Schulman et al. 2015b` 를 참고하시고 자연 현상에 대한 `Reward function design`은 `Lee et al. 2014; Wang et al. 2012`가 있습니다.  또 최근에 모션캡처를 모방하는 `GAIL(Ho and Ermon 2016)` 도 참고해주세요. `DeepLoco(Peng et al. 2107a)` 본 논문과 유사한 연구입니다. 

## Motion Imitation

 어떤 모션을 모방하는 것은 역사적으로 오래됐습니다. `Planer Character`를 이용한 `bipedal locomotion`의 연구는 `Sharon and van de Panne 2005; Sok et al. 2007` 이 있습니다. `Model based` 방법과 `Policy search` 를 쓴 3D humanoid 연구는 `Lee et al. 2010a; Muico et al. 2009; Yin et al. 2007` 이 있습니다. `Reward function`을 적용한 `Deep RL`의 시도는 `Peng et al. 2017a, b` 이며, 이 논문에서는 더 어려운 동작들에 대해서 시도했고 두 중요성을 알게 됐습니다. 초기 상태와 학습 에피소드의 조기 종료의 중요성을 이 연구를 통해 알게됐습니다.

 사전지식을 이용한 컨트롤러 설계의 좋은 예시는 `Sampling-Based Controller(SAMCON)` 으로 `Liu et al. 2016, 2010` 을 참고해주시고 이에 대한 확장 연구로는 `Liu and Hodgins 2017`을 참고해주세요.

# <span style="color:#2E64FE">OVERVIEW</span>

저희가 구현한 시스템은 레퍼런스 모션과 일치하는 캐릭터 모델을 입력으로 하고 `Reward function` 을 통한 Task를 정의합니다. 참조 모션을 모방하기위한 컨트롤러를 붙입니다. 컨트롤러는 PID 제어중에 PD제어(`Proportional-Derivative`)를 사용합니다.이 논문에서 사용된 `Terminologies` 는 아래와 같습니다.


$$
\text{a sequence of target poses: }\hat{q_t}\\
\text{A control policy: } \pi(a_t|s_t,g_t)\\
\text{Character state: } s_t,\ \text{a task-specific goal: }g_t, \text{and action: } a_t\\
$$


`Reward` 는 분할된 수식으로서 모방 점수(
$$
r^I(s_t,\ a_t)
$$
)와 태스크 목표 점수(
$$
r^G(s_t,\ a_t,\ g_t)
$$
를 받습니다.

끝으로 에이전트 학습은 `Neural networks` 와 `Proximal policy optimization algorithm` 을 이용했습니다. 이 구조를 채택함에 있어서 `Schulman et al. 2017` 을 참고했습니다.

# <span style="color:#2E64FE">BACKGROUND</span>

 가장 먼저, 이 연구에서 가장 일반적인 강화학습을 설계했습니다. 최대 보상(`Reward`)을 이끌어내는 `Policy`로 인해 `Agent`가 어떤 `action`을 하고 그로 인해 환경(`Environment`)과 상호작용을 합니다. 간결함을 위해서 `Terminology` 를 정리했습니다. 가장 기본적인 목표(
$$
\text{goal }g,
$$
), 그리고 `Policy`는 
$$
\pi(a|s)
$$
models로, 조건부 분포입니다. 이런 조건부 분포를 설명할 때는
$$
a \in A \text{ given a state } s \in S
$$
라고 말합니다. 이는 매 컨트롤러에서 나오는 그 순간 타임스텝에 대한 단일 액션입니다. 이게 꾸준히 이어진다면 시퀀스죠. 또한 `agent`는 현재 `state`를 알 수 있고 `Policy`로 부터 `action`을 얻습니다. 그러면 상호작용을 통해서 `Environment`는 새로운 `state`(
$$
s'=s_{t+1}
$$
)을 가져옵니다. 그리고 `Environment`의 상호작용은 받아온 `action`과  현재 `state`를 이용하여 역학을 반영한 동작을 하고 `reward`(
$$
r_t
$$
)를 추산합니다. 파라미터가 반영된 `Policy`는 
$$
\pi_\theta(a|s)
$$
 로 표현하며, 강화학습의 목적은 `Expected return`을 최대가 되도록 최적화된 파라미터(
$$
\theta^*
$$
)를 학습시키는 것입니다.


$$
\text{Expected Return }J(\theta)=\mathbb{E}_{\tau\sim p_\theta(\tau)}\left[\sum^T_{t=0}\gamma^tr_t\right]
$$


순서대로 봅시다. 가장 먼저, `parameter`에 의한 행동 확률은


$$
p_\theta(\tau)=p(s_0)\prod_{t=0}^{T-1}p(s_{t+1}|s_t,\ a_t)\pi_\theta(a_t|s_t)
$$


위 처럼 나옵니다. 정책
$$
\pi_\theta
$$
으로부터 가능한 모든 궤적을 
$$
\tau=(s_0,\ a_0, s_1,\dots,\ a_{T-1},\ s_T)
$$
라고 볼 수 있습니다. 그리고 가장 초기 `state` 분포는 
$$
p(s_0)
$$
라고 표현하구요. 그리고 `Expected` 안에 있는 
$$
\left[\sum_{t=0}^T\gamma^tr_t\right]
$$
 식은 모든 궤적에 대한 시간 흐름으로 받는 `return` 값 입니다. 그런데 여기서 `T`는 강화학습 환경에서 Open-end식 끝이 없는 상황도 염두해야하고, 미래에 대한 믿음으로 사용하는 discount factor 
$$
\gamma \in [0,\ 1]
$$
 도 어떤 값으로 설정할지 고려해야 합니다.



여기서 유명한 방법론이 하나가 있는데요. `gradient method`를 `policy`에 적용한 `Sutton et al. 2001`의 연구가 있습니다. Expected return의 기울기 
$$
\nabla_\theta J(\theta)
$$
는 `Policy`를 따르는 궤적 샘플을 예측할 수 있는 건데요. 전체적인 식 구성은 아래와 같습니다.


$$
\nabla_\theta J(\theta)=E_{s_t\sim d_\theta(s_t),a_t\sim \pi_\theta(a_t|s_t)}\left[\nabla_\theta\log(\pi_\theta(a_t|s_t))\mathcal{A_t}\right]
$$


식이 조금 복잡해졌는데, 아까처럼 천천히 풀어나갑시다. 먼저 
$$
d_\theta(s_t)
$$
는 
$$
\pi_\theta
$$
 를 기반으로 한 `state`의 분포입니다. 그리고 
$$
\mathcal{A_t}
$$
는 t시점에 이뤄지는 `Advantage`라고 얘기하며 이를 좀 더 풀어서 표현하면 `Reward` - `Value function` 으로 볼 수 있습니다.


$$
\mathcal{A_t}=R_t-V(s_t)
$$


여기서 `Advantage`에 들어가는 `Reward`는 
$$
R_t=\sum_{l=0}^{T-t}\gamma^lr_{t+1}
$$
입니다. 그리고 `Value function`은 
$$
V(s_t)=\mathbb{E}[R_t|\pi_\theta,\ s_t]
$$
로서 결국 진짜 `Reward`와 예상되는 `Reward`의 편차를 이용하여, 예상한 것보다 얼마나 더 좋은 결과를 가져왔는지 얘기합니다. 이러한 구조는 `generalized advantage estimator GAE, [Schulman et al. 2015b]`를 참고해주세요.

# <span style="color:#2E64FE">POLICY REPRESENTATION</span>

 위 `Background`의 설명에서 `Policy`가, 그 중에서도 `Parametric policy`가 얼마나 중요한지 말했습니다. 강화학습의 목적은 `Optimal parameter`를 찾는 것이라, `Poilicy`가 온전하고 강건하게 구현되어 있어야 합니다. 그래서 본 연구에서는 모션 크릷이 주어지면, 타겟 포즈의 시퀀스 
$$
\hat{q}_t
$$
를 표현합니다. 본 연구는 물리적 시뮬레이션 환경에서 요구하는 모션들을 그대로 따라하는 정책을 만드는 것이 목적입니다. 자연스레 어떤 추가적인 모션을 만족해야합니다. 

## States and Actions

`state`는 캐릭터의 몸통 설정을 설명합니다. 이게 다는 아니고, 각 포지션에 따른 연결관계의 특징들도 포함되며  4 방향씩 묶어서 회전이나, 선형, 곡선 움직임도 있습니다. 모든 특징들은 캐릭터의 로컬 좌표계에서 계산되어 이러한 연산 과정에서는 위상변수(`phase variable`)가 적용됩니다. 이는 
$$
\phi\in[0,\ 1]
$$
로 표현됩니다.사실 애니메이션 변수로 봐도 되는데, 모션이 시작되면 0이고 모션이 종료되면 1이 됩니다. 그래서 매 모션의 사이클마다 0으로 초기화 됩니다.

## Network

## Reward



# <span style="color:#2E64FE">TRAINING</span>

# <span style="color:#2E64FE">MULTI-SKILL INTEGRATION</span>

# <span style="color:#2E64FE">CHARACTERS</span>

# <span style="color:#2E64FE">TASKS</span>

# <span style="color:#2E64FE">RESULTS</span>

# <span style="color:#2E64FE">DISCUSSION AND LIMITATION</span>
