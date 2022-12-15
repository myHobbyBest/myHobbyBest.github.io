---
title:  "제네릭(Generics) "  
date:   2022-12-10 13:02:09 +0900
categories: [Flutter, Dart]
tag: [Generics, generic methods]
toc: true
---

### 제네릭 (Generics)

기본 배열 유형인 List에 대한 API 설명서를 보면 유형이 실제로 `List<E>`임을 알 수 있다.  `<…>`  표기법은 List 를 정규 유형 매개변수를 가지는 generic(또는 매개변수화된) type으로 표시한다. 규칙에 따라 대부분의 type 변수는 E, T, S, K 및 V와 같은 단일 문자 이름이 있다.

- #### 제네릭을 사용하는 이유?

유형 안전성을 위해 종종 제네릭이 필요하다. 하지만 그저 코드 실행을 허용하는 것보다 더 많은 이점이 있다.

- 제네릭 형식을 올바르게 지정하면 코드가 더 잘 생성된다.
- 제네릭을 사용하여 코드 중복을 줄일 수 있다.

List에 문자열 만 포함하려는 경우  `List<String>`으로 선언할 수 있다("문자열 리스트"라고 읽음). 이렇게 하면 본인이나 동료 프로그래머, 그리고 본인의 도구(IDE ?)가 문자열이 아닌 것을 List에 할당하는 것이 실수일 가능성이 있음을 미리 감지할 수 있다. 예를 들면 다음과 같다.

``` dart
// static analysis : error/warning
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
names.add(42); // Error
```

제네릭을 사용하는 또 다른 이유는 코드 중복을 줄이기 위해서 이다. 제네릭을 사용하면 정적해석의 잇점을 계속 활용하면서 단일 인터페이스로 여러 유형 간에 implementation(구현)을 공유할 수 있다. 예를 들어 객체 캐싱을 위한 인터페이스를 생성한다고 가정해 보자.

``` dart
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}
```

이 인터페이스의 문자열-특성 버전이 필요하다는 사실을 발견하고 또 다른 인터페이스를 생성하게 된다.

``` dart
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}
```

나중에 이 인터페이스의 숫자-특성 버전이 필요하다고 결정한 경우 또 ... 아이디어를 얻게된다.

제네릭 형식을 사용하면 이러한 모든 인터페이스를 만드는 수고를 덜 수 있다. 대신 유형 매개변수를 사용하는 단일 인터페이스를 작성할 수 있다.

``` dart
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

이 코드에서 `T`는 스탠드인(stand-in) 유형이다. 나중에 개발자가 정의할 유형으로 생각할 수 있는 placeholder (자리 표시자?) 이다.

---

- #### 유형 매개변수의 이름을 지정할 때 기존 니모닉 규칙을(mnemonic conventions) 따르자.

(별개의 페이지에 설명된 단일문자 매개변수 이름 지정 방법을 알아보았다.)

단일 문자 이름은 정확히 조명되지 않지만 거의 모든 일반 유형에서 사용합니다. 다행히도 그들은 대부분 일관되고 기억하기 쉬운 방식으로 사용합니다. 규칙은 다음과 같다.

- E : 컬렉션(List)에서 엘리먼트( __elememt__ ) 유형 ( the element type in a collection)

``` dart
class IterableBase<E> {}
class List<E> {}
class HashSet<E> {}
class RedBlackTree<E> {}
```

- K, V : 연관 컬렉션(map)의 키( __key__ ) 및 값( __value__ ) 유형:

``` dart
class Map<K, V> {}
class Multimap<K, V> {}
class MapEntry<K, V> {}
```

- R : 함수 또는 클래스의 메서드의 반환( __return__ ) 유형으로 사용되는 유형이다. 이것은 일상적이지는 않지만 가끔 typedefs와 방문자 패턴을 구현하는 클래스에 나타난다.

``` dart
abstract class ExpressionVisitor<R> {
  R visitBinary(BinaryExpression node);
  R visitLiteral(LiteralExpression node);
  R visitUnary(UnaryExpression node);
}
```

-  T, S, and U : 단일 유형 매개변수가 있고 주변 유형이 그 의미를 명확하게 만드는 제네릭에 사용한다. 여기에는 주변 이름을 가리지(shadowing) 않고 중첩할 수 있도록 여러 문자가 허용된다. 아래 예제를 참고하자.

``` dart
class Future<T> {
  Future<S> then<S>(FutureOr<S> onValue(T value)) => ...
}
```

여기서 일반 메서드 ``then<S>()`` 는 S를 사용하여 Future<T>에서 T를 가리지 않도록 한다.
위의 경우 중 어느 것도 적합하지 않은 경우 다른 단일 문자 니모닉 이름이나 설명이 포함된 이름을 사용한다. 

``` dart
class Graph<N, E> {
  final List<N> nodes = [];
  final List<E> edges = [];
}

class Graph<Node, Edge> { // 설명이 포함된 이름
  final List<Node> nodes = [];
  final List<Edge> edges = [];
}
```

실제로 이 규칙(conventions)은 대부분의 유형 매개변수를 포괄한다.

---

- #### Using collection literals

List, set 및 map 문자를 매개 변수화할 수 있습니다. 매개변수화된 문자(literals)은 여는 대괄호 앞에 <type>(List 및 set의 경우) 또는 <keyType, valueType>(map의 경우)을 추가한다는 점을 제외하면 이미 앞에서 본 문자(literals)과 같다. 다음은 형식화된 리터럴을 사용하는 예이다.

``` dart
var names = <String>['Seth', 'Kathy', 'Lars'];
var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
```

- ####  생성자와 함께 매개변수화된 유형를 사용하는 방법 (Using parameterized types with constructors)

생성자를 사용할 때 하나 이상의 유형(type)을 지정하려면 클래스 이름 바로 뒤에 유형을 꺾쇠 괄호(`<...>`)로 묶는다. 예를 들어:

``` dart
var nameSet = Set<String>.from(names);
```

다음 코드는 정수 키와 View 유형의 값이 있는 map 생성한다.

``` dart
var views = Map<int, View>();
```

- #### 제네릭 컬렉션과 그 컬렉션에 포함된 유형 (Generic collections and the types they contain)

Dart 제네릭 유형(generic types)은 구체화된다. 즉 런타임 시 유형 정보를 함 전달한다. 예제와 같이 컬렉션의 유형을 테스트 해보자.

``` dart
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true

```
(주: 대조적으로 Java의 제네릭은 삭제를 사용한다. 즉, 제네릭 유형 매개변수가 런타임 시 제거됨을 의미한다. Java에서는 개체가 List인지 여부를 테스트할 수 있지만 `List<String>`인지 여부는 테스트할 수 없다.)

- #### 매개변수화된 유형 제한 (Restricting the parameterized type)

제네릭 형식을 구현할 때 인수가 특정 형식의 하위 형식이 되도록 인수로 제공할 수 있는 형식을 제한할 수 있다. 이를 위해 extends를 사용할 수도 있다.

일반적인 사용 사례는 유형을 Object의 하위 유형(기본값인 Object? 대신)으로 만들어 non-nullable 인지 확인하는 것이다.

``` dart
class Foo<T extends Object> {
  // Any type provided to Foo for T must be non-nullable.
}
```

Object 외에 다른 유형과 함께 extends를 사용할 수 있다. 다음은 `SomeBaseClass`를 확장하여 `SomeBaseClass`의 멤버가 T 유형의 객체에서 호출될 수 있도록 하는 예이다.

``` dart
class Foo<T extends SomeBaseClass> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'";
}

class Extender extends SomeBaseClass {...}
```

`SomeBaseClass` 또는 그 하위 유형을 일반 인수로 사용하는 것도 허용된다. 

``` dart
var someBaseClassFoo = Foo<SomeBaseClass>();
var extenderFoo = Foo<Extender>();
```

제네릭 인수를 지정하지 않아도 좋다.

``` dart
var foo = Foo();
print(foo); // Instance of 'Foo<SomeBaseClass>'
```

하지만 SomeBaseClass가 아닌 유형을 지정하면 오류가 발생한다.

``` dart
// static analysis : error/warning
var foo = Foo<Object>();
```

- #### 제네릭 메서드 사용방법 (Using generic methods)

메서드와 함수는 type 인수도 허용한다.

``` dart
T first<T>(List<T> ts) {
  // Do some initial work or error checking, then...
  T tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}
```

여기서 `first( <T> )`로 사용된 제네릭 형식 매개 변수가 아래와 같이 여러 위치에서 형식 인수 T를 사용할 수 있도록 해 준다.

함수의 반환 유형(T)에서.
인수 유형(`List<T>`).
지역 변수의 유형(T tmp).

### 참고 자료

- https://dart.dev/guides/language/language-tour 