---
title:  "Class 와 객체지향 프로그래밍 ( OOP )"  
date:   2022-12-05 14:10:09 +0900
categories: [Flutter, dart]
tag: [class, OOP, 객체지향프로그래밍 ]
toc: true
---

## Class와 객체 지향 프로그래밍(OOP)

### Class 란? 

- 객체 지향 프로그래밍(OOP)에서 특정 객체를 생성하기 위해 그 객체의 여러 특성(속성,변수)과 기능(메소드)들을 정의하여 묶어놓은 일종의 템플리트(template)이다.

- 템플릿을 사용하면 객체를 분류할 때 멤버의 자료형을 미리 정하지 않고 객체를 사용할 때 결정할 수 있다. 이를 통해 클래스나 변수의 중복 정의를 하지 않아도 되므로 효율적으로 코딩이 가능하다.

- 클래스는 전부 혹은 일부를 그 클래스 특성으로부터 상속받는 서브클래스를 가질 수 있으며, 클래스는 각 서브클래스에 대해 수퍼클래스가 된다.

- 서브클래스는 자신만의 메소드와 변수를 정의할 수도 있다.
이러한 클래스와 그 서브클래스 간의 구조를 "클래스 계층(hierarchy)"이라 한다.

### 객체 지향 프로그래밍의 특징
객체 지향 프로그래밍이 가지는 특징은 다음과 같다. 
1. 추상화(abstraction)
2. 캡슐화(encapsulation)
3. 정보 은닉(data hiding)
4. 상속성(inheritance)
5. 다형성(polymorphism)

### 객체 와 class 비교
 | Object |  Class    |
|-----|----|
|  객체는 class의 인스턴스이다.     |             class 는 객체를 생성하기 위한 청사진(템플리트) 이다.    |
|  객체는 펜, 마우스, 의자 등과 같은 현실 세계의 개체(entity)이다.     |                class 는 유사한 객체들의 집합이다.                |
|  객체는 물리적 개체이다.  |      class는 논리적 개체(entity)이다.         |
|  객체는 필요할 때마다 반복해서 생성된다.   |      class는 오직 한번 만 선언한다.  |
|  객체가 생성되면 메모리에 상주한다.  |           class는 선언해도 메모리를 점유하지않는다.    |

### 생성자 (constructor)


Class 에는 항상 생성자가 따라 다닌다. class 가 객체가 생성될때 (인스턴스화 할때) 호출되기 때문에 생성자라고 이름지어졌다.
생성자에는 알아두어야할 여러가지 개념이 있다.
- 기본 생성자(default constructor), 이름있는 생성자(Named constructor), 초기화 리스트(initializer list), 리다이렉팅 생성자(redirecting constructor),상수 생성자(constant constructor), 팩토리 생성자(factory constructor).

#### 기본 생성자(default constructor)

class를 선언할 때 생성자를 선언하지 않으면 기본생성자가 자동으로 제공된다. Class 명과 동일한 이름을 가지며 매개변수(arguments)를 가지지 않는다. 

``` dart
class 클래스명{
    클래스명(){        // 생략된 것이지만 존재한다.
    }
}
```
#### 생성자의 상속
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

클라스 내에서 많은 생성자를 형성하거나 생성자를 명확히 하기위해 사용한다. 

``` dart
class 클래스명{

    클래스명. 생성자명(){

    }
}
```
예제

``` dart
class Person{

    Person(){
        print('This is Person Constructor!');
    }

    Person.init(){
        print('This is Person.init Constructor!');
    }
}
Class Student extends Person{
    print(' This is Student Constructor!');
    }
}
main(){

    var person = Person();
    var init = Person.init();

}
```

