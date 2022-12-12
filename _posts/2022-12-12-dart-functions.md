---
title:  "Functions"  
date:   2022-12-12 18:40:22 +0900
categories: [Flutter, Dart]
tag: [Functions]
toc: true
---
### 함수 (Functions)

Dart는 진정한 객체 지향 언어이므로 함수도 객체이며 유형이 Function이다. 이는 함수를 변수에 할당하거나 다른 함수에 인수로 전달할 수 있음을 의미한다. 마치 함수인 것처럼 Dart 클래스의 인스턴스를 호출할 수도 있다. 자세한 내용은 호출 가능 클래스를 참조한다.

다음은 함수 구현의 예이다.

``` dart
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

Effective Dart는 공개 API에 대한 유형 주석을 권장하지만 유형을 생략해도 함수는 계속 작동한다.

``` dart
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```
하나의 표현식만 포함하는 함수의 경우 단축 구문을 사용할 수 있다.

``` dart
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```
`=> expr` 구문은 { return expr; } 구문의 단축표현이다.  `=>` 표현은 화살표 구문이라고도 합다.

(참고: 화살표(`=>`)와 세미콜론(`;`) 사이에는 명령문이 아닌 표현식만 나타날 수 있다. 예를 들어 if 문은 넣을 수 없지만 조건식은 사용할 수 있다.)

- #### 매개변수 (Parameters)

함수는 필수 위치 매개변수를 얼마든지 가질 수 있습니다. 그 뒤에는 이름있는 매개변수 또는 선택적 위치 매개변수가 올 수 있다(둘 다는 아님).

 ( 참고: 일부 API(특히 Flutter 위젯 생성자)는 필수 매개변수의 경우에도 이름있는 매개변수만 사용합니다. 자세한 내용은 다음 섹션을 참조한다.)

함수에 인수를 전달하거나 함수 매개 변수를 정의할 때 후행 쉼표를 사용할 수 있다.

- 이름있는 매개변수
이름있는 매개변수는 명시적으로 `required`로 표시되지 않는 한 선택 사항이다.

함수를 정의할 때 {param1, param2, …}를 사용하여 이름있는 매개변수를 지정한다. 기본값을 제공하지 않거나 이름있는 매개변수를 `required`로 표시하지 않으면 해당 유형은 기본값이 null이 되므로 null을 허용해야 한다.

``` dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool? bold, bool? hidden}) {...}
```
함수를 호출할 때 paramName: value를 사용하여 이름있는 인수를 지정할 수 있다. 예를 들어:

``` dart
enableFlags(bold: true, hidden: false);
```
null 이외의 이름있는 매개 변수에 대한 기본값을 정의하려면 `=`를 사용하여 기본값을 지정한다. 지정된 값은 컴파일 타임 상수여야 합다. 예를 들어:

``` dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {...}

// bold will be true; hidden will be false.
enableFlags(bold: true);
```
