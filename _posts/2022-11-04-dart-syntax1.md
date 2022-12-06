---
title:  "Dart문법(1) - type, null-safty, loop"  
date:   2022-11-04 23:00:09 +0900
categories: [Flutter, Dart syntax ]
tag: [type, null safty, loop ]
toc: true
---


## Dart문법 (1) 


### 변수 type

``` dart
int num1 = 10;
double num2 = 3.0;
String str = 'hello';
bool isTrue = true;
num num3 = 10;
num num4 = 10.0

print(num1 is int); // true
print(mun2 is int); // false

print(num1.runtimeType); //int
```
var 은 compile time에 type 이 결정되지만
dynamic 은 runtime에 type 이 결정된다

#### 변수 type의 확장
프로그래밍 언어에서 전통적인 의미의 __변수 type__ 이란 문자인지 숫자인지 정수인지 실수인지 논리값인지 array ( List, Map 등을 포함? ) 인지 정도를 구분하기 위한 것이 었다면 요즘의 프로그래밍 언어에서는 __변수 type__ 은 그 의미가 많이 확장되었다. color, class(뒤에서 다시 설명할 기회가 있다. ) 등도 변수 type 으로 선언할 수 있다.



### null safty

``` dart
int? age ; //nullable
print(age == null); // true

String? name;
String result = name; //error null이 포함됬는지 여부가 중요하다.

if (name !=null) { 
    String result = name; // no error null을 제거했으므로 가능하다.
}

```
### Null-aware operators (널인식 연산자)
``` dart
int? a; // = null
a ??= 3;
print(a); // <-- Prints 3.(null이면 3을 넣는다)

a ??= 5;
print(a); // <-- Prints 3.(null이 아니라서 5를 넣지 않는다.)

int? a; // = null;
print(1 ?? 3); // <-- Prints 1.  null 이 아니라서 1출력
print(a ?? 12); // <-- Prints 12. null 이라서 12출력

String? str;
str ??='Hello';    //  --1)
str = str ?? 'Hello';    //  2) 1)과2)는 같다.

```
### 반복문 (loop)

``` dart
for (var i=0; i < 5; i++){
    // break;
    // continu;
}

int i = 0;
while (i < 3) {
    //
    i++    
    // break;
    // continu;
}
```

