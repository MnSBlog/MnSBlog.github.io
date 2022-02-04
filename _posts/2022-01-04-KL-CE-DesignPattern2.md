---
date: 2022-01-04 21:28:00
layout: post
title: Structural Pattern(Design Pattern)
subtitle: Understanding GoF's Design Pattern
description: Understanding GoF's Design Pattern
image: https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/6_Adaptor.png
category: Knowledge
tags:
  - Basic
  - Computer Engineering
  - OOP
author: 안상현
---

[**생성패턴(Creational Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern1/)

[**행위패턴(Behavioral Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern3/)

# <span style="color:#2E64FE">Structural Pattern</span>

구조 패턴은 클래스와 객체를 아우르는 패턴이며 조합을 하거나 흩어진 인터페이스를 합치거나 기능적으로 개선하는 것에 목적을 두고 있습니다.

### 어댑터(Adapter)

![6_Adaptor](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/6_Adaptor.png)

어댑터는 주로 인터페이스 호환성을 위해 쓰이며 인터페이스간 연결을 해주거나 그러면서 클래스를 재활용합니다. Adaptee는 변환된 메소드를 담고 있습니다.

예제

```c++

```



### 브릿지(Bridge)

![7_Bridge](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/7_Bridge.png)

브릿지는 추상부분을 분리하여 결합도를 낮추는데에 목적을 둡니다. 다양한 독립적 클래스를 만드는데 이래서 한 단계 상위 개념으로 이어주는 브릿지 느낌입니다.

예제

```c++

```



### 컴퍼지트(Composite)

![8_Composite](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/8_Composite.png)

전체-부분을 계층적으로 표현할때 사용하는 객체인데, 사용하는 입장에서는 계층적인 느낌을 받지않도록 동일한 인터페이스로 작용가능합니다. Component는 Leaf와 Composite 클래스에 공통 인터페이스로 동작하고 Composite 클래스가 전체 클래스입니다. 그래서 복수의 Component를 가질 수 있습니다.

```c++

```

 

### 데코레이터(Decorator)

![9_Decorator](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/9_Decorator.png)

데코레이터는 기능을 동적으로 유연하게 확장함에 중점을 두고 있습니다. 기본 기능을 유지한 채로, 제가 필요한 기능들을 붙여서 사용합니다. 데코레이터는 참조로서 주고받는 동적 컴포지션(`Dynamic Composition`), 템플릿을 이용한 정적 컴포지션(`Static Composition`)이 있습니다. 더 나아가 특정 함수에 다른 동작을 합성하는 함수형 컴포지션(`Functional Composition`)이 있습니다.

예제

```c++

```



### 퍼사드(Facade)

![10_Facade](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/10_Facade.png)

퍼사드는 건물의 정면을 의미합니다. 여러 복잡한 시스템에서 눈으로 보여지는 부분을 담당합니다. 복잡한 서브 시스템 앞에 단순한 인터페이스를 두는 용도입니다.

예제

```c++

```



### 플라이웨이트(Flyweight)

![11_Flyweight](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/11_Flyweight.png)

잘게 쪼개져 있는 많은 비슷한 기능을 가진 객체들을 핸들링할때 사용합니다. 다만 이 패턴에서 설명하는 '많은'을 잘못이해하면 비효율적인 패턴이 됩니다. 그러니 해당 내용도 아래에 설명하겠습니다.

일반적인 예제

```c++

```

 비효율의 예제

특정 부분을 대문자로 변경하는 기능을 플라이웨이트로 구성해보겠습니다. 특정 부분은 범위로서 시작과 끝 단을 표시해도 되는데 플라이웨이트로 Fine grained로 억지로 변환하다보니 낭비가 생깁니다.

```c++

```



### 프록시(Proxy)

![12_Proxy](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/12_Proxy.png)

프록시는 데코레이터처럼 확장의 개념에 중점을 둡니다. 다만, 내부에서 다르게 돌아가죠. 프록시를 가장 잘 활용가능한 것은 속성 기능을 구현한다던가, 적절한 포인터를 반환하는 방식입니다.

예제

```c++

```

