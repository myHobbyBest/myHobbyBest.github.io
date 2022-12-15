---
title:  "Comments "  
date:   2022-12-11 12:45:12 +0900
categories: [Flutter, Dart]
tag: [Comments]
toc: true
---
### Comments (주석)

Dart는 한 줄 주석, 여러 줄 주석 및 문서형 주석을 지원한다.

- #### 한 줄 주석

한 줄 주석은 `//`로 시작합니다. `//`과 줄 끝 사이의 모든 내용은 Dart 컴파일러에서 무시된다.

```dart
void main() {
  // TODO: refactor into an AbstractLlamaGreetingFactory?
  print('Welcome to my Llama farm!');
}
```

- #### 여러 줄 주석

여러 줄 주석은 `/*`로 시작하여 `*/`로 끝난다. `/*`와 `*/` 사이의 모든 내용은 Dart 컴파일러에서 무시된다(주석이 문서 주석이 아닌 경우; 다음 섹션 참조). 여러 줄 주석은 중첩될 수 있다.

```dart
void main() {
  /*
   * This is a lot of work. Consider raising chickens.

  Llama larry = Llama();
  larry.feed();
  larry.exercise();
  larry.clean();
   */
}
```

- #### 문서형 주석

문서형 주석은 `///` 또는 `/**`로 시작하는 여러 줄 또는 한 줄 주석이다. 연속된 줄에 `///`를 사용하면 여러 줄 문서 주석과 같은 효과가 있다.

문서 주석 내에서 해석기는 대괄호로 묶이지 않은 모든 텍스트를 무시한다. 대괄호를 사용하여 클래스, 메서드, 필드, 최상위 변수, 함수 및 매개 변수를 참조할 수 있다. 괄호 안의 이름은 문서화된 프로그램 요소의 어휘 범위에서 해석된다.

다음은 다른 클래스 및 인수에 대한 참조가 있는 문서 주석의 예이다.

``` dart
/// A domesticated South American camelid (Lama glama).
///
/// Andean cultures have used llamas as meat and pack
/// animals since pre-Hispanic times.
///
/// Just like any other animal, llamas need to eat,
/// so don't forget to [feed] them some [Food].

class Llama {
  String? name;

  /// Feeds your llama [food].
  ///
  /// The typical llama eats one bale of hay per week.
  void feed(Food food) {
    // ...
  }

  /// Exercises your llama with an [activity] for
  /// [timeLimit] minutes.
  void exercise(Activity activity, int timeLimit) {
    // ...
  }
}
```

클래스에 생성된 문서에서 [feed]는 feed 메서드에 대한 문서로의 링크가 되고 [Food]는 Food 클래스에 대한 문서로의 링크가 된다.

Dart 코드를 해석하여 HTML 문서를 생성하려면 Dart의 문서 생성 도구인 dart doc를 사용할 수 있다. 생성된 문서의 예는 Dart API 문서를 참조하자. 여러분의 의견을 구조화하는 방법에 대한 조언은 Effective Dart: Documentation을 참조하자.

