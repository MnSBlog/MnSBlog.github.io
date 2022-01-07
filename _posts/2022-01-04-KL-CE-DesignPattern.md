---
date: 2022-01-04 21:28:00
layout: post
title: GoF Design Pattern
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



# <span style="color:#2E64FE">Design Pattern</span>

[휠 그림]

**"Don't reinvent the wheel."**

제가 살면서 처음으로 리팩토링(`Refactoring`)을 시작할 때 전해들은 유명한 말입니다.

객체 지향 프로그래밍(`Object-Oriented Programming`)은 구조적으로 잘 설계를 한다면, 결합도(`Coupling`)를 낮게, 응집도(`Cohesion`)는 높게 만들 수 있으니 처음부터 잘 생각해서 프로그램을 설계하라는 말을 딱 한마디로 얘기하면 *휠을 재발명 하지마라* 가 됩니다.

오늘 내용의 디자인 패턴(`Design Pattern`)은 객체 지향 프로그래밍에서 쓰면 좋은 품질을 제공하는 템플릿을 얘기할 수 있습니다. 일부러 자신의 지식을 자랑하고자 복잡하게 설계한 오버 엔지니어링과 빠른 구현을 위해 불 필요한 반복이 난무하는 언더 엔지니어링 사이의 적절한 수위를 맞춰주기도 합니다.



## Features

- 공통의 언어로서 원활한 소통을 제공
- 공통된 설계 문제에 대한 솔루션을 제공

---

[고민하는 사진]

디자인 패턴은 설계 과정을 포함하여 유지보수까지 소프트웨어 엔지니어간 소통을 원활하게 해줍니다. 어떤 문제(`Problem`)가 발생하는 여러 상황(`Context`)를 어떻게 해결(`Solution`)할 수 있을 지에 대해 **디자인 패턴의 무슨 모델을 쓰면 된다**로 간단히 회의를 끝낼 수 있죠.

[Context, Problem, Solution 다이어그램]



디자인 패턴은 정말로 많은 방법들이 있습니다. 그래서 오늘 얘기할 내용은  *Erich Gamma, Richard Helm, Ralph Johnson, Hohn Vissides*(`GoF: Gang of Fout`) 가 정의한 디자인 패턴을 얘기합니다. GoF 디자인 패턴에는 크게 세 가지로 나뉩니다.

| 생성 패턴(Creational Pattern)                                | 구조 패턴(Structural Pattern)                                | 행위 패턴(Behavioral Pattern)                                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| - 추상 팩토리(Abstract Factroy)<br />- 빌더(Builder)<br />- 팩토리 메소드(Factory Methods)<br />- 프로토 타입(Prototype)<br />- 싱글톤(Singleton) | - 어댑터(Adapter)<br />- 브릿지(Bridge)<br />- 컴퍼지트(Composite)<br />- 데코레이터(Decorator)<br />- 퍼사드(Facade)<br />- 플라이웨이트(Flyweight)<br />- 프록시(Proxy) | - 책임 사슬(Chain of Responsibility)<br />- 커맨드(Command)<br />- 인터프리터(Interpreter)<br />- 반복자(Iterator)<br />- 미디에이터(Mediator)<br />- 메멘토(Memento)<br />- 옵저버(Observer)<br />- 상태(State)<br />- 전략(Strategy)<br />- 템플릿 메소드(Templete method)<br />- 방문자(Visitor) |



**아래 포스팅 이미지 출처는 모두 GoF Design Pattern Reference Card([Jason S. McDonald](http://www.McDonaldLand.info))입니다.**

[**생성패턴(Creational Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern1/)

[**구조패턴(Structural Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern2/)

[**행위패턴(Behavioral Pattern)**](https://mnsblog.github.io/KL-CE-DesignPattern3/)
