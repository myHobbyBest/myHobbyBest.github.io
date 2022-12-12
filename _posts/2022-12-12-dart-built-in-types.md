---
title:  "Built-in types"  
date:   2022-12-12 09:00:20 +0900
categories: [Flutter, Dart]
tag: [Built-in types]
toc: true
---
### 내장 유형 (Built-in types)


Dart 언어는 아래와 같은 것들을 특별히 지원한다.

- Numbers (int, double)
- Strings (String)
- Booleans (bool)
- Lists (List, 배열이라고도 함)
- Sets (Set)
- Maps (Map)
- Runes (Runes; 종종 문자 API로 대체됨)
- Symbols (Symbol)
- The value null (Null)

이 지원에는 리터럴을 사용하여 개체를 만드는 기능이 포함된다. 예를 들어 'this is a string'은 ``string`` 리터럴이고 true는 ``bool`` 리터럴이다.

Dart의 모든 변수는 객체(클래스의 인스턴스)를 참조하기 때문에 일반적으로 생성자를 사용하여 변수를 초기화할 수 있다. 일부 built-in type 에는 자기자신의 고유한 생성자가 있다. 예를 들어 ``Map()`` 생성자를 사용하여 map을 만들 수 있다.

일부 다른 유형도 Dart 언어에서 특별한 역할을 한다.

- ``Object`` : Null을 제외한 모든 Dart 클래스의 슈퍼클래스이다.
- ``Enum`` : 모든  enum들의 슈퍼클래스이다.
- ``Future`` 와 ``Stream`` : 비동기 지원에 사용된다.
- ``Iterable`` : for-in loop 및 동기 생성기 함수에 사용된다.
- ``Never`` : 표현식이 평가를 성공적으로 완료할 수 없음을 나타낸다. 항상 예외를 발생시키는 함수에 가장 자주 사용된다.
- ``dynamic``: 정적 검사를 비활성화할 것임을 나타낸다. 일반적으로 ``Object`` 또는 ``Object?``를 사용해야 한다.
- ``void``: 값이 사용되지 않음을 나타낸다. 반환 유형으로 자주 사용된다.

``Object``, ``Object?``, ``Null`` 및 ``Never`` 클래스는 null safty 이해의 상위 및 하위 섹션에 설명된 것 처럼 클래스 계층 구조에서 특별한 역할을 한다.

- #### Numbers

다트에서 Number에는 두 가지 종류가 있다.

``int``
플랫폼에 의존하지만  대개 64비트 이하의 정수 값이다. 기본 플랫폼에서 값은 $-2^{63}$ 에서 $2^{63}-1$ 까지일 수 있다. 웹에서 정수 값은 JavaScript 숫자(소수부가 없는 64비트 부동 소수점 값)로 표시되며 $-2^{53}$ 에서 $2^{53}-1$ 까지일 수 있다.

``double``

IEEE 754 표준에 지정된 64비트(double-precision) 부동 소수점 숫자이다.

`int`와 `double`은 모두 `num`의 하위 유형이다. `num` 유형에는 `+`, `-`, `/` 및 `*`와 같은 기본 연산자가 포함되며 `abs()`, `ceil()` 및 `floor()` 등의 메서드도 있다. ( `>>` 와 같은 비트 연산자는 `int` 클래스에 정의되어 있다.) `num` 및 해당 하위 유형에 원하는 것이 없으면 `dart:math` 라이브러리에서 찾을 수 있다.

정수는 소수점이 없는 숫자이다. 다음은 정수 리터럴을 정의하는 몇 가지 예이다.

``` dart
var x = 1;
var hex = 0xDEADBEEF;
```

숫자에 소수점이 포함되어 있으면 `double`이다. 다음은 `double` 리터럴을 정의하는 몇 가지 예이다.

``` dart
var y = 1.1;
var exponents = 1.42e5;
```
변수를 `num`으로 선언할 수도 있다. 이렇게 하면 변수가 `int` 값과 `double` 값을 모두 가질 수 있다.

```dart
num x = 1; // x can have both int and double values
x += 2.5;
```
`int` 리터럴은 필요할 때 자동으로 `double`로 변환된다.

```dart
double z = 1; // Equivalent to double z = 1.0.
```

문자열을 숫자로 변환하거나 그 반대로 변환하는 방법은 다음과 같다.

```dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

int 유형은  비트 필드에서 플래그 조작 및 마스킹에 유용한 전통적인 비트 시프트(<<, >>, >>>), complement (~), AND(&), OR(|) 및 XOR(^) 연산자를 활용한다.예를 들어:

``` dart
assert((3 << 1) == 6); // 0011 << 1 == 0110
assert((3 | 4) == 7); // 0011 | 0100 == 0111
assert((3 & 4) == 0); // 0011 & 0100 == 0000
```

더 많은 예제를 보려면 bitwise and shift operator 섹션을 참조하자.

리터럴 숫자는 컴파일 타임 상수이다. 피연산자가 숫자로 평가되는 컴파일 시간 상수인 한 많은 산술 표현식도 컴파일 시간 상수가 된다.

``` dart
const msPerSecond = 1000;
const secondsUntilRetry = 5;
const msUntilRetry = secondsUntilRetry * msPerSecond;
```
더 자세한 것은 Numbers in Dart 를 참고하자.

- #### Strings (문자열)

Dart 문자열(String 객체)는 UTF-16 코드 단위 시퀀스를 유지한다. 작은 따옴표(`'`) 또는 큰 따옴표(`"`)를 사용하여 문자열을 만들 수 있다.

``` dart
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```

${expression}을 사용하여 표현식의 값을 문자열 안에 넣을 수 있다. 표현식이 식별자인 경우 {}를 건너뛸 수 있다.  Dart에서 객체에 해당하는 문자열을 얻으려면 객체의 toString() 메서드를 호출한다.

``` dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
         'Dart has string interpolation, '
         'which is very handy.');

assert('That deserves all caps. '
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. '
        'STRING INTERPOLATION is very handy!');
```

(참고: `==` 연산자는 두 개체가 동일한지 여부를 테스트한다. 두 문자열이 동일한 코드 단위 순서로 구성되면 동일하다.)

문자열 리터럴을 인접 시키거나 `+` 연산자를 사용하여 문자열을 연결할 수 있다.

``` dart
var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
assert(s1 ==
    'String concatenation works even over '
        'line breaks.');

var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```
여러 줄 문자열을 만드는 또 다른 방법: 작은 따옴표 또는 큰 따옴표를 이용하여 삼중따옴표를 구성한다.

``` dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```

r을 접두어로 지정하여 "raw" 문자열을 생성할 수 있다.

``` dart
var s = r'In a raw string, not even \n gets special treatment.';
```

유니코드 문자를 문자열로 표현하는 방법에 대한 자세한 내용은  Runes and grapheme clusters를 참조한다.

리터럴 문자열은 interpolated 표현식이 null 또는 숫자, 문자열 또는 bool 값으로 평가되는 컴파일 시간 상수인 한 컴파일 시간 상수이다.

``` dart
// These work in a const string.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// These do NOT work in a const string.
var aNum = 0;
var aBool = true;   
var aString = 'a string';
const aConstList = [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString';
// const invalidConstString = '$aNum $aBool $aString $aConstList';
```
문자열 사용에 대한 자세한 내용은 Strings and regular expressions 을 참조한다.

