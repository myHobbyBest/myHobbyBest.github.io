---
title:  "Dart문법(4) - Map"  
date:   2022-11-07 00:01:30 +0900
categories: [Dart syntax, Flutter]
tag: [map, Map.from() , Map.of()   ]
toc: true 
---

### Map

#### Map 을 초기화하는 방법들

-   괄호  (curly braces, {} )를 이용해 간단하게 초기화

- from(), of() constructor를 이용해 다른 Map 으로부터 모든l key/value 쌍을 생성er Map using from(), of() constructor.
- fromIterables() 을 이용해 주어진 key/value 값으로부터 새로운 Map을 생성.
- fromIterables() 을 이용해 key/value 값을 계산하여 새로운 Map을 생성.
- unmodifiable() 을 이용해 상수의 Map을 생성.

``` dart

Map<String, int> map1 = {'zero': 0, 'one': 1, 'two': 2};
print(map1);  // {zero: 0, one: 1, two: 2}

// not specify key-value type
Map map2 = {'zero': 0, 'I': 'one', 10: 'X'};
print(map2); //{zero: 0, I: one, 10: X}

var map3 = {'zero': 0, 'I': 'one', 10: 'X'};
print(map3); //{zero: 0, I: one, 10: X}

Map<String, int> map1 = {'zero': 0, 'one': 1, 'two': 2};

Map map2 = Map.from(map1);
print(map2); //{zero: 0, one: 1, two: 2}

Map map3 = Map.of(map1);
print(map3); //{zero: 0, one: 1, two: 2}

// fromIterable() 재미있는 방법
List<String> letters = ['I', 'V', 'X'];
List<int> numbers = [1, 5, 10];

Map<String, int> map = Map.fromIterables(letters, numbers);
print(map); //{I: 1, V: 5, X: 10}


List<int> numbers = [1, 2, 3];

Map<String, int> map = Map.fromIterable(
  numbers,
  key: (k) => 'double ' + k.toString(),
  value: (v) => v * 2);

print(map); //{double 1: 2, double 2: 4, double 3: 6}

// unmodifiable
Map map = Map.unmodifiable({1: 'one', 2: 'two'});
print(map); // {1: one, 2: two}

map[3] = 'three'; // Unhandled exception: Unsupported operation: Cannot modify unmodifiable map

```

#### Map.from() 와 Map.of() 의 차이점

``` dart
Map<int, String> map = {1: 'one', 2: 'two'};

Map<String, String> map1 = Map.from(map); // runtime error
Map<String, String> map2 = Map.of(map);   // compilation error

```

Map.of(map)은 컴파일 시에 에러감지 가능하지만 Map.from()은 prototype 이 <dynamic, dynamic> 이라서 컴파일 시에 에러를 감지하지 못함

#### 내부 조건문 if, 내부 반복문 for

 List처럼 동일하게 적용가능

 ``` dart
var mobile = true;
var myMap = {1: 'kotlin', 2: 'dart', if (mobile) 3: 'flutter'};
// {1: kotlin, 2: dart, 3: flutter}

var squareMap = {
  for (var i = 1; i <= 5; i++) i: i * i
};  // {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

var tringList = ['kotlin', 'dart', 'flutter', 'react'];
var i = 0;
var data = {for (var s in tringList) if (s.length > 5) i++: s};
// {0: kotlin, 1: flutter}
```
#### Add item to a Map

``` dart 
Map map = {1: 'one', 2: 'two'};

map[3] = 'three';
print(map); //{1: one, 2: two, 3: three}

var threeValue = map.putIfAbsent(3, () => 'THREE');
print(map); //{1: one, 2: two, 3: three}
print(threeValue); // the value associated to key, if there is one
   //three 
map.putIfAbsent(4, () => 'four');
print(map); //{1: one, 2: two, 3: three, 4: four}
 
// addAll  method
 Map map = {1: 'one', 2: 'two'};
map.addAll({3: 'three', 4: 'four', 5: 'five'});
print(map); // {1: one, 2: two, 3: three, 4: four, 5: five}
```

#### Map update value by key

``` dart
Map map = {1: 'one', 2: 'two'};

map[1] = 'ONE';
print(map);  //{1: ONE, 2: two}

map.update(2, (v) {
  print('old value before update: ' + v); //old value before update: two
  return 'TWO';
});
print(map); //{1: ONE, 2: TWO}

map.update(3, (v) => 'THREE', ifAbsent: () => 'addedThree');
print(map); //{1: ONE, 2: TWO, 3: addedThree} !!! 이해되지 않음
```

#### Access items from Map 

``` dart
Map map = {1: 'one', 2: 'two'};

print(map.length);      // 2

print(map.isEmpty);     // false
print(map.isNotEmpty);  // true

print(map.keys);        // (1, 2)
print(map.values);      // (one, two)

print(map[2]);          // two
print(map[3]);          // null
```

#### check existence of key/value in Map

``` dart
Map map = {1: 'one', 2: 'two'};

print(map.containsKey(1));       // true
print(map.containsKey(3));       // false

print(map.containsValue('two')); // true
print(map.containsValue('three')); // false
```

#### Remove objects from Map

``` dart
Map map = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'};

map.remove(2);
print(map); //{1: one, 3: three, 4: four, 5: five}

map.removeWhere((k, v) => v.startsWith('f'));
print(map); //{1: one, 3: three}

map.clear();
print(map); //{}

```

#### Iterate over Map

``` dart
Map map = {1: 'one', 2: 'two', 3: 'three'};

map.forEach((k, v) {
  print('{ key: $k, value: $v }'); 
});

map.entries.forEach((e) { 
  print('{ key: ${e.key}, value: ${e.value} }'); 
});

// { key: 1, value: one }
// { key: 2, value: two }
// { key: 3, value: three }

map.keys.forEach((k) => print(k));
map.values.forEach((v) => print(v));

// 1
// 2
// 3
// one
// two
// three
```

####  get key by value

``` dart
Map map = {1: 'one', 2: 'two', 3: 'three'};

var key = map.keys.firstWhere((k) => map[k] == 'two', orElse: () => null);
print(key);
// 2
```
#### Sort a Map 

``` dart
Map map = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'};

var sortedMap = Map.fromEntries(
    map.entries.toList()
    ..sort((e1, e2) => e1.value.compareTo(e2.value)));
print(map.entries); // (MapEntry(1: one), MapEntry(2: two), MapEntry(3: three), MapEntry(4: four), MapEntry(5: five))
print(sortedMap); //{5: five, 4: four, 1: one, 3: three, 2: two} ascending

```

#### Map.map() method to transform a Map 

``` dart
Map map = {1: 'one', 2: 'two', 3: 'three'};

var transformedMap = map.map((k, v) {
  return MapEntry('($k)', v.toUpperCase());
});

print(transformedMap); //{(1): ONE, (2): TWO, (3): THREE}
```