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

**생성패턴(Creational Pattern)**

**구조패턴(Structural Pattern)**

**행위패턴(Behavioral Pattern)**

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

데코레이터는 기능을 동적으로 유연하게 확장함에 중점을 두고 있습니다. 기본 기능을 유지한 채로, 제가 필요한 기능들을 붙여서 사용합니다. 데코레이터는 참조로서 주고받는 동적 컴포지션(`Dynamic Composition`), 템플릿을 이용한 정적 컴포지션(`Static Composition`)이 있습니다. 더 나아가 특정 함수에 다른 동작을 합성하는 함수형 컴포지션(`Functional Composition`)이 있습니다.

예제

```c++

```



### 퍼사드(Facade)

![10_Facade](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\10_Facade.png)

퍼사드는 건물의 정면을 의미합니다. 여러 복잡한 시스템에서 눈으로 보여지는 부분을 담당합니다. 복잡한 서브 시스템 앞에 단순한 인터페이스를 두는 용도입니다.

예제

```c++

```



### 플라이웨이트(Flyweight)

![11_Flyweight](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\11_Flyweight.png)

잘게 쪼개져 있는 많은 비슷한 기능을 가진 객체들을 핸들링할때 사용합니다. 다만 이 패턴에서 설명하는 '많은'을 잘못이해하면 비효율적인 패턴이 됩니다. 그러니 해당 내용도 아래에 설명하겠습니다.

일반적인 예제

```c++

```

 비효율의 예제

특정 부분을 대문자로 변경하는 기능을 플라이웨이트로 구성해보겠습니다. 특정 부분은 범위로서 시작과 끝 단을 표시해도 되는데 플라이웨이트로 Fine grained로 억지로 변환하다보니 낭비가 생깁니다.

```c++

```



### 프록시(Proxy)

![12_Proxy](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\12_Proxy.png)

프록시는 데코레이터처럼 확장의 개념에 중점을 둡니다. 다만, 내부에서 다르게 돌아가죠. 프록시를 가장 잘 활용가능한 것은 속성 기능을 구현한다던가, 적절한 포인터를 반환하는 방식입니다.

예제

```c++

```



# <span style="color:#2E64FE">Behavioral Pattern</span>

### 책임 사슬(Chain of Responsibility)

![13_CoR](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\13_CoR.png)

시스템을 구성하는 여러 다른 컴포넌트들이 역할에 따라 메시지를 주고받으며 처리하는 패턴입니다. 다만 어떤 처리를 할지 관리하는 인터페이스가 존재합니다. 즉 작업을 차례로 처리할 수 있는 단순한 패턴입니다.

예제

```c++

```



### 커맨드(Command)

![14_Command](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\14_Command.png)

어떤 객체를 활용할 때 작업 내용을 보내는 방식입니다. 전형적으로 알고리즘을 전달하는 방식으로 볼 수 있습니다.

예제

```c++

```



### 인터프리터(Interpreter)

![15_Interpreter](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\15_Interpreter.png)

굉장히 다양하게 사용되는 인터프리터 패턴(많이 사용하진 않음)은 입력을 기능적으로 해석하는데에 중점을 두고 있습니다. 이는 여러 예제로서 설명하겠습니다.

예제

```c++

```



### 반복자(Iterator)

![16_Iterator](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\16_Iterator.png)

반복자는 위 인터프리터와 다르게 상당히 많이 사용하고 있습니다. 링크드 리스트처럼 다음 요소로 접근하는 방법을 통해 순회하는 것이죠. 이 내용을 보기전에 많이 사용했던 경험들이 있을겁니다.

예제

```c++

```



### 미디에이터(Mediator)

![17_Mediator](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\17_Mediator.png)

컴포넌트끼리 커뮤니케이션을 도와주는 패턴이며 컴포넌트 모두에게 접근 가능한 전역 정적 변수로 구성되어 있습니다.

예제

```c++

```



### 메멘토(Memento)

![18_Memento](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\18_Memento.png)

메멘토를 사전적 용의로 보기보다는 영화 '메멘토'가 더 지금 패턴 성격과 어울립니다. 메멘토는 10분짜리 기억력을 가진 남자의 이야기죠. 메멘토 패턴은 특정 시점의 시스템 상태를 Memento 클래스에 저장하여 리턴합니다. 순수한 읽기전용의 클래스이며 별다른 액티비티는 없습니다. 

예제

```c++

```



### 옵저버(Observer)

![19_Observer](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\19_Observer.png)

중요한 패턴 중 하나이며 아주 자주 쓰입니다. C#에서는 표준라이브러리로 제공하고 있습니다. 이 패턴은 특정 정보를 모니터링하여 커뮤니케이션에 쓸 수도 있고 이를 알림형태로 처리할 수 있습니다. 또한 이 알림 수신은 병렬형태로 복수의 수신이 가능합니다.

예제

```c++

```



### 상태(State)

![20_State](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\20_State.png)

현 상태가 동작을 제어함으로서 상태는 바뀔 수 있다는 아이디어로 단순한 방식입니다.

예제

```c++

```



### 전략(Strategy)

![21_Strategy](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\21_Strategy.png)

출력형태를 유연하게 바꿔주는 패턴입니다. 알고리즘의 뼈대를 정의하는 Strategy 인터페이스, 그 세부 전략들을 바꿔 구현합니다.

예제

```c++

```



### 템플릿 메소드(Templete method)

![22_Templete method](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\22_Templete method.png)

전략 패턴과 가장 유사하나 템플릿 메소드는 상속을 이용합니다. 구조적인 차이말고 기능자체는 골격을 마련하여 상세하게 구현하는 것은 동일합니다.

예제

```c++

```



### 방문자(Visitor)

![23_Visitor](D:\MnS\발표자료\Seminar\Computer Engineering\Design Pattern card\23_Visitor.png)

이 디자인 패턴은 어떤 객체의 계층마다 서로 다른 작업을 하는 경우에 쓰입니다. 

예제

```c++

```

