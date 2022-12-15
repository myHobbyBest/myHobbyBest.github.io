---
title:  "Exceptions"  
date:   2022-12-14 09:05:02 +0900
categories: [Flutter, Dart]
tag: [Exceptions]
toc: true
---
### 예외처리(Exceptions)

Dart 코드는 예외를 발생(throw) 시키고 처리,해결(catch)할 수 있다. 예외(exception)는 예상치 못한 일이 발생했음을 나타내는 오류이다. 예외가 포착되지 않으면 예외를 발생시킨 격리가 일시 중단되고 일반적으로 격리와 해당 프로그램이 종료된다.

Java와 달리 Dart의 모든 예외는 확인되지 않은 예외이다. 메서드는 어떤 예외를 발생(throw)시킬 수 있는지 선언하지 않으며 예외를 처리할(catch)필요가 없다.

Dart는 Exception 및 Error 유형뿐만 아니라 수 많은 사전 정의된 하위 유형을 제공한다. 물론 자신 만의 예외를 정의할 수 있다. 그러나 Dart 프로그램은 Exception 및 Error 객체 뿐 아니라 null이 아닌 모든 객체를 예외로 발생 시킬 수 있다.

- #### 예외 생성(Throw )

다음은 예외를 던지거나 발생시키는 예이다.

``` dart
throw FormatException('Expected at least 1 section');
```

임의의 개체를 발생 시킬 수도 있다.

``` dart
throw 'Out of llamas!';
```

(참고: 프로덕션 품질 코드는 일반적으로 오류 또는 예외를 구현하는 유형을 발생시킨다.)

예외를 던지는(발생시키는) 것은 표현식이기 때문에 `=>` 문 뿐만 아니라 표현식을 허용하는 다른 모든 곳에서 예외를 던질(발생시킬) 수 있다.

``` dart
void distanceTo(Point other) => throw UnimplementedError();
```

- #### 예외의 처리 (Catch)

예외를 포착하거나 캡처하면 예외가 전파되지 않는다. (예외를 다시 발생시키지 않는 한). 예외를 포착하면 이를 처리할 기회가 생긴다.

``` dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
```

둘 이상의 예외 유형을 `throw`할 수 있는 코드를 처리하려면 여러 `catch` 절을 지정할 수 있다. 던져진 객체의 유형과 일치하는 첫 번째 `catch` 절이 예외를 처리한다. `catch` 절이 유형을 지정하지 않으면 해당 절은 모든 유형의 `throw`된 객체를 처리할 수 있다.

``` dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
}
```

앞의 코드에서 볼 수 있듯이 `on` 또는 `catch`를 사용하거나 둘 다를 사용할 수 있다. 예외 유형을 지정해야 하는 경우 `on`을 사용한다. 예외 처리기에 예외 개체가 필요한 경우 `catch`를 사용한다.

`catch()`에 하나 또는 두 개의 매개변수를 지정할 수 있다. 첫 번째는 `throw`된 예외이고 두 번째는 스택 추적(`StackTrace` 개체)이다.

``` dart
try {
  // ···
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```

예외의 전파를 허용하면서 예외를 부분적으로 처리하려면 rethrow 키워드를 사용한다.

``` dart
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    rethrow; // Allow callers to see the exception.
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
```

- #### `finally`

예외 발생 여부에 관계없이 일부 코드가 실행되도록 하려면 `finally` 절을 사용한다. 예외와 일치하는 `catch` 절이 없으면 `finally` 절이 실행된 후 예외가 전파된다.

``` dart
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}
```

`finally` 절은 일치하는 `catch` 절 다음에 실행된다.

``` dart
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```

예외의 처리에 관해서는 liblary 둘러보기의 Exceptions 섹션을 자세히 읽어보기 바란다.