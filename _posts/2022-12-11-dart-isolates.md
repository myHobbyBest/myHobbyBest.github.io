---
title:  "Isolates "  
date:   2022-12-11 11:01:13 +0900
categories: [Flutter, Dart]
tag: [Isolates]
toc: true
---
### Isolates

요즘은 심지어 모바일 플랫폼에서도 대부분의 컴퓨터에는 CPU가 멀티 코어로 되어있다. 모든 코어를 활용하는 장점을 취하기 위해 개발자는 전통적으로 동시에 실행되는 공유 메모리 스레드를 사용한다. 그러나 공유 상태의 동시성은 오류가 발생하기 쉽고 복잡한 코드로 이어질 수 있다.

모든 Dart 코드는 스레드 대신 내부에서 독립적으로 분리 실행된다. 각 독립 Dart 에는 단일 실행 스레드가 있으며 다른 독립 스레드와 변경 가능한 객체를 공유하지 않는다.

자세한 내용은 아래 자료를 참조하자.

- Concurrency in Dart
- dart:isolate API reference, including Isolate.spawn() and TransferableTypedData
- Background parsing cookbook on the Flutter site
- Isolate sample app