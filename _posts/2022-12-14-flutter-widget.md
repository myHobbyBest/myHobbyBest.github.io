---
title:  "Introduction to widgets"  
date:   2022-12-14 13:05:12 +0900
categories: [Flutter, Widget]
tag: [Widget]
toc: true
---
## 위젯 소개 (Introduction to widgets)

---

위젯은 UI의  구성부분 중 형식화 하거나 정형화 할 수 있는 부분들을  class로 정의하여 필요한 곳에 필요할 때 언제든지 객체로 불러내서 사용하고자 하는 플러터의 가장 중요한 프레임워크 기능 중 하나이다.
아래 내용은 flutter.dev 에 기재된 __Introduction to widgets__ 내용을 번역한 것이다.

---
Flutter의 위젯은 React에서 영감을 얻은 최신 프레임워크를 사용하여 구축되었다. 핵심 아이디어는 위젯에서 UI를 구축한다는 것이다. 위젯은 현재 구성 및 상태에 따라 외모가 어떻게 보여야 하는지 설명한다. 위젯의 상태가 변경되면 위젯은 한 상태에서 다음 상태로 전환하기 위한 기본 렌더링 트리에서 필요한 최소한의 변경 사항을 결정하기 위해 프레임워크가 이전의 묘사와 비교하는 묘사를 다시 빌드한다.
(참고: 몇 가지 코드를 살펴 봄으로써 Flutter에 대해 더 잘 알고 싶다면  basic layout codelab, building layouts, and adding interactivity to your Flutter app를 확인하기 바란다.)

### Hello world

최소한의 Flutter 앱은 하나의 위젯을 가진 runApp() 함수를 호출하는 간단한 내용이다.

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

`runApp()` 함수는 주어진 `Widget`을 가져와 위젯 트리의 루트로 만든다. 이 예에서 위젯 트리는 `Center` 위젯과 그 하위인 `Text` 위젯의 두 위젯으로 구성된다. 프레임워크는 루트 위젯이 화면을 덮도록 강제한다. 즉, "Hello, world"라는 텍스트가 화면 중앙에 표시된다. 이 경우 텍스트 방향을 지정해야 하는데 ,  여기에 관해서는 뒤에서  `MaterialApp` 위젯이 사용되었을 떄 설명할 것이다.

앱을 작성할 때 일반적으로 위젯이 상태를 관리하는지 여부에 따라 `StatelessWidget` 또는 `StatefulWidget`의 하위 클래스인 새 위젯을 작성한다. 위젯의 주요 작업은 다른 하위 수준 위젯의 관점에서 위젯을 설명하는 `build()` 함수를 구현하는 것이다. 프레임워크는 바탕에 있는 `RenderObject`를 (위젯의 지오메트리를 계산하고 기술한다)표현하는 위젯 내부에서 프로세스가 끝날 때까지 해당 위젯을 차례로 빌드한다.

### 기본 위젯 (Basic widgets)

Flutter에는 다음과 같은 강력한 기본 위젯이 함께 제공된다.

__Text__
`Text` 위젯을 사용하면 애플리케이션 내에서 스타일이 지정된 텍스트 실행을 만들 수 있다.

__Row 와 Column__
이러한 플렉스 위젯을 사용하면 가로(행), 세로(열) 방향 모두에서 유연한 레이아웃을 만들 수 있다. 이러한 개체의 디자인은 웹의 flexbox 레이아웃 모델을 기반으로 한다.

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

pubspec.yaml 파일의 flutter 섹션에 `uses-material-design: true` 항목이 있는지 확인한다. `Material icons` 사전 정의된  세트를 사용할 수 있다.

``` dart
name: my_app
flutter:
  uses-material-design: true
```

머티리얼 디자인 위젯이 테마 데이터를 상속해서 제대로 표시되도록 하려면  `MaterialApp` 내부에 있어야 한다. 따라서 `MaterialApp`으로 애플리케이션을 실행한다.

`MyAppBar` 위젯은 좌우 양쪽 모두에 8픽셀의 내부 패딩이 있는 56개의 device-independent(장치독립적) 픽셀 높이를 가진  `Container`를 만든다. `Container` 내에서 `MyAppBar`는 행(Row) 레이아웃을 사용하여 자식(하위 위젯)을 구성한다. middle childe인 `title`위젯은 `Expanded`로 표시된다. 이는 다른 자식이 사용하지 않은 나머지 사용 가능한 공간을 확장(`Expanded`)하여 채운다는 의미이다. 확장된 자식을 여러 개 가질 수 있으며 `Expanded`에 대한 `flex` 인수를 사용하여 사용 가능한 공간을 소비하는 비율을 결정할 수 있다.

`MyScaffold` 위젯은 수직 `column`에 하위 항목을 구성한다. `column`의 맨 위에 `MyAppBar`의 인스턴스를 배치하고 제목으로 사용할 `Text` 위젯을 `MyAppBar`에 전달한다. 위젯을 다른 위젯에 인수로 전달하는 것은 다양한 방법으로 재사용할 수 있는 제네릭 위젯을 만들 수 있는 강력한 기술이다. 마지막으로 `MyScaffold`는 `Expanded`를 사용하여 중앙 메시지로 구성된 본문으로 나머지 공간을 채웁니다.

자세한 내용은 `Layouts`을 참조한다.

### Using Material Components

Flutter는 머티리얼 디자인을 따르는 앱을 빌드하는 데 도움이 되는 다양한 위젯을 제공한다. Material 앱은 `MaterialApp` 위젯으로 시작한다. 이 위젯은 `“routes”`라고도 하는 문자열로 식별되는 위젯 스택을 관리하는 `Navigator`를 포함하여 앱의 루트에 여러 유용한 위젯을 빌드한다.  `Navigator`를 사용하면 응용 프로그램 화면 간을 원활하게 전환할 수 있다. `MaterialApp` 위젯을 사용하는 것은 전적으로 선택 사항이지만 좋은 습관이 된다.

``` dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    title: 'Flutter Tutorial',
    home: TutorialHome(),
  ));
}

class TutorialHome extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Scaffold is a layout for the major Material Components.
    return Scaffold(
      appBar: AppBar(
        leading: IconButton(
          icon: Icon(Icons.menu),
          tooltip: 'Navigation menu',
          onPressed: null,
        ),
        title: Text('Example title'),
        actions: <Widget>[
          IconButton(
            icon: Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
      // body is the majority of the screen.
      body: Center(
        child: Text('Hello, world!'),
      ),
      floatingActionButton: FloatingActionButton(
        tooltip: 'Add', // used by assistive technologies
        child: Icon(Icons.add),
        onPressed: null,
      ),
    );
  }
}
```

이제 코드가 `MyAppBar` 및 `MyScaffold`에서 `AppBar` 및 `Scaffold` 위젯으로, 그리고 `material.dart`에서 전환되었으므로 앱이 조금 더 많은 `Material`을 살펴보기 시작한다. 예를 들어 `AppBar` 에는 그림자가 있고 제목 텍스트는 올바른 스타일을 자동으로 상속한다. `floatingActionButton` 도 추가된다.

위젯은 다른 위젯에 인수로 전달됩니다. `Scaffold` 위젯은 이름있는 인수로 다양한 위젯을 사용하며 각 위젯은 `Scaffold` 레이아웃의 적절한 위치에 배치됩니다. 마찬가지로 `AppBar` 위젯을 사용하면 선행 위젯에 대한 위젯과 제목 위젯의 작업을 전달할 수 있습니다. 이 패턴은 프레임워크 전체에서 반복되며 자체 위젯을 디자인할 때 고려할 수 있는 패턴입니다.

자세한 내용은 `Material Components` 위젯을 참조하자.

(참고: `Material`은 Flutter에 포함된 2개의 번들 디자인 중 하나이다. iOS 중심 디자인을 만들려면 자체 버전의 `CupertinoApp` 및 `CupertinoNavigationBar`가 있는 `Cupertino `구성 요소 패키지를 참조한다.)

### 제스처의 처리 (Handling gestures)

대부분의 애플리케이션에는 시스템과의 사용자 상호 작용 형식이 포함된다. 대화형 애플리케이션 구축의 첫 번째 단계는 입력 제스처를 감지하는 것이다. 간단한 버튼을 만들어 어떻게 작동하는지 확인하자.

``` dart
class MyButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        print('MyButton was tapped!');
      },
      child: Container(
        height: 36.0,
        padding: const EdgeInsets.all(8.0),
        margin: const EdgeInsets.symmetric(horizontal: 8.0),
        decoration: BoxDecoration(
          borderRadius: BorderRadius.circular(5.0),
          color: Colors.lightGreen[500],
        ),
        child: Center(
          child: Text('Engage'),
        ),
      ),
    );
  }
}
```
`GestureDetector` 위젯에는 시각적 표현이 없지만 대신 사용자의 제스처를 감지한다. 사용자가 `Container`를 탭하면 `GestureDetector`가 `onTap()` 콜백을 호출하고 이 경우 console에 메시지를 출력한다. `GestureDetector`를 사용하여 탭(taps), 끌기(drags), 배율 조정(scales)을 비롯한 다양한 입력 제스처를 감지할 수 있다.

많은 위젯이  `GestureDetector`를 사용하여 다른 위젯에 대한 선택적 콜백을 제공,한다. 예를 들어 `IconButton`, `RaisedButton` 및 `FloatingActionButton` 위젯에는 사용자가 위젯을 누를 때 트리거되는 `onPressed()` 콜백이 있다.

자세한 내용은 `Flutter`의 `Gestures` 섹션을 참조하자.

### 입력에 대한 응답으로 위젯 변경 (Changing widgets in response to input)

지금까지 이 페이지에서는 stateless 위젯만 사용했다. stateless 위젯은 상위 위젯에서 인수를 받아 최종 멤버 변수에 저장한다. 위젯이 build()를 요청하면 이 저장된 값을 사용하여 새로 생성하는 위젯에 대한 새 인수를 파생한다.

보다 복잡한 경험을 구축하기 위해(예: 사용자 입력에 보다 흥미로운 방식으로 반응하기 위해) 애플리케이션은 일반적으로 어떤 상태를 전달합니다. Flutter는 이 아이디어를 포착하기위해  `StatefulWidgets` 를 사용한다. `StatefulWidgets`는 상태를 유지하는 데 사용되는 State 개체를 생성하는 방법을 알고 있는 특수 위젯이다. 앞에서 언급된 `RaisedButton`을 사용하는 아래 기본 예제를 고려해보자.

``` dart
class Counter extends StatefulWidget {
  // This class is the configuration for the state. It holds the
  // values (in this case nothing) provided by the parent and used by the build
  // method of the State. Fields in a Widget subclass are always marked "final".

  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      // This call to setState tells the Flutter framework that
      // something has changed in this State, which causes it to rerun
      // the build method below so that the display can reflect the
      // updated values. If you change _counter without calling
      // setState(), then the build method won't be called again,
      // and so nothing would appear to happen.
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called,
    // for instance, as done by the _increment method above.
    // The Flutter framework has been optimized to make rerunning
    // build methods fast, so that you can just rebuild anything that
    // needs updating rather than having to individually change
    // instances of widgets.
    return Row(
      children: <Widget>[
        RaisedButton(
          onPressed: _increment,
          child: Text('Increment'),
        ),
        Text('Count: $_counter'),
      ],
    );
  }
}
```

StatefulWidget과 State가 왜 별개의 개체인지 궁금할 수 있다. Flutter에서 이 두 유형의 객체는 수명 주기가 다르다. 위젯은 현재 상태에서 응용 프로그램의 프레젠테이션을 구성하는 데 사용되는 임시 개체이다. 반면에 상태 개체는 build() 호출 간에 지속되므로 정보를 기억할 수 있다.

위의 예제는 사용자 입력을 수락하고 build() 메서드에서 결과를 직접 사용한다. 더 복잡한 애플리케이션에서는 위젯 계층 구조의 다른 부분이 다른 문제를 담당할 수 있다. 예를 들어, 한 위젯은 날짜나 위치와 같은 특정 정보를 수집할 목적으로 복잡한 사용자 인터페이스를 제공하고 다른 위젯은 해당 정보를 사용하여 전체 표시를 변경할 수 있다.

Flutter에서 변경 알림(change notifications)은 콜백을 통해 위젯 계층 구조에서 "위로" 흐르는 반면 현재 상태는 프레젠테이션을 수행하는 stateless 위젯으로 "아래로" 흐른다. 이 흐름을 리디렉션하는 공통 부모는 상태이다. 다음의 약간 더 복잡한 예는 이것이 실제로 어떻게 작동하는지 보여준다.

``` dart
class CounterDisplay extends StatelessWidget {
  CounterDisplay({this.count});

  final int count;

  @override
  Widget build(BuildContext context) {
    return Text('Count: $count');
  }
}

class CounterIncrementor extends StatelessWidget {
  CounterIncrementor({this.onPressed});

  final VoidCallback onPressed;

  @override
  Widget build(BuildContext context) {
    return RaisedButton(
      onPressed: onPressed,
      child: Text('Increment'),
    );
  }
}

class Counter extends StatefulWidget {
  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      ++_counter;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Row(children: <Widget>[
      CounterIncrementor(onPressed: _increment),
      CounterDisplay(count: _counter),
    ]);
  }
}
```

카운터를 표시하는 문제(CounterDisplay)와 카운터를 변경하는 문제(CounterIncrementor)를 깔끔하게 분리하는 두 개의 새로운 stateless 위젯 생성에 주목해보자. 최종 결과는 이전 예와 동일하지만 응답성을 분리하면 부모(상위 위젯)에서는 단순성을 유지하면서도 개별 위젯에서는 더 복잡한 것도 캡슐화할 수 있다.

자세한 내용은 다음을 참조하자.

- __StatefulWidget__
- __setState()__

### 모든 것을 하나로 모으기 (Bringing it all together)

다음은 이러한 개념을 결합한 보다 완전한 예이다. 가상의 쇼핑 응용 프로그램은 판매용으로 제공되는 다양한 제품을 표시하고 원하는 구매를 위한 장바구니를 갖추고 있다. 프레젠테이션 클래스인 ShoppingListItem을 정의하여 시작한다.

``` dart
class Product {
  const Product({this.name});
  final String name;
}

typedef void CartChangedCallback(Product product, bool inCart);

class ShoppingListItem extends StatelessWidget {
  ShoppingListItem({Product product, this.inCart, this.onCartChanged})
      : product = product,
        super(key: ObjectKey(product));

  final Product product;
  final bool inCart;
  final CartChangedCallback onCartChanged;

  Color _getColor(BuildContext context) {
    // The theme depends on the BuildContext because different parts of the tree
    // can have different themes.  The BuildContext indicates where the build is
    // taking place and therefore which theme to use.

    return inCart ? Colors.black54 : Theme.of(context).primaryColor;
  }

  TextStyle _getTextStyle(BuildContext context) {
    if (!inCart) return null;

    return TextStyle(
      color: Colors.black54,
      decoration: TextDecoration.lineThrough,
    );
  }

  @override
  Widget build(BuildContext context) {
    return ListTile(
      onTap: () {
        onCartChanged(product, inCart);
      },
      leading: CircleAvatar(
        backgroundColor: _getColor(context),
        child: Text(product.name[0]),
      ),
      title: Text(product.name, style: _getTextStyle(context)),
    );
  }
}
```

`ShoppingListItem` 위젯은 상태 비저장(stateless) 위젯의 일반적인 패턴을 따른다. 생성자에서 받은 값을 최종 멤버 변수에 저장한 다음 build() 함수 중에 사용한다. 예를 들어 `inCart` 부울은 현재 테마의 기본 색상을 사용하는 것과 회색을 사용하는 것의 두 가지 시각적 모양 사이를 전환한다.

사용자가 list 항목을 탭하면 위젯이 inCart 값을 직접 수정하지 않는다. 대신 위젯은 상위 위젯에서 받은 `onCartChanged` 함수를 호출한다. 이 패턴을 사용하면 위젯 계층 구조에서 더 높은 상태를 저장할 수 있으므로 상태가 더 오랜 시간 동안 지속된다. 극단적으로 `runApp()`에 전달된 위젯에 저장된 상태는 애플리케이션의 수명 동안 지속된다.

부모가 `onCartChanged` 콜백을 수신하면 부모는 내부 상태를 업데이트하여 부모가 새 `inCart` 값으로 `ShoppingListItem`의 새 인스턴스를 다시 작성하고 생성하도록 트리거한다. 부모가 다시 빌드할 때 `ShoppingListItem`의 새 인스턴스를 생성하지만 프레임워크가 새로 빌드된 위젯을 이전에 빌드된 위젯과 비교하고 차이점만 기본 `RenderObject`에 적용하기 때문에 해당 작업이 저렴하다.

다음은 변경 가능한 상태를 저장하는 부모 위젯의 예이다.
``` dart
  class ShoppingList extends StatefulWidget {
  ShoppingList({Key key, this.products}) : super(key: key);

  final List<Product> products;

  // The framework calls createState the first time a widget appears at a given
  // location in the tree. If the parent rebuilds and uses the same type of
  // widget (with the same key), the framework re-uses the State object
  // instead of creating a new State object.

  @override
  _ShoppingListState createState() => _ShoppingListState();
}

class _ShoppingListState extends State<ShoppingList> {
  Set<Product> _shoppingCart = Set<Product>();

  void _handleCartChanged(Product product, bool inCart) {
    setState(() {
      // When a user changes what's in the cart, you need to change
      // _shoppingCart inside a setState call to trigger a rebuild.
      // The framework then calls build, below,
      // which updates the visual appearance of the app.

      if (!inCart)
        _shoppingCart.add(product);
      else
        _shoppingCart.remove(product);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Shopping List'),
      ),
      body: ListView(
        padding: EdgeInsets.symmetric(vertical: 8.0),
        children: widget.products.map((Product product) {
          return ShoppingListItem(
            product: product,
            inCart: _shoppingCart.contains(product),
            onCartChanged: _handleCartChanged,
          );
        }).toList(),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    title: 'Shopping App',
    home: ShoppingList(
      products: <Product>[
        Product(name: 'Eggs'),
        Product(name: 'Flour'),
        Product(name: 'Chocolate chips'),
      ],
    ),
  ));
}
```
`ShoppingList` 클래스는 `StatefulWidget`을 확장한다. 즉, 이 위젯은 변경 가능한 상태를 저장한다. `ShoppingList` 위젯이 트리에 처음 삽입되면 프레임워크는 `createState()` 함수를 호출하여 트리의 해당 위치와 연결할 _`ShoppingListState`의 새 인스턴스를 만든다.

(`State`의 하위 클래스는 일반적으로 private 구현 세부 정보임을 나타내기 위해 이름앞에 underscores가 사용된다.) 이 위젯의 부모가 다시 빌드되면 부모는 `ShoppingList`의 새 인스턴스를 생성하지만 프레임워크는 `createState`를 다시 호출하는 기 보다는 이미 트리에 있는 `_ShoppingListState` 인스턴스를 재사용한다.

현재 `ShoppingList`의 속성에 액세스하기 위해 _`ShoppingListState`는 위젯 속성을 사용할 수 있다. 부모가 새 `ShoppingList`를 다시 작성하고 만들면 `_ShoppingListState`가 새 위젯 값으로 다시 작성된다. 위젯 속성이 변경될 때 알림을 받으려면 이전 위젯을 현재 위젯과 비교할 수 있도록 `oldWidget`으로 전달되는 `didUpdateWidget()` 함수를 재정의하라.

`onCartChanged` 콜백을 처리할 때 `_ShoppingListState`는 `_shoppingCart`에서 제품을 추가하거나 제거하여 내부 상태를 변경한다. 내부 상태가 변경되었음을 프레임워크에 알리기 위해 해당 호출을 `setState()` 호출로 래핑한다. `setState`를 호출하면 이 위젯이 더티( dirty)로 표시되고 다음에 앱에서 화면을 업데이트해야 할 때 다시 빌드되도록 예된다. 위젯의 내부 상태를 수정할 때 `setState`를 호출하는 것을 잊은 경우 프레임워크는 위젯이 더티( dirty)라는 것을 알지 못하고 위젯의 `build()` 함수를 호출하지 않을 수 있다. 즉, 사용자 인터페이스가 변경된 상태를 반영하도록 업데이트되지 않을 수 있다.
이러한 방식으로 상태를 관리하면 자식 위젯을 만들고 업데이트하기 위한 별도의 코드를 작성할 필요가 없다. 대신 두 상황을 모두 처리하는 빌드 기능을 구현하기만 하면 된다.


### 위젯 수명 주기 이벤트에 반응하기 (Responding to widget lifecycle events)

`StatefulWidget`에서 `createState()`를 호출한 후 프레임워크는 새 상태 개체를 트리에 삽입한 다음 상태 개체에서 `initState()`를 호출한다. `State`의 하위 클래스는 한 번만 발생해야 하는 작업을 수행하도록 `initState`를 재정의할 수 있다. 예를 들어 애니메이션을 구성하거나 플랫폼 서비스를 구독하려면 `initState`를 재정의한다. `initState`의 구현은 `super.initState`를 호출하여 시작해야 한다.

상태 개체가 더 이상 필요하지 않으면 프레임워크는 상태 개체에서 `dispose(`)를 호출한다. 정리 작업을 수행하려면 `dispose` 함수를 재정의한다. 예를 들어 타이머를 취소하거나 플랫폼 서비스에서 구독을 취소하려면 `dispose`를 재정의한다. `dispose` 구현은 일반적으로 `super.dispose`를 호출하여 끝낸다.

자세한 내용은 State를 참조하자.

### Keys

키를 사용하여 위젯이 다시 빌드될 때 프레임워크가 다른 위젯과 일치하는 위젯을 제어한다. 기본적으로 프레임워크는 `runtimeType` 과 그 나타나는 순서에 따라 현재 및 이전 빌드의 위젯을 일치시킨다. 키를 사용하면 프레임워크는 두 위젯이 동일한 `runtimeType`일뿐 만 아니라 동일한 키를 가질 것을 요구한다.

키는 동일한 유형의 위젯의 많은 인스턴스를 빌드하는 위젯에서 가장 유용하다. 예를 들어, 표시 영역을 채우기에 충분한 `ShoppingListItem` 인스턴스를 빌드하는 `ShoppingList` 위젯은 다음과 같다.

  - 키가 없으면 현재 빌드의 첫 번째 항목은 항상 이전 빌드의 첫 번째 항목과 동기화된다. 의미론적으로 목록의 첫 번째 항목이 화면 밖으로 스크롤되어 더 이상 뷰포트에 표시되지 않는 경우에도 마찬가지이다.

  - 목록의 각 항목에 "의미론적(semantic)" 키를 할당하면 프레임워크가 항목을 일치하는 의미론적 키와 동기화되고 이에 따라 유사한(또는 동일한) 시각적 모양이 동기화하므로 무한 목록이 더 효율적일 수 있다. 또한 항목을 의미론적으로 동기화한다는 것은 상태 저장 하위 위젯에 유지된 상태가 뷰포트에서 동일한 숫자 위치에 있는 항목이 아니라 동일한 의미론 항목에 연결된 상태로 남아 있음을 의미한다.

자세한 내용은 Key API를 참조하라.

### 전역 키 (Global Keys)

전역 키를 사용하여 자식 위젯을 고유하게 식별한다. 전역 키는 형제 간에 고유해야 하는 로컬 키와 달리 전체 위젯 계층에서 전역적으로 고유해야 한다. 전역적으로 고유하기 때문에 전역 키를 사용하여 위젯과 연결된 상태를 검색할 수 있다.

자세한 내용은 GlobalKey API를 참조하라.

