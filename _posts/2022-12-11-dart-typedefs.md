---
title:  "Typedefs "  
date:   2022-12-11 11:26:10 +0900
categories: [Flutter, Dart]
tag: [Typedefs]
toc: true
---
### Typedefs

유형 별칭 (alias) (`typedef` 키워드로 선언되기 때문에 흔히 `typedef`라고 함)는 유형을 참조하는 간결한 방법이다. 다음은 `IntList`라는 유형 별칭을 선언하고 사용하는 예이다.

``` dart
typedef IntList = List<int>;
IntList il = [1, 2, 3];
```

유형 alias 는 유형 매개변수를 가질 수 있다.

``` dart
typedef ListMapper<X> = Map<X, List<X>>;
Map<String, List<String>> m1 = {}; // Verbose.
ListMapper<String> m2 = {}; // Same thing but shorter and clearer.
```

(주: 버전 2.13 이전에는 typedef가 함수 유형으로 제한되었다. 새 `typedef`를 사용하려면 언어 버전이 2.13 이상이어야 한다.)

대부분의 경우에 함수에 대해 `typedef` 대신 인라인 함수 유형을 사용하는 것이 좋다. 그러나 함수 `typedef`는 여전히 유용할 수 있다.

``` dart
typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  assert(sort is Compare<int>); // True!
}
```

---
< PREFER inline function types over typedefs >
Dart 1에서는 필드, 변수 또는 제네릭 형식 인수에 대해 함수 형식을 사용하려면 먼저 이에 대한 typedef를 정의해야 했지만  Dart 2는 유형 주석이 허용되는 모든 곳에서 사용할 수 있는 함수 유형 구문을 지원한다.

``` dart
class FilteredObservable {
  final bool Function(Event) _predicate;
  final List<void Function(Event)> _observers;

  FilteredObservable(this._predicate, this._observers);

  void Function(Event)? notify(Event event) {
    if (!_predicate(event)) return null;

    void Function(Event)? last;
    for (final observer in _observers) {
      observer(event);
      last = observer;
    }

    return last;
  }
}
```

---
