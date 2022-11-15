---
title:  "Dart문법(2)-Ternary operator, type casting, function"  
date:   2022-11-05 21:00:50 +0900
categories: [Dart syntax, Flutter]
tag: [Ternary operator, cascade notation, type casting, function ]
toc: true
---

### 삼항 연산자(Ternary operator)

``` dart
    bool isClear = true;
    var weather = isClear == true ? '맑음' : '흐림';
```

### Cascade notation

``` dart
    // var paint = Paint();
    // paint.color = 'black';
    // paint.strokeCap = ;

    var paint = Paint()  // ';' 를 붙이지 않는다. 
    ..color = 'black'
    ..strokeCap = ;

```

### type casting

``` dart

    num i = 10;
    int ii = i as int;  // type 이 달라서 오류날 때 강제로 type을 일치시킨다.

    num d = 10.5;
    double dd = d as double; 
```

### function

``` dart

    void main(){
        print (sum1(10, 20)); //  30
        print (sum2()); //  0
        print (sum2(a: 5)); //  5

    }

    int sum1(int a, int b){  // return-type,method-name, 입력매개변수
        return a + b; //, 함수내용 또는 return
    }

    int sum2({int a = 0, int b = 0}){  // named parameter
        return a + b; 
    }

    void main (){
        print ( calc(10,5, (a,b) => a+b)); // 함수를 파라메터로 받을 수 있다.
    }

    int calc(int a, int b , function(int, int) callback) {
        return callback(a,b);
    }
```

함수를 named parameter로 넣은 경우 (Flutter에서 많이 보게될 case)

``` dart
     void main (){
        print (calc(
            10,
            5, 
            callback: (a,b){ // 함수를 named parametr 로 넣은 경우
                return a + b;
            },
        ));
    }

    int calc(int a, int b ,{ required function(int, int) callback} ) {
        return callback(a,b);
    }
```


