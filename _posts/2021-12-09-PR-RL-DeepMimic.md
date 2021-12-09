---
date: 2021-11-10 21:28:00
layout: post
title: Design Luxury reward function in Reinforcement Learning
subtitle: Review paper X. B. Peng's paper 'Deep Mimic' about Reinforcement Learning
description: Review paper X. B. Peng's paper 'Deep Mimic' about Reinforcement Learning
image: https://drive.google.com/uc?export=view&id=1cviYyQgeBiA9i9dNiDAQ8AMkD8jFr0xw
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

운동학(`Kinematic`)

## Physics-based Models

## Reinforcement Learning

## Motion Imitation

# <span style="color:#2E64FE">OVERVIEW</span>

# <span style="color:#2E64FE">BACKGROUND</span>

# <span style="color:#2E64FE">POLICY REPRESENTATION</span>

# <span style="color:#2E64FE">TRAINING</span>

# <span style="color:#2E64FE">MULTI-SKILL INTEGRATION</span>

# <span style="color:#2E64FE">CHARACTERS</span>

# <span style="color:#2E64FE">TASKS</span>

# <span style="color:#2E64FE">RESULTS</span>

# <span style="color:#2E64FE">DISCUSSION AND LIMITATION</span>
