---
title:  "Widgets"  
date:   2022-12-14 13:05:12 +0900
categories: [Flutter, Widget]
tag: [Widget]
toc: true
---
## 위젯 (Widgets)

Flutter의 위젯은 React에서 영감을 얻은 최신 프레임워크를 사용하여 구축되었다. 핵심 아이디어는 위젯에서 UI를 구축한다는 것이다. 위젯은 현재 구성 및 상태에 따라 외모가 어떻게 보여야 하는지 설명한다. 위젯의 상태가 변경되면 위젯은 한 상태에서 다음 상태로 전환하기위한 기본 렌더링 트리에서 필요한 최소한의 변경 사항을 결정하기 위해 프레임워크가 이전의 묘사와 비교하는 묘사를 다시 빌드한다.
(참고: 몇 가지 코드를 살펴봄으로써 Flutter에 대해 더 잘 알고 싶다면  basic layout codelab, building layouts, and adding interactivity to your Flutter app를 확인하기바란다.)

 ### Hello world

최소한의 Flutter 앱은 하나의 위젯을 가진 runApp() 함수를 호출하는 간단한 내용이 된다.


``` dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    Center(
      child: Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```

`runApp()` 함수는 주어진 `Widget`을 가져와 위젯 트리의 루트로 만든다. 이 예에서 위젯 트리는 `Center` 위젯과 그 하위인 `Text` 위젯의 두 위젯으로 구성된다. 프레임워크는 루트 위젯이 화면을 덮도록 강제한다. 즉, "Hello, world"라는 텍스트가 화면 중앙에 표시된다. 이 경우 텍스트 방향을 지정해야 하는데 ,  에기에 관해서는 뒤에서  `MaterialApp` 위젯이 사용되었들 떄 설명할 것이다.

앱을 작성할 때 일반적으로 위젯이 상태를 관리하는지 여부에 따라 `StatelessWidget` 또는 `StatefulWidget`의 하위 클래스인 새 위젯을 작성한다. 위젯의 주요 작업은 다른 하위 수준 위젯의 관점에서 위젯을 설명하는 `build()` 함수를 구현하는 것이다. 프레임워크는 바탕에 있는 `RenderObject`를 (위젯의 지오메트리를 계산하고 기술한다)표현하는 위젯 내부에서 프로세스가 끝날 때까지 해당 위젯을 차례로 빌드한다.

### 기본 위젯 (Basic widgets)

Flutter에는 다음과 같은 강력한 기본 위젯이 함께 제공된다.

__Text__

`Text` 위젯을 사용하면 애플리케이션 내에서 스타일이 지정된 텍스트 실행을 만들 수 있다.

__Row 와 Column__
이러한 플렉스 위젯을 사용하면 가로(행) 및 세로(열) 방향 모두에서 유연한 레이아웃을 만들 수 있다. 이러한 개체의 디자인은 웹의 flexbox 레이아웃 모델을 기반으로 한다.
__Stack__
선형 방향(수평 또는 수직)이 아닌 `Stack` 위젯을 사용하면 페인트 순서에 따라 위젯을 서로 위에 배치할 수 있다. 그런 다음 `Stack`의 자식에 있는 위치 지정 위젯을 사용하여 스택의 위쪽, 오른쪽, 아래쪽 또는 왼쪽 가장자리를 기준으로 위치를 지정할 수 있다. `Stack`은 웹의 절대 위치 지정 레이아웃 모델을 기반으로 한다.

__Container__

`Container` 위젯을 사용하면 직사각형 시각적 요소를 만들 수 있다. `Container`는 배경, 테두리 또는 그림자와 같은 BoxDecoration으로 꾸밀 수 있다. `Container`에는 크기에 적용되는 여백, 패딩 및 제약 조건이 있을 수도 있다. 또한 `Container`는 행렬을 사용하여 3차원 공간에서 변형될 수 있다.

다음은 이러한 위젯과 다른 위젯을 결합한 몇 가지 간단한 위젯이다.

``` dart
import 'package:flutter/material.dart';

class MyAppBar extends StatelessWidget {
  MyAppBar({this.title});

  // Fields in a Widget subclass are always marked "final".

  final Widget title;

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 56.0, // in logical pixels
      padding: const EdgeInsets.symmetric(horizontal: 8.0),
      decoration: BoxDecoration(color: Colors.blue[500]),
      // Row is a horizontal, linear layout.
      child: Row(
        // <Widget> is the type of items in the list.
        children: <Widget>[
          IconButton(
            icon: Icon(Icons.menu),
            tooltip: 'Navigation menu',
            onPressed: null, // null disables the button
          ),
          // Expanded expands its child to fill the available space.
          Expanded(
            child: title,
          ),
          IconButton(
            icon: Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
    );
  }
}

class MyScaffold extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Material is a conceptual piece of paper on which the UI appears.
    return Material(
      // Column is a vertical, linear layout.
      child: Column(
        children: <Widget>[
          MyAppBar(
            title: Text(
              'Example title',
              style: Theme.of(context).primaryTextTheme.title,
            ),
          ),
          Expanded(
            child: Center(
              child: Text('Hello, world!'),
            ),
          ),
        ],
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    title: 'My app', // used by the OS task switcher
    home: MyScaffold(),
  ));
}
```
