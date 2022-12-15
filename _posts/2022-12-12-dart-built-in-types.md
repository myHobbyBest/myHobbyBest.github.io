---
title:  "Built-in types"  
date:   2022-12-12 09:00:20 +0900
categories: [Flutter, Dart]
tag: [Built-in types]
toc: true
---
### 내장 유형 (Built-in types)

Dart 언어는 아래와 같은 것들을 특별히 지원한다.

- Numbers (int, double)
- Strings (String)
- Booleans (bool)
- Lists (List, 배열이라고도 함)
- Sets (Set)
- Maps (Map)
- Runes (Runes; 종종 문자 API로 대체됨)
- Symbols (Symbol)
- The value null (Null)

이 지원에는 리터럴을 사용하여 개체를 만드는 기능이 포함된다. 예를 들어 'this is a string'은 `string` 리터럴이고 true는 `bool` 리터럴이다.

Dart의 모든 변수는 객체(클래스의 인스턴스)를 참조하기 때문에 일반적으로 생성자를 사용하여 변수를 초기화할 수 있다. 일부 built-in type 에는 자기자신의 고유한 생성자가 있다. 예를 들어 `Map()` 생성자를 사용하여 map을 만들 수 있다.

일부 다른 유형도 Dart 언어에서 특별한 역할을 한다.

- `Object` : Null을 제외한 모든 Dart 클래스의 슈퍼클래스이다.
- `Enum` : 모든  enum들의 슈퍼클래스이다.
- `Future` 와 `Stream` : 비동기 지원에 사용된다.
- `Iterable` : for-in loop 및 동기 생성기 함수에 사용된다.
- `Never` : 표현식이 평가를 성공적으로 완료할 수 없음을 나타낸다. 항상 예외를 발생시키는 함수에 가장 자주 사용된다.
- `dynamic`: 정적 검사를 비활성화할 것임을 나타낸다. 일반적으로 `Object` 또는 `Object?`를 사용해야 한다.
- `void`: 값이 사용되지 않음을 나타낸다. 반환 유형으로 자주 사용된다.

`Object`, `Object?`, `Null` 및 `Never` 클래스는 null safty 이해의 상위 및 하위 섹션에 설명된 것 처럼 클래스 계층 구조에서 특별한 역할을 한다.

- #### Numbers

다트에서 Number에는 두 가지 종류가 있다.

`int`
플랫폼에 의존하지만  대개 64비트 이하의 정수 값이다. 기본 플랫폼에서 값은 $-2^{63}$ 에서 $2^{63}-1$ 까지일 수 있다. 웹에서 정수 값은 JavaScript 숫자(소수부가 없는 64비트 부동 소수점 값)로 표시되며 $-2^{53}$ 에서 $2^{53}-1$ 까지일 수 있다.

`double`

IEEE 754 표준에 지정된 64비트(double-precision) 부동 소수점 숫자이다.

`int`와 `double`은 모두 `num`의 하위 유형이다. `num` 유형에는 `+`, `-`, `/` 및 `*`와 같은 기본 연산자가 포함되며 `abs()`, `ceil()` 및 `floor()` 등의 메서드도 있다. ( `>>` 와 같은 비트 연산자는 `int` 클래스에 정의되어 있다.) `num` 및 해당 하위 유형에 원하는 것이 없으면 `dart:math` 라이브러리에서 찾을 수 있다.

정수는 소수점이 없는 숫자이다. 다음은 정수 리터럴을 정의하는 몇 가지 예이다.

``` dart
var x = 1;
var hex = 0xDEADBEEF;
```

숫자에 소수점이 포함되어 있으면 `double`이다. 다음은 `double` 리터럴을 정의하는 몇 가지 예이다.

``` dart
var y = 1.1;
var exponents = 1.42e5;
```

변수를 `num`으로 선언할 수도 있다. 이렇게 하면 변수가 `int` 값과 `double` 값을 모두 가질 수 있다.

```dart
num x = 1; // x can have both int and double values
x += 2.5;
```

`int` 리터럴은 필요할 때 자동으로 `double`로 변환된다.

```dart
double z = 1; // Equivalent to double z = 1.0.
```

문자열을 숫자로 변환하거나 그 반대로 변환하는 방법은 다음과 같다.

```dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

int 유형은  비트 필드에서 플래그 조작 및 마스킹에 유용한 전통적인 비트 시프트(<<, >>, >>>), complement (~), AND(&), OR(|) 및 XOR(^) 연산자를 활용한다.예를 들어:

``` dart
assert((3 << 1) == 6); // 0011 << 1 == 0110
assert((3 | 4) == 7); // 0011 | 0100 == 0111
assert((3 & 4) == 0); // 0011 & 0100 == 0000
```

더 많은 예제를 보려면 bitwise and shift operator 섹션을 참조하자.

리터럴 숫자는 컴파일 타임 상수이다. 피연산자가 숫자로 평가되는 컴파일 시간 상수인 한 많은 산술 표현식도 컴파일 시간 상수가 된다.

``` dart
const msPerSecond = 1000;
const secondsUntilRetry = 5;
const msUntilRetry = secondsUntilRetry * msPerSecond;
```

더 자세한 것은 Numbers in Dart 를 참고하자.

- #### Strings (문자열)

Dart 문자열(String 객체)는 UTF-16 코드 단위 시퀀스를 유지한다. 작은 따옴표(`'`) 또는 큰 따옴표(`"`)를 사용하여 문자열을 만들 수 있다.

``` dart
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```

`${expression}`을 사용하여 표현식의 값을 문자열 안에 넣을 수 있다. 표현식이 식별자인 경우 `{}`를 건너뛸 수 있다.  Dart에서 객체에 해당하는 문자열을 얻으려면 객체의 `toString()` 메서드를 호출한다.

``` dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
         'Dart has string interpolation, '
         'which is very handy.');

assert('That deserves all caps. '
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. '
        'STRING INTERPOLATION is very handy!');
```

(참고: `==` 연산자는 두 개체가 동일한지 여부를 테스트한다. 두 문자열이 동일한 코드 단위 순서로 구성되면 동일하다.)

문자열 리터럴을 인접 시키거나 `+` 연산자를 사용하여 문자열을 연결할 수 있다.

``` dart
var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
assert(s1 ==
    'String concatenation works even over '
        'line breaks.');

var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```

여러 줄 문자열을 만드는 또 다른 방법: 작은 따옴표 또는 큰 따옴표를 이용하여 삼중따옴표를 구성한다.

``` dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```

r을 접두어로 지정하여 "raw" 문자열을 생성할 수 있다.

``` dart
var s = r'In a raw string, not even \n gets special treatment.';
```

유니코드 문자를 문자열로 표현하는 방법에 대한 자세한 내용은  Runes and grapheme clusters를 참조한다.

리터럴 문자열은 interpolated 표현식이 null 또는 숫자, 문자열 또는 bool 값으로 평가되는 컴파일 시간 상수인 한 컴파일 시간 상수이다.

``` dart
// These work in a const string.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// These do NOT work in a const string.
var aNum = 0;
var aBool = true;   
var aString = 'a string';
const aConstList = [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString';
// const invalidConstString = '$aNum $aBool $aString $aConstList';
```

문자열 사용에 대한 자세한 내용은 Strings and regular expressions 을 참조한다.

- #### Booleans

불리언 값을 나타내기 위해 Dart에는 bool이라는 유형이 있다. 부울 리터럴 true 과 false 두 개체만 bool 유형을 갖는다. 둘 다 컴파일 타임 상수이다.

Dart의 유형 안전성(type safety)이란 `if(nonbooleanValue)`또는 `assert(nonbooleanValue)`와 같은 코드를 사용할 수 없음을 의미한다. 대신 다음과 같이 명시적으로 값을 확인한다.

``` dart
// 빈 문자열을 확인한다.
var 전체 이름 = '';
assert(fullName.isEmpty);

// 0인지 확인한다.
var hitPoints = 0;
assert(hitPoints <= 0);

// null을 확인한다.
var 유니콘;
assert(유니콘 == null);

// NaN을 확인한다.
var iMeantToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
```

- #### List

아마도 거의 모든 프로그래밍 언어에서 가장 일반적인 컬렉션은 __배열(array)__ 또는 __정렬된 객체 그룹__ 일 것이다. Dart에서 배열은 List 객체이므로 대부분의 사람들은 배열을 List 이라고 부른다.

Dart의 List 리터럴은 쉼표로 구분된 표현식 또는 값의 목록을 대괄호(`[]`)로 묶어서 표시한다. 다음은 간단한 Dart List이다.

```dart
var list = [1, 2, 3];
```

(참고: Dart는 앞의 변수 `list` 가 `List<int>`유형이라고 추론한다. 정수가 아닌 개체를 이 `list` 에 추가하려고 하면 컴파일 또는 런타임에서 오류가 발생한다. 자세한 내용은 형식 유추(type inference) 를 참고한다.)

Dart 컬렉션 리터럴의 마지막 항목 뒤에 쉼표를 추가할 수 있다. 이 후행 쉼표는 컬렉션에 영향을 주지 않지만 복사-붙여넣기 오류를 방지하는 데 도움이 될 수 있다.

``` dart
var list = [
  'Car',
  'Boat',
  'Plane',
];
```

`List`는 0부터 시작하는 인덱싱을 사용한다. 여기서 0은 첫 번째 값의 인덱스이고 `list.length - 1`은 마지막 값의 인덱스이다. `.length` 속성을 사용하여 목록의 길이를 가져오고 첨자 연산자(`[]`)를 사용하여 `List`의 값에 액세스할 수 있다.

``` dart
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
```

컴파일 시간 상수인 List를 만들려면 List 리터럴 앞에 const를 추가한다.

``` dart
var constantList = const [1, 2, 3];
// constantList[1] = 1; // This line will cause an error.
```

Dart는 컬렉션에 여러 값을 삽입하는 간결한 방법을 제공하는 스프레드연산자  ( __spread operator__ ) ``...`` 및 null 인식 스프레드 연산자 ( __null-aware spread operator__ ) ``...?``를 지원한다.

예를 들어 스프레드 연산자 ``...``를 사용하여 List의 모든 값을 다른 List에 삽입할 수 있다.

``` dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```

스프레드 연산자 오른쪽에 있는 표현식이 null일 수 있는 경우 null 인식 스프레드 연산자(...?)를 사용하여 예외를 방지할 수 있다.

``` dart
var list2 = [0, ...?list];
assert(list2.length == 1);
```

스프레드 연산자 사용에 대한 자세한 내용과 예는  spread operator proposal 을 참조한다.

Dart는 조건문(if) 및 반복(for)을 사용하여 컬렉션을 구축하는 데 사용할 수 있는 컬렉션 if 및 컬렉션 for도 제공한다.

다음은 3개 또는 4개의 항목이 있는 List을 만들기 위해 collection if를 사용하는 예이다.

``` dart
var nav = ['Home', 'Furniture', 'Plants', if (promoActive) 'Outlet'];
```

다음은 다른 list에 항목을 추가하기 전에 list 항목을 조작하기 위해 collection for 를 사용하는 예이다.

``` dart
var listOfInts = [1, 2, 3];
var listOfStrings = ['#0', for (var i in listOfInts) '#$i'];
assert(listOfStrings[1] == '#1');
```

컬렉션 if 및 for 사용에 대한 자세한 내용과 예는  control flow collections proposal 을 참조한다.

List 유형에는 list을 조작하기 위한 편리한 방법이 많이 있다. list에 대한 자세한 내용은  Generics 과 Collections 을 참조한다.

- #### Sets

Dart의 set는 단일항목의 정렬되지 않은 콜렉션이다. set세트에 대한 Dart 지원은 set 리터럴 및 set 유형에 의해 제공된다.

다음은 set 리터럴을 사용하여 만든 간단한 Dart set이다.

``` dart
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```

(참고: Dart는 앞의 예에서  변수 halogens 이 `Set<String>` 유형이라고 추론합니다. set에 잘못된 유형의 값을 추가하려고 하면 디버거 또는 런타임에서 오류가 발생합니다. 자세한 내용은  type inference 에 대해 읽어보자.)

텅빈 집합을 만들려면 {} 앞에 유형 인수를 쓰거하거나 {}를 Set 유형의 변수에 할당한다.

```dart
var names = <String>{};
// Set<String> names = {}; // This works, too.
// var names = {}; // Creates a map, not a set.
```

(참고: __set인가 map인가?__ : map 리터럴의 구문은 set 리터럴의 구문과 비슷하다. map 리터럴이 먼저 나왔기 때문에 `{}`는 기본적으로 map 유형이다. `{}`의 유형 주석이나 할당된 변수를 잊은 경우 Dart는 `Map<dynamic, dynamic>` 유형의 객체를 생성한다.)

add() 또는 addAll() 메서드를 사용하여 기존 set에 항목을 추가한다.

```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
```

`.length`를 사용하여 set의 항목 수를 가져온다.

```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
assert(elements.length == 5);
```

컴파일 시간 상수인 set을 만들려면 set 리터럴 앞에  `const`를 추가합니다.

```dart
final constantSet = const {
  'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
};
// constantSet.add('helium'); // This line will cause an error.
```

set는 list와 마찬가지로 스프레드 연산자(... 및 ...?)와 컬렉션 if 및 for를 지원한다. 자세한 내용은 list spread operator 와 list collection operator  토론을 참조한다.//요.

set에 대한 자세한 내용은  Generics 과 Sets 참조한다.

- #### Maps

일반적으로 map은 키(key)와 값(value)을 연결하는 개체입니다. 키와 값 모두 모든 유형의 객체가 될 수 있다. 각 키는 한 번만 발생하지만 동일한 `vlaue`는 여러 번 사용할 수 있습니다. map에 대한 Dart의 지원은 map 리터럴과 map type에 의해 제공,된다.

다음은 map 리터럴을 사용하여 만든 몇 가지 간단한 Dart map이다.

``` dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

(참고: 앞의 예에서 Dart는 변수 gifts 는 Map<String, String> 유형이고 변수 nobleGases는 Map<int, String> 유형이라고 추론합니다. map에 잘못된 유형의 값을 추가하려고 하면 디버거 또는 런타임에서 오류가 발생합니다. 자세한 내용은 type inference 에 대해 읽어보자.)

Map 생성자를 사용하여 동일한 개체를 만들 수 있다.

``` dart
var gifts = Map<String, String>();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = Map<int, String>();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

(참고: C# 또는 Java와 같은 언어를 사용하는 경우 Map() 대신 new Map()이 나타날 것으로 예상할 수 있다. Dart에서 new 키워드는 선택 사항이다. 자세한 내용은 생성자 사용을 참조하자.)

아래 첨자 할당 연산자(`[]=`)를 사용하여 기존 맵에 새 key-value 쌍을 추가한다.

``` dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
```

아래 첨자 연산자([])를 사용하여 맵에서 값을 검색한다.

```dart
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```

맵에 없는 키를 찾으면 null이 반환된다.

```dart
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

`.length`를 사용하여 맵에서 key-value 쌍의 갯수를 가져온다.

```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```

컴파일 시간 상수인 map을 만들려면 map 리터럴 앞에 `const`를 추가한다.

``` dart
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// constantMap[2] = 'Helium'; // This line will cause an error.
```

map는 list처럼 스프레드 연산자(... 및 ...?)와 콜렉션 if 및 for를 지원한다. 자세한 내용과 예제는 spread operator proposal 및  control flow collections proposal을 참조한다.

지도에 대한 자세한 내용은  generics 섹션과 Maps API에 대한 라이브러리 둘러보기를 참조한다.

- #### Runes and grapheme clusters

Dart에서 룬(Runes)은 문자열의 Unicode 코드 포인트를 노출한다. 문자 패키지를 사용하여 유니코드(확장된) 문자소 클러스터라고도 알려진 사용자 인식 문자를 보거나 조작할 수 있다.

유니코드는 전 세계의 모든 쓰기 시스템에서 사용되는 각 문자, 숫자 및 기호에 대해 고유한 숫자 값을 정의한다. Dart 문자열은 UTF-16 코드유닛의 시퀀스이기 때문에 문자열 내에서 유니코드 코드 포인트를 표현하려면 특별한 구문이 필요하다. 유니코드 코드 포인트를 표현하는 일반적인 방법은 `\uXXXX`이다. 여기서 `XXXX`는 4자리 16진수 값이다. 예를 들어 하트 문자(♥)는 `\u2665`이다. 4자리 이하 또는 이상인 16진수를 지정하려면 값을 중괄호 안에 넣는다. 예를 들어 웃는 이모티콘(😆)은 `\u{1f606}`이다.

개별 유니코드 문자를 읽거나 써야 하는 경우 문자 패키지에서 String에 정의한 문자 getter를 사용한다. 반환된 `Characters` 객체는 일련의 문자소 클러스터로서의 문자열이다. 다음은 문자 API를 사용하는 예이다.

```dart
import 'package:characters/characters.dart';

void main() {
  var hi = 'Hi 🇩🇰';
  print(hi);
  print('The end of the string: ${hi.substring(hi.length - 1)}');
  print('The last character: ${hi.characters.last}');
}
```
출력은 ,사용된 시스템환경에 따라 다르지만, 다음과 같이 표시된다.

``` console
$ dart run bin/main.dart
Hi 🇩🇰
The end of the string: ???
The last character: 🇩🇰
```

문자 패키지를 사용하여 문자열을 조작하는 방법에 대한 자세한 내용은 문자 패키지에 대한 예제 및  API reference 를 참고한다.

- #### Symbols

`Symbol` 객체는 Dart 프로그램에서 선언된 연산자 또는 식별자를 나타낸다. 심볼기호를 사용할 필요가 없을 수도 있지만  `minification`는 식별자 이름을  변경하지만 식별자 기호는 변경하지 않기 때문에 이름으로 식별자를 참조하는 API에 매우 중요하다.

식별자에 대한 심볼기호를 얻으려면 `Symbol` 리터럴을 사용한다. `Symbol`리터럴은 # 다음에 식별자가 오는 것이다.

``` dart
#radix
#bar
```

`Symbol`  리터럴은 컴파일 타임 상수이다.
