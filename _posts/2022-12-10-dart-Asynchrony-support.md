---
title:  "비동기 지원(Asynchrony support) "  
date:   2022-12-10 20:10:09 +0900
categories: [Flutter, Dart]
tag: [Asynchrony]
toc: true
---
### 비동기 지원 (Asynchrony support)

Dart 라이브러리는 Future 또는 Stream 객체를 반환하는 함수로 가득 차 있다. 이러한 함수는 비동기 방식이다. 시간이 많이 소요될 수 있는 작업(예: I/O)을 설정한 후 해당 작업이 완료될 때까지 기다리지 않고 반환된다.

async 및 await 키워드는 비동기 프로그래밍을 지원하므로 동기 코드와 유사해 보이는 비동기 코드를 작성할 수 있다.

- #### Future 다루기

완료된 Future의 결과가 필요한 경우 두 가지 옵션이 있다.

- 여기에 설명된 대로 async 및 await를 사용한다. 또한  asynchronous programming codelab를 참조한다. 
- 라이브러리 둘러보기(the library tour.)에 설명된 대로 Future API를 사용한다.


async 및 await를 사용하는 코드는 비동기식이지만 동기식 코드와 매우 유사하다. 예를 들어 다음은 await를 사용하여 비동기 함수의 결과를 기다리는 코드의 일부이다.

``` dart
await lookUpVersion();
```

await를 사용하려면 그 코드가 async 함수(async로 표시된 함수) 안에 있어야 한다.

``` dart
Future<void> checkVersion() async {
  var version = await lookUpVersion();
  // Do something with version
}
```
(주: 비동기 함수는 시간이 많이 걸리는 작업을 수행할 수 있지만 해당 작업을 기다리지 않는다. 대신 async 함수는 첫 await 표현식을 만날 때까지만 실행된다. 그런 다음 Future 객체를 반환하고 await 표현식이 완료된 후에만 실행을 재개한다.)

try, catch 및 finally를 사용하여 await를 사용하는 코드에서 오류를 처리하고 정리한다.

``` dart
try {
  version = await lookUpVersion();
} catch (e) {
  // React to inability to look up the version
}
```

async 함수에서 await는 여러 번 사용할 수 있다. 예를 들어 다음 코드는 함수 결과를 세 번 기다린다.

``` dart
var entrypoint = await findEntryPoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

await 표현식에서 그 값은 일반적으로 Future이다. 그렇지 않은 경우 값은 자동으로 Future에 감싸진다(래핑). 이 Future 객체는 객체를 반환하겠다는 약속을 나타낸다. await 표현식의 값은 반환된 개체이다. await 표현식은 해당 개체를 사용할 수 있을 때까지 실행을 일시 중지한다.

await를 사용할 때 컴파일 타임 오류가 발생하면 await가 async 함수에 있는지 확인한다. 예를 들어 앱의 main() 함수에서 await를 사용하려면 main()의 본문을 async로 표시해야 한다.

``` dart
void main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
```
(주:앞의 예제에서는 결과를 기다리지 않고 비동기 함수(checkVersion())를 사용한다. 코드에서 함수 실행이 완료되었다고 가정하면 문제가 발생할 수 있다. 이 문제를 방지하기위해 unawaited_futures linter 규칙을 사용한다.)

futures, async, await 사용에 대한 대화형 소개는 asynchronous programming codelab 을 참조한다.

- #### 비동기 함수 선언 (Declaring async functions)

async 함수는 본문이 async 한정자로 표시된 함수이다.

함수에 async 키워드를 추가하면 Future를 반환한다. 예를 들어 문자열을 반환하는 다음 동기 함수를 고려해 보자.

``` dart
String lookUpVersion() => '1.0.0';
```

예를 들어 향후 구현에 시간이 많이 걸리기 때문에 비동기 함수로 변경하면 반환되는 값은 Future이다.
``` dart
Future<String> lookUpVersion() async => '1.0.0';
```
함수 본문은 Future API를 사용할 필요가 없다. Dart는 필요한 경우 Future 객체를 생성한다. 함수가  값을 반환하지 않는 경우라면 반환 유형을 Future<void>로 만든다.

futures, async, await 사용에 대한 대화형 소개는 asynchronous programming codelab을 참조한다.


- #### 스트림 다루기 

스트림에서 값을 가져와야 하는 경우 두 가지 옵션이 있다.

- async 와 비동기 for loop (await for)를 사용한다.
-  library tour에 설명된 대로 Stream API를 사용한다.

(주: await for를 사용하기 전에 코드가 더 명확해지는지 스트림의 모든 결과를 정말로 기다리고 싶은지 확인한다. 예를 들어 UI 프레임워크는 끝없는 이벤트 스트림을 보내기 때문에 일반적으로 UI 이벤트 리스너에 대해 await for를 사용하면 안된다.)

비동기 for loop 의 형식은 다음과 같다.

``` dart
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```
expression의 값은 Stream 유형이어야 한다. 실행은 다음과 같이 진행된다.

1. 스트림이 값을 내보낼 때까지 기다린다.
2. 내보낸 값으로 설정된 변수를 사용하여 for 루프의 본문을 실행한다.
3. 스트림이 닫힐 때까지 1과 2를 반복한다.

스트림 수신을 중지하려면 for loop 를 중단하고 스트림 구독을 취소하는 break 또는 return 문을 사용할 수 있다.

비동기 for loop 를 구현할 때 컴파일 타임 오류가 발생하면 await for가 async 함수에 있는지 확인한다. 예를 들어 앱의 main() 함수에서 비동기 for loop를 사용하려면 main() 본문을 async로 표시해야 한다.

``` dart
void main() async {
  // ...
  await for (final request in requestServer) {
    handleRequest(request);
  }
  // ...
}
```
일반적으로 비동기 프로그래밍에 대한 자세한 내용은 the library tour 의 dart:async 섹션을 참조하자.
