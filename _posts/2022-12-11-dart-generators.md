---
title:  "제너레이터 (Generators) "  
date:   2022-12-11 10:10:09 +0900
categories: [Flutter, Dart]
tag: [Generators]
toc: true
---
### Generators

연속되는 값들을 천천히 생성해야 하는 경우에는 제너레이터 함수를 사용하는 것이 좋다. Dart는 두 종류의 제너레이터 함수를 기본적으로 지원한다.

- 동기 제너레이터: Iterable 객체를 반환한다.
- 비동기 제너레이터: Stream 개체를 반환한다.
동기식 제너레이터 함수를 구현하려면 함수 본문을 ``sync*``로 표시하고 yield 문을 사용하여 값을 전달한다.

``` dart
Iterable<int> naturalsTo(int n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
```

비동기 생성기 함수를 구현하려면 함수 본문을 ``async*``로 표시하고 yield 문을 사용하여 값을 전달한다.

``` dart
Stream<int> asynchronousNaturalsTo(int n) async* {
  int k = 0;
  while (k < n) yield k++;
}
```

생성기가 재귀적이라면 ``yield*``를 사용하여 성능을 향상시킬 수 있다.

``` dart
Iterable<int> naturalsDownFrom(int n) sync* {
  if (n > 0) {
    yield n;
    yield* naturalsDownFrom(n - 1);
  }
}
```
