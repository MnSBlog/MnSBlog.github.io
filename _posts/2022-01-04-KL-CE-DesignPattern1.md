---
date: 2022-01-07 22:28:00
layout: post
title: Creational Pattern(Design Pattern)
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

[**구조패턴(Structural Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern2/)

[**행위패턴(Behavioral Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern3/)

# <span style="color:#2E64FE">Creational Pattern</span>

생성 패턴은 객체(`Object`)를 생성할 때 쓰입니다. 생성 패턴의 주요 포인트는 캡슐화(`Encapsulation`)입니다.

### 추상 팩토리(Abstract Factory)

![1_Abstract factory](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\1_Abstract factory.png)

추상 팩토리는 연관되거나 종속된 객체들을 묶어서 팩토리 클래스를 정의하고 해당하는 조건에 맞춰서 객체를 생성하는 패턴입니다. 여기서 AbstractFactory는 공통 인터페이스로 동작하고 ConcreteFactory는 인터페이스를 오버라이드하여 구체적인 ProductA, B를 정의합니다. 마찬가지로 AbstractProduct도 추상 인터페이스, ConcreteProduct는 오버라이드합니다. 

예제

```c++

```



### 빌더(Builder)

![2_Builder](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\2_Builder.png)

복잡한 객체와 표현 객체를 분리하는 것이 핵심인 패턴입니다. 동일한 프로세스에도 다른 표현을 꾸릴 수 있습니다. ConcreteBuilder는 추상클래스 Builder를 구현하는 클래스입니다. 그래서 표현을 다양하게 할 수 있고, 생성과 표현이 분리되어 있으니 생성 절차를 세밀하게 쪼갤 수 있습니다.

예제

```c++

```



### 팩토리 메소드(Factory Methods)

![3_Factory method](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\3_Factory method.png)

팩토리 메소드는 객체 생성을 서브 클래스(ConcreteCreator)가 맡습니다. 분리된 만큼 다채로운 생성을 할 수 있는 장점이 있으나 규모에 따라 빈번한 중복이 생길 수 있습니다. Product는 팩토리 메소드의 공통 인터페이스로, ConcreteProduct가 구현을 담당합니다. Creator는 팩토리 **메소드**를 가지는 **클래스**이고 ConcreteCreator는 팩토리 메소드를 구현합니다.

예제

```c++

```



### 프로토 타입(Prototype)

![4_Ptrototype](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\4_Ptrototype.png)

프로토타입은 말 그대로 베이스를 가지고 있는 인스턴스로 필요한 기능을 붙인 인스턴스를 만드는 패턴입니다. 헷갈리지 마세요. **인스턴스**입니다. Prototype의 구조는 쉬워보이지만 예제를 봐야 정확한 이해를 할 수 있으니 예제를 봐주세요. 



### 싱글톤(Singleton)

![5_Singleton](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\5_Singleton.png)

싱글톤은 전역에서 참조가능한데도 하나만 생성되는 특징을 가지고 있습니다.

예제

```c++

```
