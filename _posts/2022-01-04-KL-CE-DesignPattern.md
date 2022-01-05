---
date: 2021-11-10 21:28:00
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
| - 추상 팩토리(Abstract Factroy)<br />- 빌더(Builder)<br />- 팩토리 메소드(Factory Methods)<br />- 프로토 타입(Prototype)<br />- 싱글톤(Singleton) | - 어댑터(Adapter)<br />- 브릿지(Bridge)<br />- 컴퍼지트(Composite)<br />- 데코레이터(Decorator)<br />- 퍼사드(Facade)<br />- 플라이웨이트(Flyweight)<br />- 프록시(Proxy) | - 책임 연쇄(Chain of Responsibility)<br />- 커맨드(Command)<br />- 인터프리터(Interpreter)<br />- 이터레이터(Iterator)<br />- 미디에이터(Mediator)<br />- 메멘토(Memento)<br />- 옵저버(Observer)<br />- 상태(State)<br />- 전략(Strategy)<br />- 템플릿 메서드(Templete method)<br />- 방문자(Visitor) |



**아래 이미지 출처는 모두 GoF Design Pattern Reference Card([Jason S. McDonald](http://www.McDonaldLand.info))입니다.**

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



# <span style="color:#2E64FE">Structural Pattern</span>

구조 패턴은 클래스와 객체를 아우르는 패턴이며 조합을 하거나 흩어진 인터페이스를 합치거나 기능적으로 개선하는 것에 목적을 두고 있습니다.

### 어댑터(Adapter)

![6_Adaptor](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\6_Adaptor.png)

어댑터는 주로 인터페이스 호환성을 위해 쓰이며 인터페이스간 연결을 해주거나 그러면서 클래스를 재활용합니다. Adaptee는 변환된 메소드를 담고 있습니다.

예제

```c++

```



### 브릿지(Bridge)

![7_Bridge](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\7_Bridge.png)

브릿지는 추상부분을 분리하여 결합도를 낮추는데에 목적을 둡니다. 다양한 독립적 클래스를 만드는데 이래서 한 단계 상위 개념으로 이어주는 브릿지 느낌입니다.

예제

```c++

```



### 컴퍼지트(Composite)

![8_Composite](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\8_Composite.png)

전체-부분을 계층적으로 표현할때 사용하는 객체인데, 사용하는 입장에서는 계층적인 느낌을 받지않도록 동일한 인터페이스로 작용가능합니다. Component는 Leaf와 Composite 클래스에 공통 인터페이스로 동작하고 Composite 클래스가 전체 클래스입니다. 그래서 복수의 Component를 가질 수 있습니다.

```c++

```

 

### 데코레이터(Decorator)

![9_Decorator](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\9_Decorator.png)

데코레이터는 기능을 동적으로 유연하게 확장함에 중점을 두고 있습니다.

### 퍼사드(Facade)

![10_Facade](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\10_Facade.png)

### 플라이웨이트(Flyweight)

![11_Flyweight](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\11_Flyweight.png)

### 프록시(Proxy)

![12_Proxy](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\12_Proxy.png)

# <span style="color:#2E64FE">Behavioral Pattern</span>

### 책임 연쇄(Chain of Responsibility)

![13_CoR](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\13_CoR.png)

### 커맨드(Command)

![14_Command](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\14_Command.png)

### 인터프리터(Interpreter)

![15_Interpreter](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\15_Interpreter.png)

### 이터레이터(Iterator)

![16_Iterator](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\16_Iterator.png)

### 미디에이터(Mediator)

![17_Mediator](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\17_Mediator.png)

### 메멘토(Memento)

![18_Memento](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\18_Memento.png)

### 옵저버(Observer)

![19_Observer](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\19_Observer.png)

### 상태(State)

![20_State](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\20_State.png)

### 전략(Strategy)

![21_Strategy](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\21_Strategy.png)

### 템플릿 메서드(Templete method)

![22_Templete method](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\22_Templete method.png)

### 방문자(Visitor)

![23_Visitor](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\23_Visitor.png)
