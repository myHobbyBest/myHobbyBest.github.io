---
title:  "Control flow statements"  
date:   2022-12-13 10:05:45 +0900
categories: [Flutter, Dart]
tag: [Control flow statements]
toc: true
---
### 제어 흐름 명령문(Control flow statements)

다음 중 하나를 사용하여 Dart 코드의 흐름을 제어할 수 있다.

- `if` and `else`
- `for` loops
- `while` and `do-while` loops
- `break` and `continue`
- `switch` and `case`
- `assert`

예외( Exceptions)에 설명된 대로 `try-catch` 및 `throw`를 사용하여 제어 흐름에 영향을 줄 수도 있다.

- #### `If` and `else`

Dart는 다음 예제와 같이 선택적 `else` 문이 있는 `if` 문을 지원합니다. conditional expressions 도 참조하라.

``` dart
if (isRaining()) {
  you.bringRainCoat();
} else if (isSnowing()) {
  you.wearJacket();
} else {
  car.putTopDown();
}
```
명령문 조건은 부울 값으로 평가되는 표현식이어야 한다. 자세한 내용은 Booleans을 참조하라.

- #### For loops

표준 `for` 루프를 사용하여 반복할 수 있다. 예를 들어:

``` dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
```
Dart의 `for` 루프 내부의 클로저는 인덱스 값을 캡처하여 JavaScript에서 발견되는 일반적인 함정을 피한다. 다음 예를 고려해보자.

``` dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}

for (final c in callbacks) {
  c();
}
```
출력은 예상대로 0과 1이다. 대조적으로, 예제는 JavaScript에서 2를 인쇄한 다음 2를 인쇄합니다.

반복하려는 객체가 Iterable(예: List 또는 Set)이고 현재 반복 카운터를 알 필요가 없는 경우 for-in 형식의 반복(iteration)을 사용할 수 있다.

``` dart
for (final candidate in candidates) {
  candidate.interview();
}
```
(팁: for-in 사용을 연습하려면  Iterable collections codelab을 참고하자.)

Iterable 클래스에는 또 다른 방법으로 forEach() 메서드가 있다.

``` dart
var collection = [1, 2, 3];
collection.forEach(print); // 1 2 3
```

- #### While 과 do-while


