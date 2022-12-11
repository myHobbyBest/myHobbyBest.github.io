---
title:  "Variables"  
date:   2022-12-11 15:10:20 +0900
categories: [Flutter, Dart]
tag: [Variables]
toc: true
---
### Variables

다음은 변수를 만들고 초기화하는 예이다.

``` dart
var name = 'Bob';
```
변수는 참조를 저장한다. name이라는 변수에는 값이 "Bob"인 String 개체에 대한 참조가 포함되어 있다.

name 변수의 유형은 String으로 유추되지만 지정하여 해당 유형을 변경할 수 있다. 개체가 단일유형으로 제한되지 않는다면  개체 유형(또는 필요한 경우 동적유형)을 지정한다.

``` dart
Object name = 'Bob';
```
또 다른 옵션은 유추할 형식을 명시적으로 선언하는 것이다.

``` dart
String name = 'Bob';
```

(주: 이 페이지는 로컬 변수에 유형 주석 대신 var를 사용하는 스타일 가이드 권장 -style guide recommendation- 사항을 따른다.)

- #### 기본값 (Default value)

null 이 허용되는 유형의 초기화되지 않은 변수의 초기값은 null이다. (null 안전성을 선택하지 않은 경우 모든 변수는 nullable 유형을 가진다.) Dart의 다른 모든 것과 마찬가지로 숫자도 객체이기 때문에 숫자 유형 변수도 처음에는 null이다.

``` dart
int? lineCount;
assert(lineCount == null);
```
(주: 프로덕션 코드(개발 완료되어 사용중인 코드)는 ``assert()`` 호출을 무시한다. 반면에 개발 중에 ``assert(condition)`` 는 condition이 false인 경우 예외를 발생시킨다. 자세한 내용은  ``assert``을 참조한다.)

null 안전성이 활성화된 경우 null을 허용하지 않는 변수의 값은 사용하기 전에 초기화해야 한다.

```dart
int lineCount = 0;
```

지역 변수는 선언핼떄 초기화할 필요는 없지만 사용하기 전에는 값을 할당해야 한다. 예를 들어 다음 코드는 Dart가 ``print()``에 전달될 때 ``lineCount``가 null이 아님을 감지할 수 있기 때문에 유효하다.

``` dart
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
```

최상위 수준 변수와 클래스 변수는 뒤늦게 초기화된다. 초기화 코드는 변수가 처음 사용될 때 실행된다.

- #### Late variables

Dart 2.12는 ``late`` 수정자를 추가했다. 두 가지 사용예가 있다. 

- 선언 후에 초기화되는 null을 허용하지 않는 변수를 선언한다.
- 변수를 뒤늦게 초기화한다.

종종 Dart의 제어 흐름 분석은 null을 허용하지 않는 변수가 사용되기 전에 null이 아닌 값으로 설정되는 경우를 감지할 수 있지만 때때로 분석이 실패한다. 두 가지 일반적인 경우는 최상위 변수와 인스턴스 변수이다. Dart는 종종 설정되었는지 여부를 결정할 수 없으므로 시도하지 않는다.

변수가 사용되기 전에 설정되는 것이 확실하지만 Dart가 동의하지 않는 경우(에러가 발생하는 경우) 변수를 ``late``로 표시하여 오류를 수정할 수 있다.

``` dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
```
(주: ``late`` 선언된 변수를 초기화하지 못하면 변수를 사용할 때 런타임 오류가 발생한다.)

변수를 ``late``로 표시했지만 선언시 초기화하더라도 변수가 처음 사용될 때 초기화 프로그램이 실행됩니다. 이러한 지연 초기화는 몇 가지 경우에 유용합니다.

- 변수가 필요하지 않을 수 있으며 초기화하는 데 비용이 많이 든다.
- 인스턴스 변수를 초기화한 경우 그 이니셜라이저는 ``this``에 접근할 필요가 있다.

다음 예제에서 온도 변수가 사용되지 않으면 비용이 많이 드는 ``readThermometer()`` 함수가 호출되지 않는다.

```dart
// This is the program's only call to readThermometer().
late String temperature = readThermometer(); // Lazily initialized.
```

- #### ``Final`` 과 ``const``

변수의 값을 변경하지 않을 경우 ``var`` 대신 (또는 유형에 추가하여)  ``final`` 또는 ``const`` 를 사용하십시오. 최종 변수는 한 번만 설정할 수 있다.; ``const`` 변수는 컴파일 타임 상수이다. (Const 변수는 암시적으로 ``final`` 변수이다.)

  (참고: 인스턴스 변수는 ``final``일 수 있지만 ``const``는 아니다.)

다음은 최종 변수를 만들고 설정하는 예이다.

``` dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';
```
``fianl`` 변수의 값은 변경할 수 없다.

```dart
// static analysis : error/warnang.
name = 'Alice'; // Error: a final variable can only be set once.
```

컴파일 타임 상수로 사용할 변수에는 ``const``를 사용한다. ``const`` 변수가 클래스 수준에 있는 경우 ``static const``로 표시한다. 변수를 선언하는 위치에서 값을 숫자나 리터럴 문자열 , ``const`` 변수 또는 상수에 대한 산술 연산 결과와 같은 컴파일 타임 상수로 설정한다.

```dart
const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```

``const`` 키워드는 단지 상수 변수를 선언하기 위한 것이 아니다. 이를 사용하여 상수 값을 생성하고 상수 값을 생성하는 생성자를 선언할 수도 있다. 모든 변수는 상수 값을 가질 수 있다.

```dart
var foo = const [];
final bar = const [];
const baz = []; // Equivalent to `const []`
```

위의 ``baz``와 같이 ``const`` 선언의 초기화 식에서 ``const``를 생략할 수 있습니다. 자세한 내용은 DON'T use const redundantly를 참조한다.

이전에 ``const`` 값을 가졌더라도 ``non-final``,``non-const`` 변수의 값은 변경할 수 있다.

``` dart
foo = [1, 2, 3]; // Was const []
```

``const`` 변수의 값은 변경할 수 없다.

```dart
// static analysis : error/warnang.
baz = [42]; // Error: Constant variables can't be assigned a value.
```

유형 확인 및 캐스트(``is`` 와 ``as``), 컬렉션 ``if`` 및 확산 연산자(``...`` 및 ``...?``)를 사용하는 상수를 정의할 수 있다.

``` dart
const Object i = 3; // Where i is a const Object with an int value...
const list = [i as int]; // Use a typecast.
const map = {if (i is int) i: 'int'}; // Use is and collection if.
const set = {if (list is List<int>) ...list}; // ...and a spread.
```

(참고: ``final`` 개체는 수정할 수 없지만 그 필드는 변경할 수 있다. 이에  비해 ``const`` 개체와 필드는 변경할 수 없다. 즉 __immutable__ 이다.)

``const``를 사용하여 상수값을 만드는 방법에 대한 자세한 내용은 List, map 및 class를 참조한다.




