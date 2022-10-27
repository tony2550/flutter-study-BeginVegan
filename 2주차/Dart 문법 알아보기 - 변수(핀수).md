# Dart 문법 알아보기1 - 변수

</br>

## DartPad

[DartPad](https://dartpad.dev/?)로 다트 문법을 알아보자

</br>

# Dart 실행 방식

- main 메소드 내부가 실행된다.

```dart
void main() {
		
}
```

</br>

# Dart 문법 알아보기

## 변수

### — 다트는 타입을 먼저 선언할 수도, 타입을 추론할 수도 있다.

</br>

```dart
void main() {
    // type variable = data;
    int n1 = 1; 
    double d1 = 10.1;
    bool b1 = true; // Boolean
    String s1 = "Amy";
    
    var n2 = 1;
    var d2 = 10.1;
    var b2 = false;
    var s2 = "Amy";
}
```

</br>
var 로 선언된 변수의 경우 타입 추론이 가능하다.

```dart
print(n2.runtimeType); // int
```

여기서 `n2 = “hello”;` 처럼 다른 타입을 대입하려는 순간 error가 발생한다.

한번 초기화 된 변수는 다른 타입으로 초기화 할 수 없다.

</br>

### — 다트는 String Template를 제공한다.

~~String Template 이 공식용어인지는 모르나..Kotlin은 String Template이라는 것을 제공하기 때문에 이렇게 이름 붙여보았다.~~

Java에서는 변수를 다른 문자열과 결합하여 출력할 때

다음과 같이 한다. (`String.format()` 은 논외로 둔다.)

```java
String name = "홍길동";
System.out.println("안녕하세요. " + name + "님!"); // 안녕하세요. 홍길동님!
```

</br>

Kotlin에서는 String Template을 제공해 보다 쉽게 사용할 수 있도록 한다.

```kotlin
val name = "홍길동"
println("안녕하세요. ${name}님!") // 안녕하세요. 홍길동님!
```

Dart에서도 다음과 같은 기능을 제공한다.

코틀린도 다트도 중괄호({}) 사용을 별로 좋아하지 않는다.

둘다 워닝과 인포를 내뱉는다.

그러나 아래와 같이 변수와 출력문의 구분이 필요할 경우 사용해야한다. (워닝도 안생김)

```dart
String name = "홍길동"
print("안녕하세요. ${name}님!") // 안녕하세요. 홍길동님!
```

Java에서처럼 문자열을 결합하면 error가 발생한다.

```dart
print("안녕하세요. " + name + "님!"); // error
```

</br>

### — Dart는 dynamic이라는 것을 제공한다.

dynamic : 모든 타입을 받을 수 있는 타입 (?)

var와 다른 게 무어냐..할 수 있지만

위에서 말했든 var는 한번 초기화되면 동일한 타입만 대입할 수 있다.

그러나 dynamic은 다른 타입도 대입이 가능하다.

```dart
dynamic dy1 = 1;
print(dy1.runtimeType); // int

dy1 = 10.2;
print(dy1.runtimeType); // double
```

</br>

# References

</br>

[이지업클래스 | 모두를 위한 온라인 IT CLASS](https://easyupclass.e-itwill.com/course/course_view.jsp?id=28&rtype=0&ch=course)