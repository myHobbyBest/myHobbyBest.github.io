---
title:  "Class 와 객체지향 프로그래밍 ( OOP )"  
date:   2022-12-05 14:10:09 +0900
categories: [Flutter, dart]
tag: [class, OOP, 객체지향프로그래밍,named constructor, ]
toc: true
---

## Class와 객체 지향 프로그래밍(OOP)

다트는 클라스와 mixin기반상속을 가지는 객체지향 언어이다. 모든 객체는 클라스의 인스턴스이고 널(Null)이 아닌 모든 클라스는 기본 객체(Object)로부터 내려온다.  
mixin기반 상속이란 '모든 클라스가 정확히 하나의 부모 클라스를 가짐에도 불구하고 하나의 클라스 몸체는 여러 클라스 계층에서 재 사용될 수 있다'는 것을 의미한다. 
확장방법(Extension methods)은 클라스를 변경하거나 하위클라스를 생성하지 않고도 클라스에 기능을 부여하는 방법을 제공한다. 



- 객체 지향 프로그래밍(OOP)에서 특정 객체를 생성하기 위해 그 객체의 여러 특성(속성,변수)과 기능(메소드)들을 정의하여 묶어놓은 일종의 템플리트(template)이다.

- 템플릿을 사용하면 객체를 분류할 때 멤버의 자료형을 미리 정하지 않고 객체를 사용할 때 결정할 수 있다. 이를 통해 클래스나 변수의 중복 정의를 하지 않아도 되므로 효율적으로 코딩이 가능하다.

- 클래스는 전부 혹은 일부를 그 클래스 특성으로부터 상속받는 서브클래스를 가질 수 있으며, 클래스는 각 서브클래스에 대해 수퍼클래스가 된다.

- 서브클래스는 자신만의 메소드와 변수를 정의할 수도 있다.
이러한 클래스와 그 서브클래스 간의 구조를 "클래스 계층(hierarchy)"이라 한다.

#### 클라스멤버의 사용 (using class members)
  
  객체는 함수(메소드)와 데이타(인스턴스 변수)로 구성된 멤버(members)를 가진다. 메소드를 호출하면 이것은 객체위에서 그것을 호출한 것이다.: 그 객체의 함수와 데이타에 접근하게 된 것이다.  
  인스턴스의 변수나 메소드를 참조하려면 dot(.)를 사용한다. 
``` dart

var p = Point(2, 2); // Point는 dart에서 기본 제공되는 2차원 (직교좌표 )위치 표현방법이다. 

// Get the value of y.
assert(p.y == 2);

// Invoke distanceTo() on p.
double distance = p.distanceTo(Point(4, 4));
```

#### __?__ 를 사용하여 null 오류를 회피한다. 

``` dart
// If p is non-null, set a variable equal to its y value.
var a = p?.y;
```

### 객체 지향 프로그래밍의 특징

객체 지향 프로그래밍이 가지는 특징은 다음과 같다.

- 추상화(abstraction)
- 캡슐화(encapsulation)
- 정보 은닉(data hiding)
- 상속성(inheritance)
- 다형성(polymorphism)

### 객체 와 class 비교

|                      Object |            Class                             |
|:----------------------------------------:|:--------------------------------:|
|  객체는 class의 인스턴스이다.             |    class 는 객체를 생성하기 위한 청사진(템플리트) 이다.    |
|  객체는 펜, 마우스, 의자 등과 같은 현실 세계의 개체(entity)이다.   |            class 는 유사한 객체들의 집합이다.    |
|  객체는 물리적 개체이다.                  |      class는 논리적 개체(entity)이다.         |
|  객체는 필요할 때마다 반복해서 생성된다.                          |      class는 오직 한번 만 선언한다.  |
|  객체가 생성되면 메모리에 상주한다.                               |           class는 선언해도 메모리를 점유하지않는다.    |


#### 예제
아래와 같이 Cat이라는 크라스를 정의해보자 
``` dart
class Cat {
    String name;
    String color;
}
```
위에서 정의된 `String name` 과 `String color` 는 속성 또는 class member 라고 부른다. 

- 인스턴스 생성방법

``` dart
Cat nora = new Cat(); //  dart 언어에서 `new` 키워드는 생략할 수 있다.  
nora.name = 'Nora';
nora.color = 'Orange';
```

`Cat nora` 이렇게 변수명 앞에 `Cat`이라고 쓰는 것은 일종의 __변수type__ 선언이다. 하지만 `var nora` 라고 선언할 수도 있다.

#### Instance variables
인스턴스 변수를 선언하는 방법을 알라보자
``` dart{
  double? x; // Declare instance variable x, initially null.
  double? y; // Declare y, initially null.
  double z = 0; // Declare z, initially 0.
}
```
초기화하지 않는 모든 변수는 null값을 가진다.
모든 인스턴스 변수는 절대적인 gertter 메소드를 생성한다. non-final 인스턴스변수와 초기화하지않은 late final 인스턴스 변수는 setter 메소드를 생성한다. 상세한 것은 getters - setters 에서 다룬다.
만일 non-late 인스턴스 변수를 선언하면서 초기화 하면 그 값은 인스턴스가 생성될 때 (생성자 앞에서 초기화 리스트가 샐행될 때) 결정된다. 

``` dart
class Point {
  double? x; // Declare instance variable x, initially null.
  double? y; // Declare y, initially null.
}

void main() {
  var point = Point();
  point.x = 4; // Use the setter method for x.
  assert(point.x == 4); // Use the getter method for x.
  assert(point.y == null); // Values default to null.
}
```
인스턴 변수는 __final__  이 될 수 있고 이 경우 반드시 한번 만 지정해야 한다. 
__final__ , __non-late__ 인스턴스 변수를 선언할 때 생성자 파라메터를 이용하거나 생성자의 초기화 리스트를 이용하여 초기화한다. 

```dart
class ProfileMark {
  final String name;
  final DateTime start = DateTime.now();

  ProfileMark(this.name);
  ProfileMark.unnamed() : name = '';
}
```
만일 생성자 몸체를 시작한 이후에 __final__ 인스턴스 변수를 지정하고 싶다면  다음 중 한가지방법을 새용할 수 있다.

- 팩토리 생성자를 이용한다. 
- __late final__  인스턴스 변수를 세심하게 이용한다.: API에 초기화 지정자 없이 __late final__ 넣어 준다. 


#### 생성자 (constructor)

Class이름과 동일한 이름을 가지는 함수(메소드)를 생성하는 방법으로 선언(생성)된다.  생성자를 이용하여 객체를 생성한다.  생성자는 미리 결정된 속성값을 가지고 객체들을 생성한다. 
` 생성자에는 표준 생성자(standard constructor,default constructor), 이름있는 생성자(Named constructor),팩토리 생성자(factory constructor) 등의 종류가 있다. 
이외에도 초기화 리스트(initializer list), 리다이렉팅 생성자(redirecting constructor), 상수 생성자(constant constructor) 등의 개념을 알아두어야한다.


#### 기본 생성자(default constructor)

class를 선언할 때 생성자를 선언하지 않으면 기본생성자가 자동으로 제공된다.  매개변수(arguments)를 가지지 않으며 부모클라스의 비매개변수 생성자를 호출한다.

#### 생성자는 생속되지 않는다.
하위 클라스는 부모 클라스로부터 생성자를 상속받지 않는다. 생성자를 선언하디 않은 하위 클라스는 단지 기본 생성자(no argument, no name)를 가질 뿐이다. 

``` dart
class Person{
    Person(){        
        print('This is Person Constructor!');
    }
}
class Student extents Person{
    
 // 자식클래스는 부모클래스의 생성자를 상속받지 않는다. 
 // 다만 생성자가 생략된 경우 기본생성자가 부모클라스의 기본생성자를 호줄한다. 
 // 
}

Main(){
    var student = new Student(); //  ( 인스턴스화 ) new 를 생략할 수 있다. 
}
```

따라서 다음과 같은 결과를 호출한다.

``` terminal 
This is Person Constructor!
```

#### 이름 있는 생성자 (Named constructor)

클라스 내에서 많은 생성자를 형성하거나 생성자를 명확히 하기위해 Named constructor를 사용한다.

``` dart
class 클래스명{

    클래스명. 생성자명(){

    }
}

const double xOrigin = 0;
const double yOrigin = 0;

class Point {
  final double x;
  final double y;

  Point(this.x, this.y);

  // Named constructor
  Point.origin()
      : x = xOrigin,
        y = yOrigin;
}

```

하위 클라스는 부모 클라스로부터 생성자를 상속받지 않는다는 점을 상기 할때 부모 클라스의 이름있는 생성자라도 자식 클라스에서 사용하기 위해서는 자식 클라스에서 생성자로 선언해 주어야 한다. 

#### Invoking a non-default superclass constructor 

기본적으로 자식 클라스에서 생성자는 부모 클라스의 이름없는 생성자를 호출한다. 부모 클라스의 생성자는 생성자 본체가 시작할때 호출된다. 초기화 리스트가 사용된 경우 부모 클라스가 호출되기 전에 실행된다. 

종합해서 실행 순서를 살펴보면 아래와 같다. 

- 초기화 리스트
- 부모 클라스의 no-arg 생성자
- 주 클라스(자식 클라스)의 no-arg 생성자

만일 부모 클라스에 이름없는 생성자가 없다면 반드시 부모클라스의 생성자 중에 하나를 수동적으로 호출해주어야만 한다. 생성자 몸체 바로 앞에서 콜론(:)을 붙이고 뒤에 부모 클라스생성자를 지정한다.

```
class Person {
  String? firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson().
  Employee.fromJson(super.data) : super.fromJson() {
    print('in Employee');
  }
}

void main() {
  var employee = Employee.fromJson({});
  print(employee);
  // Prints:
  // in Person
  // in Employee
  // Instance of 'Employee'
}

```

### 리다이렉팅 생성자

초기화리스트를 응용하면 단순히 리다이렉팅을 위한 생성자를 만들 수 있다. 본체가 비어있고 메인 생성자에게 위임하는 역할을 한다.

``` dart
class Person{
    String name;
    int age;
    Person (this.name, this,age){
        print('This is Person($name, $age) Constructor!'  );
    }

    Person.initName(String name) : this (name,20);
}

main(){
    var person = Person.initName('Kim');

}
```
결과
``` terminal
 This is Person(Kim, 20) Constructor!
```
이름있는 생성자인 Person.initName(String name)은 본체가 없고 초기화 리스트로 this(name,20)가 선언되어있다. this 는 현재의 인스턴스를 가리키므로 여기서 this(name,20)은 현재인스턴스의 생성자인 Person(this.name, this.age)가 된다. 따라서 Person.initName('Kim')을 호출하면 Person()의 인자로 쓰인 this.name은 현재 인스턴스의 name을 의미하므로 Person(this.name, this.age)의 인자로 Person.initName('Kim')에서 받은 Kim과 20이 할당된다. 


#### 상수 생성자
class 멤버 변수 앞에서 final을 선언하면 상수처럼 변하지 않는 객체를 생성한다. 이를 상수 생성자라고 부르며 생성자앞에 const 를 붙여 주어야 한다. 

``` dart
class Rectangle {
  // these are assigned in the constructor,
  // and can never be changed.
  final int width;
  final int height;
  const Rectangle(this.width, this.height);
}

main (){
  
  Rectangle rec1 = const  Rectangle(20, 30);
  Rectangle rec2 = const  Rectangle(20, 30);
  Rectangle rec3 = new  Rectangle(20, 30);
  Rectangle rec4 = new  Rectangle(20, 30);
  
  print (identical (rec1,rec2));
  print (identical (rec2,rec3));
  print (identical (rec3,rec4));
}
```
실행 결과

``` consol
true
false
false
```
`rec1`과 `rec2`완전히 동일한 인스턴스를 참조하고있기떄문에 참 값이 반환되었지만  나머지는 모두 별개의  인스턴스를 생성하고 있어서 참이 아니다.

### 초기화 리스트 

최기화 리스트를 사용하면 인스턴스가 생성될 때 생성자의 구현부가 실행되기 전에 인스턴스 변수를 초기화 할 수 있다. 
생성자 옆에서 콜론(:)을 붙여 선언한다.

``` dart
main() {
  final rectangle = Rectangle(2, 5);
}

class Rectangle {
  final int width;
  final int height;
  final int area;
  
  Rectangle(this.width, this.height) 
    : area = width * height {
      print(area);
    }
}
```
사각형의 면적은 넓이와 높이를 알아야 계산되지만 인스턴스가 생성될 때까지는  그 값을 알수 없으므로 생성자 밖에서는 계산할 수 없다. 이런경우에 유용하게 사용된다. 
- 결과 
``` terminal
10
```
#### 팩토리 생성자

- 팩토리 생성자는 클라스의 인스턴스를 반환하지만 새로운 인스턴스를 생성할 필요는 없다. 이미 존재하는 인스턴스나 하위 (자식)클라스의 인스턴스를 반환할 수 있다.
- Factory method는 부모(상위) 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴이며. 자식(하위) 클래스가 어떤 객체를 생성할지를 결정하도록 하는 패턴이기도 하다.
- 인스턴스 변수가 아닌  클래스 변수를 사용하므로 생성자 없이도 접근이 가능하다. 

__팩토리 생성자를 위한 규칙__
   - `return` 키워드를 사용할 것
   - 팩토리 생성자 내에서는 `this`를 사용할 수 없다.

- 예제

``` dart
class Cat {
    String name;
    String color;

    Cat({required this.name, required this.color});

    // factory constructor that returns a new instance
    factory Cat.fromJson(Map json) {
        return Cat(name : json['name'],
        color : json['color']);
    }
}

void main(){

    Map mew = {'name': 'kitty', 'color': 'orange'};

    Cat purr = Cat.fromJson(mew);
    print(purr.name);
    print(purr.color);

}
```
- 결과
``` consol
kitty
orange
```

### 참고 자료

-  '플러터를 위한 다트언어'  서준수    브런치북
-  유튜브 [왕초보 무료 프로그래밍 언어 강의] [Dart] #17 - Class [#1] 선언 및 Constructor (https://youtu.be/9NSlc_CRiLI )
-  플러터(flutter) 순한맛 강좌 12 | 플러터 다트(dart) 핵심정리: 클래스와 위젯의 정체 1   https://youtu.be/8k4vaoga2co