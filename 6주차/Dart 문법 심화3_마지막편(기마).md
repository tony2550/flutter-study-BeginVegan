# Dart 문법 심화3 (마지막)

### 01. 스프레드 연산자

</br>

- **깊은복사**

  - **spread = 흩뿌리다.**

  ```dart
  void main() {

    var list = [1, 2, 3];
  //var newList = list; 얕은 복사
    var newList = **[...list];** // ***깊은 복사*** -> 값을 복사함

    print(list);
    print(newList);

    list[0] = 10;

    print(list);
    print(newList);
  }
  ```

  ```
  [1, 2, 3]
  [1, 2, 3]
  [10, 2, 3]
  [1, 2, 3]
  ```

    </br>

- **추추가 복사법**<< 그래서 이름이 몬데
  - 컬렉션이 기본변수의 값을 들고있으면 깊은복사가 제대로 진행된다
  - 하지만 컬렉션이 맵이나 오브젝트, 클래스를 가지고 있을 때는
  ```
  var newList = **list.map((i)=> {...i}).toList();**
  ```
           위의 형태로 스프레드를 사용한다.

</br>

- **스프레드로 값 변경/수정하기**
  - 컬렉션을 순환하면서 값을 변경/추가하고 싶을때는 맵을 사용한다.
  ```dart
  var users = [
      {"id":1, "username": "cos", "pw":1234},
      {"id":2, "username": "ssar", "pw":5678},
    ];

  var newUsers = users.map((i)=> i["id"]==2 ? {...i, "username":"love"} : i).toList();
  print(newUsers);
  ```
  ```
  [{id: 1, username: cos, pw: 1234}, {id: 2, username: love, pw: 5678}]
  ```

</br></br>

### 02. Const, final

🌱각각의 공통점 과 특이점

- **final**
  - 값을 초기화 한 이후에 변경이 불가능하다.
  - String이라는 별도의 자료형을 적어주지않고 final name = “홍길동” 이렇게 적용 가능 → 타입추론
  - 생성시 초기화를 해줘야한다. (무조건)
- ✨ **const ✨**
  - 값을 상수화 시키는 작용
  - 값을 초기화한 이후에 변경이 불가능하다
  - 컴파일시에 초기화돼야 된다.
  - 생성자 앞에 const를 만들어내면
    - 동일한 객체는 값 메모리를 공유한다.
      → 메모리를 절약할 수 있다(앱 성능 향상에 기여함)
      → 동일한 그림을 한번 더 그릴지 말지 처리 가능
    ```dart
    class Animal{
      final name;

      const Animal(this.name);
    }

    void main() {

      Animal a1 = const Animal("강아지");
      Animal a2 = const Animal("강아지"); //고양이로 바꾸면 값 변경됨

      print(a1.hashCode);
      print(a2.hashCode);

    }
    ```
    ```
    532245237
    532245237

    //고양이로 바꿨을때의 hashCode
    25669484
    430004756
    ```

</br></br>

### 03. Null Safety ✨

- null 안전성
  - 아니 선생님 근데 지금 이 버전에서는 null safety 토글버튼이 없는데요?!
  - → 정리해서 확인해봐야함

</br>

- **옵셔널 타입**
  - String? name;
  - int? age; → null도 받고 다른 변수도 받을 수 있는 타입
  ```dart
  class Person{
    String? name;
    int? age;

    Person({this.name, this.age});
  }

  void main() {

    Person p = Person(name : "ssar");
    print(p.name);
    print(p.age ?? 1); //null 대체 연산자

  }
  ```

</br>

- **Required**
  - 무조건 값을 받아야 처리가 된다.
  - 생성시에 key값을 적는것이 편함
    → 선택적 매개변수를 사용해야함 → 옵셔널 타입으로 사용
    혹은
    → required를 처리해준다 → 옵셔널 타입으로 변경하지 않아도 된다.
