# 다트문법

### 01. 함수(메소드)

- 특별한 목적을 가진 코드를 모아놓은 것
  → 자주 사용하고 반복되는 작업을 쉽게 처리하기 위해서 작업
  → 코드의 집합을 만든다(중갈호{ } 사용)
  ⇒ 코드의 재사용을 위함
  ```dart
  void numPrint(){
    print(1);
    print(2);
    print(3);
    print(4);
  }

  void main() {

     numPrint();
     numPrint();
     numPrint();

  }
  ```
    </br>
- 매개변수
  - add 함수가 실행될때 매개변수를 넣을 수 있다
  - add 함수의 실행이 종료되면 sum은 사라진다 ⇒ 지역변수
    → 이후에도 사용하고싶으면 return을 사용해서 함수의 결과값을 만들어줘야한다
  ```dart
  void add(int n1, int n2){
  //함수가 실행될때만 메모리에 올라왔다가 종료되면 사라진다.
    int sum = n1+n2;
    print(sum);
  }

  int add(int n1, int n2){
    int sum = n1+n2;
    print(sum);
  	return sum;
  }

  void main() {

  //   numPrint();
  //   numPrint();
  //   numPrint();

    int result = add(1,5);
  	print(result);
  }
  ```

</br>
</br>

### 02. 익명함수와 람다식

- 어짜피 실행되니까 굳이 이름을 안부르는 함수
  - 코드의 내부가 변경되는 함수는 좋은 함수가 아니야
    - 함수의 내부를 수정하지않고 호출할때 결정할 수 있음
  ```dart
  // void run(){
  //   print("달리기");
  // }

  // void study(){
  //   print("공부");
  // }

  //하루의 루틴을 결정해줌
  void routine(Function start){
    String result = start();
    print(result);
  }

  void main() {
    routine((){
      return "짜파게티 먹기";
    });
  }
  ```
    </br>


### 03. 람다식

- 익명함수랑 유사하다 (위 항목에서 이어서 처리)
- 괄호다음에 바로 화살표를 넣는다
  - 중괄호 대신 화살표를 넣는다
  - 그 다음 코드는 무조건 return문이 된다.
  ```dart
  void main() {
    routine((){
      return "짜파게티 먹기";
    });


    routine(()=>"신라면 먹기");

  }
  ```

</br>

### 04. 람다식과 익명함수의 구분과 사용

- 구분
  - 한 줄만 적어서 처리가 가능하면 람다식을 사용한다.
  - 여러 줄을 사용해야하면 익명함수를 사용한다.
- 사용
  - 여러 함수들을 다 만들 수 없을때 미리 만들어두고 호출해서 사용한다.
  - (경우의 수가 너무 많을 경우 활용)

</br>

### 05. 클래스

: 현실세상에 존재하는 대부분의 것들은 클래스로 표현할 수 있다.
</br>

**객체란?**

: 클래스를 통해 현실 세계에 뿌리내릴 수 있는 것을 말한다. 아직 존재하지 않지만 존재할 수 있는 가능성이 있는 것들

- 프로그래밍 세상에서 객체란 메모리에 로드할 수 있는 것을 말한다.

</br>

**객체지향프로그래밍**

- 특징 : 메모리에 로드가 안되어있음
  메모리로드 => 객체생성 => 오브젝트
- 클래스에 있는 내용들은 객체 생성이후에 호출할 수 있다.

```dart
//특징 : 메모리에 로드가 안되어있음
// 메모리로드 => 객체생성 => 오브젝트

class Dog{
  String name="Toto";
  int age = 13;
  String color = "white";
  int thirsty = 100; //max = 100
}

void main() {

  //객체생성
  Dog d1 = Dog(); // 다트에서는 new 생략 가능
	print(d1.name);
}
```

- 시나리오 진행

  - 문자열과 함께 사용할때 . 호출이 필요하면 중괄호를 사용해야한다.
  - 갈증지수는 행위를 통해서 변경해야한다. (마법 쓰지마)
    ⇒ 클래스 내부에 메서드를 만든다 (책임, 행위)
    ⇒ 상태는 행위를 통해서 변경한다.
    ```dart
    //특징 : 메모리에 로드가 안되어있음
    // 메모리로드 => 객체생성 => 오브젝트

    class Dog{
      //상태
      String name="Toto";
      int age = 13;
      String color = "white";
      int thirsty = 100; //max = 100

      //책임, 행위
      void drinkWater(){
        thirsty = thirsty-50;
      }
    }

    void main() {

      //객체생성
      Dog d1 = Dog(); // 다트에서는 new 생략 가능
      print(d1.name);

      //d1.thirsty = 50;
      //상태는 행위를 통해서 변경한다
      d1.drinkWater();
      print("갈증지수 : ${d1.thirsty}");
    }
    ```

- 모든 것들이 객체로 존재하면서 서로 상호작용한다.

  ```dart
  void main() {

    //객체생성
    Dog d1 = Dog(); // 다트에서는 new 생략 가능
    print(d1.name);

    //d1.thirsty = 50;
    //상태는 행위를 통해서 변경한다
    Water w = Water();
    d1.drinkWater(w);
    print("갈증지수 : ${d1.thirsty}");
    print("물의 양 : ${w.liter}");


    d1.drinkWater(w);
    print("갈증지수 : ${d1.thirsty}");
    print("물의 양 : ${w.liter}");

  }
  ```

    </br>

  - 함수를 통해서 변경된 내용들이 반영된다.

  ```
  //출력 상태
  Toto
  갈증지수 : 50
  물의 양 : 1.5
  갈증지수 : 0
  물의 양 : 1
  ```
