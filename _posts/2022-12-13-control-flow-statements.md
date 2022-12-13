---
title:  "Control flow statements"  
date:   2022-12-13 21:30:26 +0900
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

- #### for 루프

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

- #### while 과 do-while

`while` 루프는 루프 앞에 있는 조건을 평가한다.

``` dart
while (!isDone()) {
  doSomething();
}
```

`do-while` 루프는 루프 뒤의 조건을 평가한다.

``` dart
do {
  printLine();
} while (!atEndOfPage());
```

- #### break 와 continue

`break`는 루프를 중지하기 위해 사용한다.

``` dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
```

`continue` 는 다음번 루프 반복으로 건너뜁니다.

``` dart
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}
```

`list` 나 `set`과 같은 Iterable을 사용하는 경우 위 예제를 다르게 작성할 수 있다.

``` dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```

- #### switch 와 case


Dart의 Switch 문은 `==`를 사용하여 정수, 문자열 또는 컴파일 타임 상수를 비교한다. 비교 대상은 모두 같은 클래스의 인스턴스여야 하며(하위 유형이 아님) 클래스는 `==` 를 재정의하면 안 된다. 열거형 유형(enum type)은 switch 문에서 잘 작동한다.

비어 있지 않은 각 `case` 절은 일반적으로 `break` 문으로 끝난다. 비어 있지 않은 `case` 절을 종료하는 다른 유효한 방법은 `continue`, `throw` 또는 `return` 문이다.

일치하는 `case` 절이 없을 때 `default` 절을 사용하여 코드를 실행한다.

``` dart
var command = 'OPEN';
switch (command) {
  case 'CLOSED':
    executeClosed();
    break;
  case 'PENDING':
    executePending();
    break;
  case 'APPROVED':
    executeApproved();
    break;
  case 'DENIED':
    executeDenied();
    break;
  case 'OPEN':
    executeOpen();
    break;
  default:
    executeUnknown();
}
```

다음 예에서는 `case` 절에서 `break` 문을 생략하여 오류를 생성한다.

``` dart
var command = 'OPEN';
switch (command) {
  case 'OPEN':
    executeOpen();
    // ERROR: Missing break

  case 'CLOSED':
    executeClosed();
    break;
}
```
그러나 Dart는 비어 있는 `case` 절을 지원하므로 다음과 같은 형태의 fall-through를 허용합니다.

``` dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED': // Empty case falls through.
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNowClosed();
    break;
}
```
폴스루(fall-through)를 원하는 경우 `continue` 문과 레이블을 사용할 수 있다.

``` dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED':
    executeClosed();
    continue nowClosed;
  // Continues executing at the nowClosed label.

  nowClosed:
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNowClosed();
    break;
}
```

`case` 절은 해당 절의 범위 내에서 만 볼 수 있는 지역 변수를 가질 수 있다.

- #### Assert 문

개발 중에 부울 조건이 false인 경우 assert 문(assert(condition, optionalMessage);)을 사용하여 정상적인 실행을 중단한다. 여기 둘러보기(tour) 전체에서 assert 문의 예를 찾을 수 있다. 다음에 몇 가지 더 있다.

``` dart
// Make sure the variable has a non-null value.
assert(text != null);

// Make sure the value is less than 100.
assert(number < 100);

// Make sure this is an https URL.
assert(urlString.startsWith('https'));
```
`assert`에 메시지를 첨부하려면 `assert`의 두 번째 인수로 문자열을 추가한다-선택적으로 뒤에 쉼표(trailing comma) 를 사용한다.

``` dart
assert(urlString.startsWith('https'),
    'URL ($urlString) should start with "https".');
```

