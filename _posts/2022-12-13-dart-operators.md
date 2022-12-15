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

(경고: 이 표는 유용한 가이드로만 사용해야 한다. 연산자 우선 순위와 결합성의 개념은 언어 문법에서 발견되는 실제 경우의 근사치이다.  Dart language specification 에 정의된 문법에서 Dart 연산자 관계의 올바른 관계를 찾을 수 있다.)

연산자를 사용하면 표현식이 생성된다. 다음은 연산자 표현식의 몇 가지 예이다.

``` dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

연산자 테이블에서 각 연산자는 뒤에 오는 행의 연산자보다 우선 순위가 높다. 예를 들어 곱셈 연산자 `*`는 (논리 AND 연산자 `&&` 보다 우선 순위가 높은) 같음 연산자 `==` 보다 우선 순위가 높다(따라서 먼저 실행됨). 이러한 우선 순위는 다음 두 줄의 코드가 동일한 방식으로 실행됨을 의미한다.

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

`as`, `is` 와 `is!` 연산자는 런타임에서 유형을 확인하는 데 편리하다.

![type test operators](/images/2022-12-13/2022-12-13-type-test-operator.png)

`obj`가 T로 지정된 인터페이스를 구현하는 경우 `obj is T`는 참이다. 예를 들어, `obj is Object?`는 항상 참이다.

객체가 특정 유형인지 확신하는 경우에만 `as` 연산자를 사용하여 객체를 특정 유형으로 `cast'한다. 예시:

``` dart
(employee as Person).firstName = 'Bob';
```

객체가 T 유형인지 확실하지 않은 경우 `is T`를 사용하여 객체를 사용하기 전에 유형을 확인한다.

``` dart
if (employee is Person) {
  // Type check
  employee.firstName = 'Bob';
}
```

(참고: 두 코드는 동일하지 않다. `employee`이 `null`이거나 `Person`이 아닌 경우 첫 번째 예에서 예외가 발생한니다. 두 번째 예에서는 아무것도 하지 않는다.)

- #### 할당 연산자 (Assignment operators)

이미 본 것처럼 `=` 연산자를 사용하여 값을 할당할 수 있다. 할당 대상 변수가 null인 경우에 만 할당하려면 ??= 연산자를 사용한다.

``` dart
// Assign value to a
a = value;
// Assign value to b if b is null; otherwise, b stays the same
b ??= value;
```

`+=`와 같은 복합 대입 연산자는 연산과 대입을 결합한다.

![assignment operators](/images/2022-12-13/2022-12-13-assignment-operators.png)

복합 대입 연산자의 작동 방식은 다음과 같다.

![assignment operators work](/images/2022-12-13/2022-12-13-assignment-operators-work.png)

``` dart
var a = 2; // Assign using =
a *= 3; // Assign and multiply: a = a * 3
assert(a == 6);
```

- #### 논리 연산자 (Logical operators)

논리 연산자를 사용하여 부울 식을 반전하거나 결합할 수 있다.

![logical operators](/images/2022-12-13/2022-12-13-logical-operators.png)

다음은 논리 연산자를 사용하는 예이다.

``` dart
if (!done && (col == 0 || col == 3)) {
  // ...Do something...
}
```

- #### 비트 및 시프트 연산자 (Bitwise and shift operators)

Dart에서 숫자의 개별 비트를 조작할 수 있다. 일반적으로 이러한 비트 및 시프트 연산자를 정수와 함께 사용한다.

![bitwise and shift operators](/images/2022-12-13/2022-12-13-bitwise-shift-operators.png)

다음은 비트 및 시프트 연산자를 사용하는 예이다.

``` dart
final value = 0x22;
final bitmask = 0x0f;

assert((value & bitmask) == 0x02); // AND
assert((value & ~bitmask) == 0x20); // AND NOT
assert((value | bitmask) == 0x2f); // OR
assert((value ^ bitmask) == 0x2d); // XOR
assert((value << 4) == 0x220); // Shift left
assert((value >> 4) == 0x02); // Shift right
assert((value >>> 4) == 0x02); // Unsigned shift right
assert((-value >> 4) == -0x03); // Shift right
assert((-value >>> 4) > 0); // Unsigned shift right
```

(버전 참고: `>>>` 연산자(트리플 시프트 또는 무부호 시프트로 알려짐)에는 2.14 이상의 언어 버전이 필요하다.)

- #### 조건식 ( Conditional expressions )

Dart에는 if-else 문이 필요할 수 있는 표현식을 간결하게 평가할 수 있는 두 개의 연산자가 있다.

`condition ? expr1 : expr2`
`condition`이 참이면 `expr1`을 계산하고 해당 값을 반환한다. 그렇지 않으면 `expr2`의 값을 계산하고 반환한다.
`expr1 ?? expr2`
`expr1`이 null이 아닌 경우 해당 값을 반환한다. 그렇지 않으면 `expr2`의 값을 계산하고 반환한다.
부울 식을 기반으로 값을 할당해야 하는 경우 `?`와 `:`를 고려한다.

``` dart
var visibility = isPublic ? 'public' : 'private';
```

부울 표현식이 null을 테스트하는 경우 ??를 사용하는 것이 좋다.

``` dart
String playerName(String? name) => name ?? 'Guest';
```

앞의 예제는 아래 같이 적어도 두 가지 다른 방법으로 작성될 수 있지만 간결하지는 않다.

``` dart
// Slightly longer version uses ?: operator.
String playerName(String? name) => name != null ? name : 'Guest';

// Very long version uses if-else statement.
String playerName(String? name) {
  if (name != null) {
    return name;
  } else {
    return 'Guest';
  }
}
```

- #### 캐스케이드 표기법 (Cascade notation)

캐스케이드(`..`, `?..`)를 사용하면 동일한 개체에 대해 연속적으로 작업을 수행할 수 있다. 인스턴스 멤버에 액세스하는 것 외에도 동일한 개체에서 인스턴스 메서드를 호출할 수도 있다. 이렇게 하면 종종 임시 변수를 만드는 단계가 줄어들고 더 유동적인 코드를 작성할 수 있다.

다음 코드를 생각해 보자.

``` dart
var paint = Paint();
paint.color = Colors.black;
paint.strokeCap = StrokeCap.round;
paint.strokeWidth = 5.0;
```

캐스케이드가 작동하는 개체가 null일 수 있는 경우 첫 번째 작업에 `null-shorting` 캐스케이드(`?..`)를 사용한다. `?..`로 시작하면 해당 null 개체에서 연속 작업이 시도되지 않는다.

``` dart
querySelector('#confirm') // Get an object.
  ?..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'))
  ..scrollIntoView();
```

(버전 참고: `?..` 구문에는 2.12 이상의 언어 버전이 필요하다.)
앞의 코드는 다음과 동일하다.

``` dart
var button = querySelector('#confirm');
button?.text = 'Confirm';
button?.classes.add('important');
button?.onClick.listen((e) => window.alert('Confirmed!'));
button?.scrollIntoView();
```

캐스케이드를 중첩할 수도 있다. 예를 들어:

``` dart
final addressBook = (AddressBookBuilder()
      ..name = 'jenny'
      ..email = 'jenny@example.com'
      ..phone = (PhoneNumberBuilder()
            ..number = '415-555-0100'
            ..label = 'home')
          .build())
    .build();
```

실제 개체를 반환하는 함수에서 캐스케이드를 구성하도록 주의하자. 예를 들어 다음 코드는 실패한다.

``` dart
var sb = StringBuffer();
sb.write('foo')
  ..write('bar'); // Error: method 'write' isn't defined for 'void'.
```

sb.write() 호출은 void를 반환하며 void에서 캐스케이드를 구성할 수 없다.

(참고: 엄밀히 말하면 캐스케이드 "double dot" 표기법은 연산자가 아니다. Dart 구문의 일부일 뿐이다.)

- #### 기타 연산자 (Other operators)

그 동안 다른 예제에서 나머지 연산자 대부분을 보아왔다.

![other-operators](/images/2022-12-13/2022-12-13-other-operators.png)

`.`, `?.` 및 `..` 연산자에 대한 자세한 내용은 Classes를 참조하라.
