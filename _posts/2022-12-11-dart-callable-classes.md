---
title:  "Callable classes "  
date:   2022-12-11 11:09:13 +0900
categories: [Flutter, Dart]
tag: [Callable classes]
toc: true
---
### Callable classes

Dart 클래스의 인스턴스가 함수처럼 호출되도록 하려면 ``call()`` 메서드를 구현한다.

``call()`` 메서드를 사용하면 이를 정의하는 모든 클래스가 함수를 에뮬레이트할 수 있다. 이 메서드는 매개 변수 및 반환 유형과 같은 일반 함수와 동일한 기능을 지원한다.

다음 예제에서 WannabeFunction 클래스는 3개의 문자열을 가져와 연결하고 각 문자열을 공백으로 구분하고 느낌표를 추가하는 ``call()``함수를 정의한다. 
``` dart
class WannabeFunction {
  String call(String a, String b, String c) => '$a $b $c!';
}

var wf = WannabeFunction();
var out = wf('Hi', 'there,', 'gang');

void main() => print(out);
```

- 실행 결과

``` console
Hi there, gang!
```

