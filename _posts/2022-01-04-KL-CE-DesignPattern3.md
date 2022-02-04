---
date: 2022-01-04 21:28:00
layout: post
title: Behavioral Pattern(Design Pattern)
subtitle: Understanding GoF's Design Pattern
description: Understanding GoF's Design Pattern
image: https://drive.google.com/file/d/1cviYyQgeBiA9i9dNiDAQ8AMkD8jFr0xw/view?usp=sharing
category: Knowledge
tags:
  - Basic
  - Computer Engineering
  - OOP
author: 안상현
---

[**생성패턴(Creational Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern1/)

[**구조패턴(Structural Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern2/)

# <span style="color:#2E64FE">Behavioral Pattern</span>

### 책임 사슬(Chain of Responsibility)

![13_CoR](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/13_CoR.png)

시스템을 구성하는 여러 다른 컴포넌트들이 역할에 따라 메시지를 주고받으며 처리하는 패턴입니다. 다만 어떤 처리를 할지 관리하는 인터페이스가 존재합니다. 즉 작업을 차례로 처리할 수 있는 단순한 패턴입니다.

예제

```c++

```



### 커맨드(Command)

![14_Command](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/14_Command.png)

어떤 객체를 활용할 때 작업 내용을 보내는 방식입니다. 전형적으로 알고리즘을 전달하는 방식으로 볼 수 있습니다.

예제

```c++

```



### 인터프리터(Interpreter)

![15_Interpreter](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/15_Interpreter.png)

굉장히 다양하게 사용되는 인터프리터 패턴(많이 사용하진 않음)은 입력을 기능적으로 해석하는데에 중점을 두고 있습니다. 이는 여러 예제로서 설명하겠습니다.

예제

```c++

```



### 반복자(Iterator)

![16_Iterator](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/16_Iterator.png)

반복자는 위 인터프리터와 다르게 상당히 많이 사용하고 있습니다. 링크드 리스트처럼 다음 요소로 접근하는 방법을 통해 순회하는 것이죠. 이 내용을 보기전에 많이 사용했던 경험들이 있을겁니다.

예제

```c++

```



### 미디에이터(Mediator)

![17_Mediator](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/17_Mediator.png)

컴포넌트끼리 커뮤니케이션을 도와주는 패턴이며 컴포넌트 모두에게 접근 가능한 전역 정적 변수로 구성되어 있습니다.

예제

```c++

```



### 메멘토(Memento)

![18_Memento](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/18_Memento.png)

메멘토를 사전적 용의로 보기보다는 영화 '메멘토'가 더 지금 패턴 성격과 어울립니다. 메멘토는 10분짜리 기억력을 가진 남자의 이야기죠. 메멘토 패턴은 특정 시점의 시스템 상태를 Memento 클래스에 저장하여 리턴합니다. 순수한 읽기전용의 클래스이며 별다른 액티비티는 없습니다. 

예제

```c++

```



### 옵저버(Observer)

![19_Observer](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/19_Observer.png)

중요한 패턴 중 하나이며 아주 자주 쓰입니다. C#에서는 표준라이브러리로 제공하고 있습니다. 이 패턴은 특정 정보를 모니터링하여 커뮤니케이션에 쓸 수도 있고 이를 알림형태로 처리할 수 있습니다. 또한 이 알림 수신은 병렬형태로 복수의 수신이 가능합니다.

예제

```c++

```



### 상태(State)

![20_State](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/20_State.png)

현 상태가 동작을 제어함으로서 상태는 바뀔 수 있다는 아이디어로 단순한 방식입니다.

예제

```c++

```



### 전략(Strategy)

![21_Strategy](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/21_Strategy.png)

출력형태를 유연하게 바꿔주는 패턴입니다. 알고리즘의 뼈대를 정의하는 Strategy 인터페이스, 그 세부 전략들을 바꿔 구현합니다.

예제

```c++

```



### 템플릿 메소드(Templete method)

![22_Templete method](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/22_Templete method.png)

전략 패턴과 가장 유사하나 템플릿 메소드는 상속을 이용합니다. 구조적인 차이말고 기능자체는 골격을 마련하여 상세하게 구현하는 것은 동일합니다.

예제

```c++

```



### 방문자(Visitor)

![23_Visitor](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/23_Visitor.png)

이 디자인 패턴은 어떤 객체의 계층마다 서로 다른 작업을 하는 경우에 쓰입니다. 

예제

```c++

```

