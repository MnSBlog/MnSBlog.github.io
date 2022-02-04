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

![1_Abstract factory](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/1_Abstract factory.png)

추상 팩토리는 연관되거나 종속된 객체들을 묶어서 팩토리 클래스를 정의하고 해당하는 조건에 맞춰서 객체를 생성하는 패턴입니다. 여기서 AbstractFactory는 공통 인터페이스로 동작하고 ConcreteFactory는 인터페이스를 오버라이드하여 구체적인 ProductA, B를 정의합니다. 마찬가지로 AbstractProduct도 추상 인터페이스, ConcreteProduct는 오버라이드합니다. 

예제

```c++
struct HotDrink
{
  virtual ~HotDrink() = default;

  virtual void prepare(int volume) = 0;
};

struct Tea : HotDrink
{

  void prepare(int volume) override
  {
    cout << "Take tea bag, boil water, pour " << volume << "ml, add some lemon" << endl;
  }
};

struct Coffee : HotDrink
{
  void prepare(int volume) override
  {
    cout << "Grind some beans, boil water, pour " << volume << "ml, add cream, enjoy!" << endl;
  }
};
```

뜨거운 음료로는 차와 커피로 나눌 수 있습니다. 이를 준비할 때 두 경우는 다른 준비과정을 거치기에 나눕니다.

```c++
unique_ptr<HotDrink> make_drink(string type)
{
  unique_ptr<HotDrink> drink;
  if (type == "tea")
  {
    drink = make_unique<Tea>();
    drink->prepare(200);
  }
  else 
  {
    drink = make_unique<Coffee>();
    drink->prepare(50);
  }
  return drink;
}
```

준비과정은 이렇게 사용할 수 있겠죠. 그리고 차와 커피를 제조하는 것 또한 다른 방식으로 진행됩니다. 그러니 이것도 공용의 팩토리를 만들고 이를 상속받아 구현합니다.

```c++
struct HotDrinkFactory
{
  virtual unique_ptr<HotDrink> make() const = 0;
};
```

이렇게 공용 인터페이스를 만들고

```c++
struct CoffeeFactory : HotDrinkFactory
{
  unique_ptr<HotDrink> make() const override
  {
    return make_unique<Coffee>();
  }
};
```

공용 인터페이스를 상속받은 커피 팩토리와

```c++
struct TeaFactory : HotDrinkFactory
{
  unique_ptr<HotDrink> make() const override {
    return make_unique<Tea>();
  }
};
```

티 팩토리입니다.



### 빌더(Builder)

![2_Builder](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/2_Builder.png)

복잡한 객체와 표현 객체를 분리하는 것이 핵심인 패턴입니다. 동일한 프로세스에도 다른 표현을 꾸릴 수 있습니다. ConcreteBuilder는 추상클래스 Builder를 구현하는 클래스입니다. 그래서 표현을 다양하게 할 수 있고, 생성과 표현이 분리되어 있으니 생성 절차를 세밀하게 쪼갤 수 있습니다.

예제

```c++
struct HtmlBuilder
{
  HtmlBuilder(string root_name)
  {
    root.name = root_name;
  }

  // void to start with
  HtmlBuilder& add_child(string child_name, string child_text)
  {
    HtmlElement e{ child_name, child_text };
    root.elements.emplace_back(e);
    return *this;
  }

  // pointer based
  HtmlBuilder* add_child_2(string child_name, string child_text)
  {
    HtmlElement e{ child_name, child_text };
    root.elements.emplace_back(e);
    return this;
  }

  string str() { return root.str(); }

  operator HtmlElement() const { return root; }
  HtmlElement root;
};
```

HtmlBuilder는 HTML 구성 요소를 생성하는 구조체입니다. add_child는 지금 element에 자식 element를 추가하는 형태입니다. 기본은 참조로서, 2가 붙은 메소드는 포인터로서 리턴됩니다. 핵심은 자기자신을 참조로 사용하기에 체인형태로 호출이 됩니다.

```c++
HtmlBuilder builder{"ul"};
builder.add_child("li", "hello").add_child("li", "world")
```

이를 흐름식 인터페이스(`fluent interface`)라고 합니다. HtmlBuilder에 있는 HtmlElement에 대해서 알아봅시다.

```c++
struct HtmlElement
{
  string name;
  string text;
  vector<HtmlElement> elements;
  const size_t indent_size = 2;

  HtmlElement() {}
  HtmlElement(const string& name, const string& text)
    : name(name),
    text(text)
  {
  }

  string str(int indent = 0) const
  {
    ostringstream oss;
    string i(indent_size*indent, ' ');
    oss << i << "<" << name << ">" << endl;
    if (text.size() > 0)
      oss << string(indent_size*(indent + 1), ' ') << text << endl;

    for (const auto& e : elements)
      oss << e.str(indent + 1);

    oss << i << "</" << name << ">" << endl;
    return oss.str();
  }

  static unique_ptr<HtmlBuilder> build(string root_name)
  {
    return make_unique<HtmlBuilder>(root_name);
  }
};
```

빌더 패턴의 핵심입니다. 생성자를 숨겨서 사용자가 접근하지 못하고 HtmlElement로 빌더를 생성할 수 있습니다. 

```c++
auto builder2 = HtmlElement::build("ul")
    ->add_child_2("li", "hello")->add_child_2("li", "world");
cout << builder2 << endl;
```



### 팩토리 메소드(Factory Methods)

![3_Factory method](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/3_Factory method.png)

팩토리 메소드는 객체 생성을 서브 클래스(ConcreteCreator)가 맡습니다. 분리된 만큼 다채로운 생성을 할 수 있는 장점이 있으나 규모에 따라 빈번한 중복이 생길 수 있습니다. Product는 팩토리 메소드의 공통 인터페이스로, ConcreteProduct가 구현을 담당합니다. Creator는 팩토리 **메소드**를 가지는 **클래스**이고 ConcreteCreator는 팩토리 메소드를 구현합니다.

예제

```c++
class Point
{
    
  Point(const float x, const float y)
    : x{x},
      y{y}
  {
  }

public:
  float x, y;


  friend std::ostream& operator<<(std::ostream& os, const Point& obj)
  {
    return os
      << "x: " << obj.x
      << " y: " << obj.y;
  }

  static Point NewCartesian(float x, float y)
  {
    return{ x,y };
  }
  static Point NewPolar(float r, float theta)
  {
    return{ r*cos(theta), r*sin(theta) };
  }
};
```

아마 이해하는데 어려움이 없을 것으로 생각합니다. New-x-에 대해서 Point를 가공하여 리턴합니다.

```c++
  auto p = Point::NewPolar(5, M_PI_4);
  std::cout << p << std::endl;
```



### 프로토 타입(Prototype)

![4_Ptrototype](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/4_Ptrototype.png)

프로토타입은 말 그대로 베이스를 가지고 있는 인스턴스로 필요한 기능을 붙인 인스턴스를 만드는 패턴입니다. 헷갈리지 마세요. **인스턴스**입니다. Prototype의 구조는 간단합니다. 

```c++
  auto addr = new Address{ "123 East Dr", "London", 0 /* ? */ };

  Contact john{ "John Doe", addr };
  john.address->suite = 123;
  Contact jane{ "Jane Doe", addr };
  jane.address->suite = 124;
```

프로토타입의 예시는 위와 같습니다. 공통된 주소를 가져와서 개인별 상세 내용을 수정하죠.



### 싱글톤(Singleton)

![5_Singleton](https://cdn.jsdelivr.net/gh/MnSBlog/MnSBlog.github.io@master/assets/img/posts/Knowledge/DesignPattern/5_Singleton.png)

싱글톤은 전역에서 참조가능한데도 하나만 생성되는 특징을 가지고 있습니다.

예제

```c++
class Database
{
public:
  virtual int get_population(const std::string& name) = 0;
};
```

인구수를 가져오는 데이터베이스가 있습니다.

```c++
class SingletonDatabase : public Database
{
  SingletonDatabase()
  {
    std::cout << "Initializing database" << std::endl;

    std::ifstream ifs("capitals.txt");

    std::string s, s2;
    while (getline(ifs, s))
    {
      getline(ifs, s2);
      int pop = boost::lexical_cast<int>(s2);
      capitals[s] = pop;
    }
  }

  std::map<std::string, int> capitals;

public:
  SingletonDatabase(SingletonDatabase const&) = delete;
  void operator=(SingletonDatabase const&) = delete;

  static SingletonDatabase& get()
  {
    static SingletonDatabase db;
    return db;
  }

  int get_population(const std::string& name) override
  {
    return capitals[name];
  }
};
```

static으로서 구현된 인스턴스를 받아옵니다. 이런 비슷한 사례로

```c++
class Printer
{
  static int id;
public:
  int get_id() const { return id; }
  void set_id(int value) { id = value; }
};
```

모노스테이트(`monostate`)라고 합니다. 보기에는 평범한 클래스처럼 동작하지만, id가 static으로 구현되어 모든 인스턴스가 같은 데이터를 보고있습니다.
