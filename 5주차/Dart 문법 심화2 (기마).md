# Dart 문법 심화2

### 01. 추상클래스

- 신입개발자야 왜 코드를 hungry로 만들었니…? 이전코드 안봤니…?
- → 이런 일들을 방지하기 위해서 만드는 것이 바로 추상클래스
  </br></br>

```dart
class Dog{
  void sound(){
    print("멍멍 배고파");
  }
 }

class Cat{
  void sound(){
    print("야옹 배고파");
  }
 }

class Fish{ //신입 개발자가 새롭게 만든 함수
  void hungry(){
    print("뻐끔뻐끔 배고파");
  }
 }

void main() {

  Dog d1 = Dog();
  Cat c1 = Cat();

  d1.sound();
  c1.sound();

  Fish f = Fish();
  f.sound(); //없음


}
```

</br>

- **강제성을 부여해준다, ✨타입일치✨ 를 위해서 사용**
- **@override :** 부모의 메써드를 자식이 같은 이름으로 만들면 바로 ✨동적 바인딩✨

</br>

```dart
//추상클래스 abstract
abstract class Animal{
  void sound();

}

//상속시에는 implements로 상속
class Dog implements Animal {
  void sound(){
    print("멍멍 배고파");
  }
 }

class Cat implements Animal {
  void sound(){
    print("야옹 배고파");
  }
 }

//새롭게 (Animal을 구현해서 ) 생성
class Fish implements Animal{

  @override //부모의 함수를 무효화 하고 -> 동적바인딩
  void sound(){
    print("뻐끔뻐끔 배고파"); //재정의

  }

}
```

</br></br>

### 02. 컬렉션

: 수집된 물품들을 말한다.

- int, double, bool, String 등 : 데이터를 하나만 받을 수 있다

```dart
// 01. 커스텀 자료형 : class
// -- 여러가지 데이터를 받을 수 있음
// -- 여러번 호출 가능
class User{
  int id = 1;
  String username = "cos";
}

void main() {
//   //02. List
//   List<int> nums = [1,2,3,4];
//   print(num[3]);

//     //타입추론도 사용가능
//     var nums2 = [3,4,5];
//     print(nums2[0]);

  //03. Map
  // - 클래스랑 유사한 자료형 하지만 선언 안해도 사용할 수 있다.
  // - 한번 만들어지면 끝임 그냥 사용해야함
  Map<String, dynamic> user = {
    "id":1,
    "username":"cos"

  };
  // map 호출
  print(user["id"]);
  print(user["username"]);


  //class 호출 => 여러번할 수 있다.
  User u = User();
  print(u.id);
  print(u.username);

}
```

</br></br>

### 03. 반복문 (for, map, where)

- 기본 반복문 **FOR**

  ```dart
  void main() {

    var list = [1,2,3,4];

    for(int i=0; i<4; i++){ //0,1,2,3
      print(list[i]); // 출력

    }

  }
  ```

  </br></br>

- **Map**

  - 람다식에는 리턴될 값을 넣어준다.
  - for문은 return 없음 하지만 ✨ map은 return 해준다. ✨
  - 반복되는 값을 하나씩 변화시키기 위해서 map을 많이 사용한다.
  - return 되는 값은 ✨ Iterable 타입이기때문에 list로 바꾸기 위해서 toList() 를 사용한다.

  ```dart
  var chobab = ["새우", "광어", "연어"];
  var chobabChange = chobab.map((i)=> "간장_"+i).toList();
  print(chobabChange);
  ```

  ```
  (간장_새우, 간장_광어, 간장_연어)
  ```

  </br></br>

- **Where**
  - 필터링하거나 새로운 값을 찾을 때 사용한다.
  - 람다식에 조건을 넣는다
  ```dart
  var chobab = ["새우", "광어", "연어"];
  var chobabChange = chobab.where((i)=> i=="장어").toList(); //찾기
  print(chobabChange);

  var chobabChange = chobab.where((i)=> i !="광어").toList(); //필터링(요소삭제)
  print(chobabChange);
  ```
