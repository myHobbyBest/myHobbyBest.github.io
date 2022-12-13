---
title:  "Functions"  
date:   2022-12-12 18:40:22 +0900
categories: [Flutter, Dart]
tag: [Functions]
toc: true
---
### 함수 (Functions)

Dart는 진정한 객체 지향 언어이므로 함수도 객체이며 유형이 Function이다. 이는 함수를 변수에 할당하거나 다른 함수에 인수로 전달할 수 있음을 의미한다. 마치 함수인 것처럼 Dart 클래스의 인스턴스를 호출할 수도 있다. 자세한 내용은 호출 가능 클래스를 참조한다.

다음은 함수 구현의 예이다.

``` dart
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

Effective Dart는 공개 API에 대한 유형 주석을 권장하지만 유형을 생략해도 함수는 계속 작동한다.

``` dart
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

하나의 표현식만 포함하는 함수의 경우 단축 구문을 사용할 수 있다.

``` dart
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

`=> expr` 구문은 { return expr; } 구문의 단축표현이다.  `=>` 표현은 화살표 구문이라고도 합다.

(참고: 화살표(`=>`)와 세미콜론(`;`) 사이에는 명령문이 아닌 표현식만 나타날 수 있다. 예를 들어 if 문은 넣을 수 없지만 조건식은 사용할 수 있다.)

- #### 매개변수 (Parameters)

함수는 필수 위치 매개변수를 얼마든지 가질 수 있습니다. 그 뒤에는 이름있는 매개변수 또는 선택적 위치 매개변수가 올 수 있다(둘 다는 아님).

 ( 참고: 일부 API(특히 Flutter 위젯 생성자)는 필수 매개변수의 경우에도 이름있는 매개변수만 사용합니다. 자세한 내용은 다음 섹션을 참조한다.)

함수에 인수를 전달하거나 함수 매개 변수를 정의할 때 후행 쉼표를 사용할 수 있다.

- 이름있는 매개변수
이름있는 매개변수는 명시적으로 `required`로 표시되지 않는 한 선택 사항이다.

함수를 정의할 때 {param1, param2, …}를 사용하여 이름있는 매개변수를 지정한다. 기본값을 제공하지 않거나 이름있는 매개변수를 `required`로 표시하지 않으면 해당 유형은 기본값이 null이 되므로 null을 허용해야 한다.

``` dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool? bold, bool? hidden}) {...}
```

함수를 호출할 때 paramName: value를 사용하여 이름있는 인수를 지정할 수 있다. 예를 들어:

``` dart
enableFlags(bold: true, hidden: false);
```

null 이외의 이름있는 매개 변수에 대한 기본값을 정의하려면 `=`를 사용하여 기본값을 지정한다. 지정된 값은 컴파일 타임 상수여야 합다. 예를 들어:

``` dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {...}

// bold will be true; hidden will be false.
enableFlags(bold: true);
```

그렇지 않고 이름이 지정된 매개변수를 필수로 지정하여 호출자가 매개변수에 대한 값을 제공하도록 요구하기를 원하는 경우 `required ` 주석을 추가한다.

``` dart
const Scrollbar({super.key, required Widget child});
```

누군가 `child` 인수를 지정하지 않고 `Scrollbar`를 만들려고 하면 디버거가 문제를 보고한다.

  (참고: `required` 로 표시된 매개변수는 여전히 null을 허용할 수 있다.)

  ``` dart
  const Scrollbar({super.key, required Widget? child});
  ```

위치 매개변수를 먼저 배치하고 싶을 수 있지만 Dart는 이를 요구하지 않는다. Dart는 API에 적합하다면 이름있는 매개변수를 매개변수 목록의 아무 곳에나 배치할 수 있도록 허용한다.

``` dart
repeat(times: 2, () {
  ...
});
```

- 선택적 위치 매개변수(Optional positional parameters)

함수 매개변수 세트를 []로 감싸면 선택적 위치 매개변수로 표시된다. 기본값을 제공하지 않으면 해당 유형은 기본값이 null이 되므로 null을 허용해야 한다.

``` dart
String say(String from, String msg, [String? device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

다음은 선택적 매개변수 없이 이 함수를 호출하는 예이다.

```dart
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
```
다음은 세 번째 매개변수를 사용하여 이 함수를 호출하는 예이다.

``` dart
assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');
```

null 이외의 선택적 위치 매개변수에 대한 기본값을 정의하려면 `=`를 사용하여 기본값을 지정한다. 지정된 값은 컴파일 타임 상수여야 한다. 예를 들어:

``` dart
String say(String from, String msg, [String device = 'carrier pigeon']) {
  var result = '$from says $msg with a $device';
  return result;
}

assert(say('Bob', 'Howdy') == 'Bob says Howdy with a carrier pigeon');
```

- #### main() 함수 ( The main() function )

모든 앱에는 앱의 진입점 역할을 하는 최상위 main() 함수가 있어야 한다. main() 함수는 void를 반환하고 인수에 대한 선택적인 `List<String>` 매개 변수가 있다.

다음은 간단한 main() 함수이다.

``` dart
void main() {
  print('Hello, World!');
}
```

다음은 인수를 사용하는 명령줄 앱용 main() 함수의 예이다.

``` dart
// Run the app like this: dart args.dart 1 test
void main(List<String> arguments) {
  print(arguments);

  assert(arguments.length == 2);
  assert(int.parse(arguments[0]) == 1);
  assert(arguments[1] == 'test');
}
```
`args` 라이브러리를 사용하여 명령줄 인수를 정의하고 구문 분석할 수 있다.

- #### 일급 객체로서의 함수(Functions as first-class objects)

함수를 매개변수로 다른 함수에 전달할 수 있다. 예를 들어:

``` dart
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
```

다음과 같이 변수에 함수를 할당할 수도 있다.

```dart
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

이 예제에서는 익명 함수를 사용한디. 다음 섹션에서 이에 대해 자세히 알아보자.

- #### 익명 함수 (Anonymous functions)

대부분의 함수는 main() 또는 printElement()와 같이 이름이 지정된다. 익명 함수 때로는 람다 또는 클로저 라고 부르는 이름 없는 함수를 만들 수도 있다. 예를 들어 컬렉션에서 익명 함수를 추가하거나 제거할 수 있도록 변수에 익명 함수를 할당할 수 있다.

익명 함수는 이름있는 함수와 비슷하게 생겼다. 0개 또는 그 이상의 매개변수가 쉼표로 구분되고 선택적 유형 주석이 괄호 사이에 있다.

다음 코드 블록에는 함수의 본문이 포함되어 있다.

``` dart
([[Type] param1[, …]]) {
  codeBlock;
};
```

다음 예제에서는 형식화되지 않은 (untyped) 매개 변수 `item`을 사용하여 익명 함수를 정의하고 이를 map 함수에 전달합니다. `list`의 각 항목에 대해 호출되는 이 함수는 각 문자열을 대문자로 변환한다. 그런 다음 forEach에 전달된 익명 함수에서 변환된 각 문자열이 문자열의 길이와 함께 출력된다.

``` dart
void main() {}
  const list = ['apples', 'bananas', 'oranges'];
  list.map((item) {
    return item.toUpperCase();
  }).forEach((item) {
    print('$item: ${item.length}');
  });
}
```

콘솔 출력은 다음과 같다.

``` console
APPLES: 6
BANANAS: 7
ORANGES: 7
```

함수에 단일 표현식 또는 return 문만 포함된 경우 화살표 표기법을 사용하여 단축할 수 있다. 다음 줄을 DartPad에 붙여넣고 실행을 클릭하여 기능적으로 동일한지 확인 해보자.

``` dart
list
    .map((item) => item.toUpperCase())
    .forEach((item) => print('$item: ${item.length}'));
```

- #### 어휘 범위 (Lexical scope)

Dart는 어휘적으로 범위가 지정된 언어이다. 즉, 변수의 범위는 단순히 코드의 레이아웃에 따라 정적으로 결정된다. "중괄호를 바깥쪽으로 따라가면" 변수가 범위에 있는지 확인할 수 있다.

다음은 각 범위 수준에서 변수가 있는 중첩 함수의 예이다.

``` dart
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      assert(topLevel);
      assert(insideMain);
      assert(insideFunction);
      assert(insideNestedFunction);
    }
  }
}
```

`nestedFunction()`이 어떻게 최상위 수준까지의 모든 수준에서 변수를 사용할 수 있는지 확인하자.

- #### 어휘 클로저 (Lexical closures)

클로저는 함수가 원래 범위 밖에서 사용되는 경우에도 어휘 범위의 변수에 액세스할 수 있는 함수 개체이다.
함수는 주변 범위에 정의된 변수를 닫을 수 있다. 다음 예제에서 makeAdder()는 변수 addBy를 캡처한다. 반환된 함수가 가는 곳마다 addBy를 기억한다.

``` dart
/// Returns a function that adds [addBy] to the
/// function's argument.
Function makeAdder(int addBy) {
  return (int i) => addBy + i;
}

void main() {
  // Create a function that adds 2.
  var add2 = makeAdder(2);

  // Create a function that adds 4.
  var add4 = makeAdder(4);

  assert(add2(3) == 5);
  assert(add4(3) == 7);
}
```

- #### 함수의 기능이 동일한지 테스트 (Testing functions for equality)

다음은 최상위 함수, 정적 메서드 및 인스턴스 메서드가 동일한지 테스트하는 예이다.

``` dart
void foo() {} // A top-level function

class A {
  static void bar() {} // A static method
  void baz() {} // An instance method
}

void main() {
  Function x;

  // Comparing top-level functions.
  x = foo;
  assert(foo == x);

  // Comparing static methods.
  x = A.bar;
  assert(A.bar == x);

  // Comparing instance methods.
  var v = A(); // Instance #1 of A
  var w = A(); // Instance #2 of A
  var y = w;
  x = w.baz;

  // These closures refer to the same instance (#2),
  // so they're equal.
  assert(y.baz == x);

  // These closures refer to different instances,
  // so they're unequal.
  assert(v.baz != w.baz);
}
```

- #### 반환 값 (Return values)

모든 함수는 값을 반환한다. 반환 값이 지정되지 않은 경우  ` return null;`  문이 함수 본문에 암시적으로 추가된다.

``` dart
foo() {}

assert(foo() == null);
```
