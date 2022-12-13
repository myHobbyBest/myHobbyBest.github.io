---
title:  "Operators"  
date:   2022-12-13 10:05:45 +0900
categories: [Flutter, Dart]
tag: [Operators]
toc: true
---
### 연산자(Operators)

Dart는 다음 표에 표시된 연산자를 지원한다. 이 표는 Dart의 연산자 연관성과 연산의 우선 순위(operator precedence)를 가장 높은 것부터 가장 낮은 것까지 (근사치로) 보여준다.  이러한 연산자 중 다수를 클래스 멤버로 구현할 수 있다.

![Operators](/images/2022-12-13/20221213-operators.png)

(경고: 이 표는 유용한 가이드로만 사용해야 한다. 연산자 우선 순위와 결합성의 개념은 언어 문법에서 발견되는 실제 경우의 근사치입니다.  Dart language specification 에 정의된 문법에서 Dart 연산자 관계의 올바른 관계를 찾을 수 있다.)

연산자를 사용하면 표현식이 생성된다. 다음은 연산자 표현식의 몇 가지 예이다.

``` dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

연산자 테이블에서 각 연산자는 뒤에 오는 행의 연산자보다 우선 순위가 높습니다. 예를 들어 곱셈 연산자 *는 (논리 AND 연산자 `&&` 보다 우선 순위가 높은) 같음 연산자 `==` 보다 우선 순위가 높다(따라서 먼저 실행됨). 이러한 우선 순위는 다음 두 줄의 코드가 동일한 방식으로 실행됨을 의미한다.

``` dart
// Parentheses improve readability.
if ((n * i == 0) && (d * i == 0)) ...

// Harder to read, but equivalent.
if (n * i == 0 && d * i == 0) ...
```

(경고: 두 개의 피연산자를 사용하는 연산자의 경우 가장 왼쪽 피연산자가 사용할 방법을 결정한다. 예를 들어 Vector 개체와 Point 개체가 있는 경우 aVector + aPoint는 벡터 합(+)을 사용한다.)

- #### 산술 연산자 (Arithmetic operators)

    Dart는 다음 표와 같이 일반적인 산술 연산자를 지원한다.

    ![Arithmetic operators](/images/2022-12-13/2022-12-13-2-arithmatic-operators.png)

예제

``` dart
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
assert(5 % 2 == 1); // Remainder

assert('5/2 = ${5 ~/ 2} r ${5 % 2}' == '5/2 = 2 r 1');
```

Dart는 또한 접두사 및 접미사 증가 및 감소 연산자를 모두 지원한다.

![increnemt-decrment-operators](/images/2022-12-13/2022-12-13-increment-decrement-operators.png)

예제

``` dart
int a;
int b;

a = 0;
b = ++a; // Increment a before b gets its value.
assert(a == b); // 1 == 1

a = 0;
b = a++; // Increment a AFTER b gets its value.
assert(a != b); // 1 != 0

a = 0;
b = --a; // Decrement a before b gets its value.
assert(a == b); // -1 == -1

a = 0;
b = a--; // Decrement a AFTER b gets its value.
assert(a != b); // -1 != 0
```

- #### 같음 및 관계 연산자 (Equality and relational operators)

다음 표에는 같음 및 관계 연산자의 의미가 나열되어 있다.

![Equality and relational operators](/images/2022-12-13/2022-12-13-equality-operators.png)

두 객체 x와 y가 같은 것을 나타내는지 테스트하려면 `==` 연산자를 사용한다. (두 개체가 정확히 같은 개체인지 알아야 하는 드문 경우에는 대신 same() 함수를 사용한다.) `==` 연산자의 작동 방식은 다음과 같다.

x 또는 y가  null인 경우에 있어서 x 와 y가 둘 다 null이면  true를 반환하고  하나만 null이면 false를 반환한다.

인수 y를 사용하여 x에 대해 `==` 메서드를 호출한 결과를 반환한다. ( 즉 `==`와 같은 연산자는 첫 번째 피연산자에서 호출되는 메서드이다. 자세한 내용은 연산자를 참조한다.)

다음은 같음 및 관계 연산자를 각각 사용하는 예이다.

``` dart
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
assert(3 >= 3);
assert(2 <= 3);
```
- #### 유형 테스트 연산자 (Type test operators)




