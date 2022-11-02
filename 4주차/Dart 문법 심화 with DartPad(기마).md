# Dart 문법

### 01. 생성자

- 이미 등록된 상태는 똑같은 내용으로 한 개만 만들어낼 수 있다.
    - 강아지 2마리를 만들기 위해서는
    
    >강아지< 가 있고 각자 가지는 상태가 변경된다 ⇒ ✨ 생성자를 사용하자
    
    ```dart
    
    class Dog{
      //상태
      String name;
      int age;
      String color;
      int thirsty; //max = 100
      
    //다트의 생성자 만드는 방법
      **Dog(this.name, this.age, this.color, this.thirsty);**
      
    }
    ```

</br>

- ✨ **선택적 매개변수**
    - 생성자에서 중괄호로 전체를 감싸서 만든다.
    - key : value 형태로 입력할 수 있다.
    - 순서를 안지켜도 된다
    - 안넣고 싶은 변수는 입력하지 않아도 된다.
    - 미리 값을 초기화 할 수 있다.
    
    ```dart
    class Dog{
      //상태
      String name;
      int age;
      String color;
      int thirsty; //max = 100
      
    //선택적 매개변수
      Dog({this.name, this.age = 1, this.color, this.thirsty});
      
    }
    
    void main() {
      
    //생성자 호출시 사용법
      Dog d1 = Dog(name : "Toto", age: 13, color : "white", thirsty : 100);
      Dog d2 = Dog( color : "yellow", name: "Momo");
      
      print(d1.name);
      print(d2.name);
    
    }
    ```
    
</br>

### 02. cascade 연산자
- 계단식 표현방법
- 객체를 넘기면서 함수를 실행할 수 있음
    - goToWork 함수가 실행될때 chef가 호출되면서 함수를 실행함
    - 2개도 넘길 수 있음
    
    ```dart
    class Chef{
      
      void cook(){
        
        print("요리를 시작합니다");
        
      }
      
      void handWash(){// 다트는 커멜표기법을 기본으로 한다. 
        
        print("손을 씻습니다");
      }
      
      
    }
    
    //수정할 수 없는 함수! 
    void goToWork(Chef c){
      
      c.cook();
      
    }
    
    void main() {
      
      goToWork(Chef()..handWash()); //계단 표기법
      
    }
    ```

</br></br>

### 03. 상속

: 부모가 가진 상태와 행위를 자식이 물려받는 것과 동시에 다형성이 성립해야한다.

- **다형성이란**
    
    : 여러가지 형태를 가질 수 있는 능력 
    
    - 아래와 위의 정의가 둘 다 성립해야한다.
    - 다형성을 만족하지 않으면 상속하지않는다.
    
    ```dart
    class Burger{
      
      Burger(){//생성자가 실행될때 뭔가 실행됨
        print("버거");
      }
      
    }
    
    class CheeseBurger extends Burger{
      
      CheeseBurger(){
        
        print("치즈버거");
      }
      
    }
    
    void main() {
      
      CheeseBurger cb = CheeseBurger();
      
      
    }
    ```
    
    실행내용 (Console)
    
    ```
    버거
    치즈버거
    ```
    
    </br>

     ✨ 여기서 주목 
    
    - 객체가 생성되면 자동으로 생성자가 실행된다
    - 상속받은 부모 클래스가 있는경우 부모의 생성자가 먼저 실행된다.
        
        ⇒ 이것이 바로 다형성. 치즈버거는 그냥 버거도 되고 치즈버거이기도 하다. 

</br>

- super활용
    
    ```dart
    class Burger{
     
      **String? name; //initialize expression : 자꾸 에러떠서 일단 해결**
      
      Burger(){//생성자가 실행될때 뭔가 실행됨
            
        print("버거");
        print(name);
      }
      
    }
    
    class CheeseBurger extends Burger{
      super.name = name; 
      CheeseBurger(String name);
      
    }
    
    void main() {
      
      CheeseBurger cb = CheeseBurger("치즈 햄버거");
      print(cb.name);
      
    }
    ```

</br>

- ✨이니셜라이즈 키워드✨
    - 부모를 실행할때 호출된 “치즈햄버거를 넘겨준다”
    - CheeseBurger 내부 실행전에 “치즈햄버거”(-초기값이)가 부모로 전달됨
    
    ```dart
    class Burger{
      
      
      String? name;
      
      Burger(this.name){//생성자가 실행될때 넘어온 name 값이 실행됨
            
        print(name);
      }
      
    }
    
    class CheeseBurger extends Burger{
      
      CheeseBurger(String name) : super(name){ //이 ':' 얘가 바로 이니셜라이즈 키워드
                           
      }
      
    }
    
    void main() {
      
      CheeseBurger cb = CheeseBurger("치즈 햄버거");
      
    }
    ```
    
</br>

### 04. ✨ Mixin

:  다형성을 만족하지 않는 상속을 진행하고 싶을때 사용

(다른 언어에서는 컴포지션을 사용한다고 함) 

⇒ 코드 재사용을 위해서 사용

```dart
class Engine{
 int power = 5000;  
}

//with을 사용해서 상속하지않고 코드 재사용 진행
class BMW with Engine{
  
}

void main() {
  
  BMW bm = BMW();
  print(bm.power);
  
  
}
```

```
//출력결과
5000
```

</br>

### Refs
[Dart 공식문서 ](https://dart.dev/tools/diagnostic-messages?utm_source=dartdev&utm_medium=redir&utm_id=diagcode&utm_content=not_initialized_non_nullable_instance_field#not_initialized_non_nullable_instance_field)

[Flutter 에러해결](https://stackoverflow.com/questions/67646067/flutter-class-error-try-adding-an-initializer-expression-or-add-a-field-initi)
