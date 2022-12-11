---
title:  "Metadata "  
date:   2022-12-11 11:26:10 +0900
categories: [Flutter, Dart]
tag: [Metadata]
toc: true
---
### Metadata

메타데이터를 사용하여 코드에 대한 추가 정보를 제공한다. 메타데이터 주석은 @ 문자로 시작하고 컴파일 시간 상수(예: deprecated)에 대한 참조 또는 상수 생성자에 대한 호출이 뒤따른다.

모든 Dart 코드에서 @Deprecated, @deprecated 및 @override의 세 가지 주석을 사용할 수 있다. @override 사용 예제는 클래스 확장을 참조한다. 다음은 @Deprecated 주석을 사용하는 예이다.

``` dart
class Television {
  /// Use [turnOn] to turn the power on instead.
  @Deprecated('Use turnOn instead')
  void activate() {
    turnOn();
  }

  /// Turns the TV's power on.
  void turnOn() {...}
  // ···
}
```
고유한 메타데이터 주석을 정의할 수 있다. 다음은 두 개의 인수를 사용하는 @Todo 주석을 정의하는 예이다.

``` dart
class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
```
다음은 @Todo 주석을 사용하는 예이다.
```dart
@Todo('Dash', 'Implement this function')
void doSomething() {
  print('Do something');
}
```
메타데이터는 라이브러리, 클래스, typedef, 유형 매개변수, 생성자, 팩토리, 함수, 필드, 매개변수 또는 변수 선언 앞과 가져오기 또는 내보내기 지시문 앞에 나타날 수 있다. 리플렉션을 사용하여 런타임에 메타데이터를 검색할 수 있다.