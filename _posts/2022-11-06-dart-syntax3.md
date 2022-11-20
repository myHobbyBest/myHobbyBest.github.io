---
title:  "Dart문법(3) - List"  
date:   2022-11-06 17:20:30 +0900
categories: [Flutter, Dart syntax ]
tag: [list,   addall, map, expand(), asMap()]
toc: true 
---


### List

``` dart

List<int> items = [1, 2, 3];
  print(items.length); // 3 (요소의 총갯수 )
  print(items.reversed); // 3,2,1 
  print(items.runtimeType); // JSArray<int>
  print(items.first); //  1   첫번재 요소
  print(items.last);  // 3  마지막 요소
  print(items.isEmpty); // false
  print(items.isNotEmpty); // true
  items.hashCode; //  객체가 같은지 여부를 빠르게 판단하기 위해 사용됨.  객체의 내부 요소들을 정수로 변환하여 구현 
  items.single //요소 갯수가 한개일 때만 그 값을 반환, 그외는 모두  StateError를  반환
```

#### iterator 와 addAll

``` dart
  
var myList = [25, 63, 84]; 
    var myListIter = myList.iterator;   //get iterator to the list
        
    while(myListIter.moveNext()){ //iterate over the list
        print(myListIter.current); // 엘레멘트를 한개씩 순서대로 반환한다.
    } // 따라서 이는 아래의 반복문과 완전히 동일한 결과를 출력한다.
    myList.foreach ( item){
        print(item);
    }
    myList.forEach((item) => print(item));
    myList.forEach(print);

    // use every()
    myList.every((item) {
        print(item);
        return true;
    });
    // for loop with item index
    for (var i = 0; i < myList.length; i++) {
        rint(myList[i]);
    }


var yourList = [1,2,3];    
    myList.addAll(yourList);  // 또 다른 List를 뒤쪽에 연결하여 합친다.
     print(myList); //  [25, 63, 84, 1 , 2, 3]

```

#### 구성요소 위치 찾기 (contains 등) 

``` dart
var myList = [0, 3, 4, 8, 6, 2, 7];
myList.contains(3);                        // true
myList.contains(5);                        // false
myList.indexOf(2);                         // 5
myList.lastIndexOf(2);                     // 5
myList.indexWhere((item) => item > 5);     // 3
myList.lastIndexWhere((item) => item > 5); // 6
```



#### any 조건문

``` dart

  var myList = [1, 3, 10, 11];

  if (myList.any((n) => n > 10)) { // 10보다 큰 것이 하나라도 있으면 
    print('At least one number > 10'); //  'At least one number > 10' 를 출력한다. 
  }
```

#### map 
``` dart
var myList = ['zero', 'one', 'two', 'three', 'four', 'five'];
  
  var uppers1 = myList.map((item) => item.toUpperCase());
  print(uppers1); // (ZERO, ONE, TWO, THREE, FOUR, FIVE)
  
  var uppers = myList.map((item) => item.toUpperCase()).toList();  
  print(uppers); // [ZERO, ONE, TWO, THREE, FOUR, FIVE]
  ```

#### 내부 조건문 if, 내부 반복문 for

``` dart
var mobile = true;
var web = false;
var tringList = ['kotring', 'dart', if (mobile) 'flutter', if(web) 'reat']; 
// [kotrinn, dart, flutter]

var intList = [for (var i = 1; i < 10; i++) i];
 // [1, 2, 3, 4, 5, 6, 7, 8, 9]

var evenList = [
  for (var i = 1; i < 10; i++)
    if (i % 2 == 0) i // 중괄호없이도 쓴다.
]; // [2, 4, 6, 8]

```

#### List of Lists의 반복문 => iteration의 구현방법

```dart

var listOfNumbers = [[1, 2], [3, 4, 5], [6, 7, 8]];
// 전통적인 for loop
for (var i = 0; i < listOfNumbers.length; i++) {
  for (var j = 0; j < listOfNumbers[i].length; j++) {
    print(listOfNumbers[i][j]);
  }
}

// 짧고 간단한 foreach 
listOfNumbers.forEach((nums) => nums.forEach((number) => print(number)));

// every와 foreach의 조합
listOfNumbers.every((nums) {
  nums.forEach((number) => print(number));
  return true;
});

//  for문 의 중복
for (var nums in listOfNumbers) {
  for (var number in nums) {
    print(number);
  }
}



/* Result:
1
2
3
4
5
6
7
8
*/

```

#### expand() method => Flatten List of Lists

``` dart
var listOfNumbers = [[1, 2], [3, 4, 5], [6, 7, 8]];

var flattenList = [];
flattenList = listOfNumbers.expand((number) => number).toList();
// [1, 2, 3, 4, 5, 6, 7, 8]

var flattenList1 = [];
listOfNumbers
    .forEach((nums) => nums.forEach((number) => flattenList1.add(number)));
// [1, 2, 3, 4, 5, 6, 7, 8]

```

### Useful List methods 

#### sublist():

``` dart
 var myList= [1,2,3,4,5]; 
 // myList.sublist(start,end) -> strat부터 end까지.
 print(myList.sublist(1,3)); // [2,3]

 // myList.sublist(start) -> strat부터 끝까지.
 print(myList.sublist(1)); // [2,3,4,5] 
```
#### shuffle():

``` dart

 var myList= [1,2,3,4,5]; 
 myList.shuffle();
 print('$myList'); // [5,4,3,1,2]  무작위로 섞는다.
```

#### asMap():

``` dart

 List<String> sports = ['cricket', 'football', 'tennis', 'baseball'];
 Map<int, String> map = sports.asMap();
 print(map); // {0: cricket, 1: football, 2: tennis, 3: baseball}
```

#### whereType():

``` dart
 var mixList = [1, "a", 2, "b", 3, "c", 4, "d"];
 var num = mixList.whereType<int>(); // int type만 골라낸다. []가 아님에 주의하자!!
 print(num); // (1, 2, 3, 4)

 mixList.whereType<String>(); // string만 골라낸다. 
 print(num); // ( "a", "b", "c",  "d")

```

#### getRange():

``` dart
var myList = [1, 2, 3, 4, 5];
 print(myList.getRange(1,4)); // (2, 3, 4) subList 와 동일하나 괄호가 다르다.
```

#### replaceRange():

```dart
  var rList= [0,1,2,3,4,5,6];
  // replaceRange(start,end,value) start포함, end불포함
 rList.replaceRange(2,4, [10,2]);
 print('$rList'); // [0, 1, 10, 3, 4, 5, 6]
 ```

#### firstWhere(): , lastWhere() -->구성요소 값(value) 찾기 

``` dart
var myList = [0, 2, 4, 5, 7, 2, 8];
myList.where((item) => item > 5).toList();   // [7, 8]
myList.firstWhere((item) => item > 5);       // 7
myList.lastWhere((item) => item > 5);        // 8
```

####  singleWhere():

``` dart
 var mList = [1, 2, 3, 4];
 print(mList.singleWhere((i) => i == 3)); // 3

 var sList = [1, 2, 3, 3, 4];
 print(sList.singleWhere((i) => i == 3)); 
// Bad state: Too many elements

//  -->  mList.single은 값을 반환하고 mList.singleWhere는 index를 반환한다.
```

####  fold(): && reduce():



``` dart
 var lst = [1,2,3,4,5];
 var res = lst.fold(5, (i, j) => i + j); // 총합 또는 곱을 구할 때 유용하다.
 print('res is ${res}'); // res is 20
```
5+1 -> 6+2 -> 8+3 -> 11+4 -> 15+5 ==> 20 
initialValue에 하나씩 꺼내서 더해간다.
length 가 1 될 때까지 반복한다

```dart

 var lst = [1,2,3,4,5];
 var res = lst.reduce((i, j) => i + j);
 print('res is ${res}'); // res is 15
```
reduce는 초기값이 없다.

#### followedBy():

``` dart
var sportsList = ['cricket', 'tennis', 'football'];
print(sportsList.followedBy(['golf', 'chess']).toList()); 

var myList = ['golf', 'chess'];  
print(sportsList.followedBy(myList).toList()); 
// [cricket, tennis, football, golf, chess] --> .addAll과 동일한 결과이다.
```

#### take(): & skip();

``` dart
print(sportsList.take(2));  // (cricket, tennis) 앞에서부터 2개를 취한다.

print(sportsList.skip(2));  // (football) 앞에서 2개를 제외한 후 하나를 취한다.

```
