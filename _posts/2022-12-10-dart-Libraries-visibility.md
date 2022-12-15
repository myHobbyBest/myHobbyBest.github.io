---
title:  "라이브러리 와 가시성(Libraries and visibility)"  
date:   2022-12-10 16:03:09 +0900
categories: [Flutter, Dart]
tag: [Libraries, visibility]
toc: true
---

### 라이브러리 와 가시성 (Libraries and visibility)

가져오기(import) 및 라이브러리 지시문은 모듈식 및 공유 가능한 코드 기반을 만드는 데 도움이 된다. 라이브러리는 API를 제공할 뿐만 아니라 비공개성?(프라이버시)의 단위가 된다. 언더스코어(_)로 시작하는 식별자는 라이브러리 내에서만 인식할 수 있다. 라이브러리 지시문을 사용하지 않더라도 모든 Dart 앱은 라이브러리이다.

라이브러리는 패키지를 사용하여 배포할 수 있다.
(주: Dart가 public 또는 private와 같은 접근 한정자 키워드 대신 언더스코(_)을 사용하는 이유가 궁금하다면 SDK 문서 33383을 참조하자)

- #### 라이브러리를 사용하는 방법 ( Using libraries )
`import` 를 사용하여 한 라이브러리의 네임스페이스가 다른 라이브러리의 범위에서 사용되는 방식을 지정한다.

예를 들어 Dart 웹 앱은 일반적으로 다음과 같이 가져올 수 있는 dart:html 라이브러리를 사용한다.

``` dart
import 'dart:html';
```

`import` 에 필요한 유일한 인수는 라이브러리를 지정하는 URI 이다. 내장 라이브러리의 경우 URI에 특별한 dart: 스키마가 있다. 다른 라이브러리의 경우 파일 시스템 경로 또는 패키지: 스키마를 사용할 수 있다. package: 스키마는 `pub` 도구와 같은 패키지 관리자가 제공하는 라이브러리를 지정한다. 예를 들어:

``` dart
import 'package:test/test.dart';
```
(주 : URI는 단일 리소스 식별자를 나타낸다. URL(Uniform Resource Locator)은 일반적인 종류의 URI이다.)

- #### 라이브러리 접두사 지정 (Specifying a library prefix)

충돌하는 식별자가 있는 두 개의 라이브러리를 가져오는 경우 하나 또는 두 라이브러리 모두에 대해 접두사를 지정할 수 있다. 예를 들어 `library1`과 `library2` 모두에 Element 클래스가 있는 경우 다음과 같이 코딩할 수 있다.

``` dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

- #### 라이브러리의 일부만 가져오기 (Importing only part of a library)

라이브러리의 일부만 사용하려는 경우 라이브러리를 선택적으로 가져올 수 있다. 예를 들어:

``` dart
// Import only foo.
import 'package:lib1/lib1.dart' show foo;

// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;

```

- #### 지연된 라이브러리 로드 (Lazily loading a library)

지연 로딩(레이지 로딩이라고도 함)을 사용하면 라이브러리가 필요한 경우와 시간에 웹 앱이 온디멘드로 라이브러리를 로드할 수 있다. 다음은 지연된 로드를 사용할 수 있는 몇 가지 경우이다.

- 웹 앱의 초기 시작 시간을 줄이기 위해.
- 예를 들어 알고리즘의 대체 구현을 시도하는 A/B 테스트를 수행한다.
- 선택적 화면 및 대화 상자와 같이 거의 사용되지 않는 기능을 로드한다.

(주: 다트 컴파일 js만이 지연 로딩을 지원한다. Flutter와 Dart VM은 지연된 로딩을 지원하지 않는다. 자세한 내용은 sdk issue #33118 및 #27776을 참조하자.)

라이브러리를 지연 로딩하려면 먼저 __deferred as__ 를 사용하여 라이브러리를 가져와야 한다.

``` dart
import 'package:greetings/hello.dart' deferred as hello;
```

라이브러리가 필요한 경우 라이브러리 식별자를 사용하여 loadLibrary()를 호출한다.

``` dart
Future<void> greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```

이전 코드에서 await 키워드는 라이브러리가 로드될 때까지 실행을 일시 중지한다.

async 및 await에 대한 자세한 내용은 비동기 지원을 참조하자.

라이브러리에서 `loadLibrary()`를 여러 번 호출하는 것도 아무문제 없이 할 수 있다. 이때 라이브러리는 한 번만 로드된다.

지연된 로드를 사용할 때 다음 사항에 유의한다.

- 지연된 라이브러리의 상수는 가져오는 파일의 상수가 아니다. 이러한 상수는 지연된 라이브러리가 로드될 때까지 존재하지 않는다는 점을 기억하자.
- 가져오는 파일에서 지연된 라이브러리의 유형을 사용할 수 없다. 대신 지연된 라이브러리와 가져오기 파일 모두에서 가져온 라이브러리로 인터페이스 유형을 이동하는 것을 고려해야 한다.
- Dart는 `deferred`를 네임스페이스로 사용하여 정의한 네임스페이스에 `loadLibrary()`를 암시적으로 삽입한다. `loadLibrary()` 함수는 Future를 반환한다.

- #### Implementing libraries (라이브러리구현)

다음을 포함하여 라이브러리 패키지를 구현하는 방법에 대한 조언은 Create Library Packages을 참조한다.

- 라이브러리 소스 코드 구성 방법.
- 내보내기 지시문을 사용하는 방법.
- 부품 지시문을 사용하는 경우.
- 라이브러리 지시문을 사용하는 경우.
- 여러 플랫폼을 지원하는 라이브러리를 구현하기 위해 조건부 가져오기 및 내보내기를 사용하는 방법

### 참고 자료

- https://dart.dev/guides/language/language-tour 