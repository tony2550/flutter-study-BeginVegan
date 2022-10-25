# 다트문법 기초

---

### 01. 다트패드

- Dart
    - 실행방법 : new pad / dart 체크 (html체크 )  패드 만들어짐
    - #으로 ID를 찾는다
    - 다트언어를 가지고 HTML을 수정할 수 있다
- Flutter
    - 실행방법 : new pad/ flutter / run

### 02. 다트의 변수

- 다트의 실행
    - main 함수를 꼭 포함한다
    - main 함수 내부가 실행된다
- 다트의 타입
    - 자료형 (int, double, bool, String) 존재한다

- 타입별 호출
    - print(”정수 : $n1”); << $를 사용해서 호출한다.
- 실습
    
    ```dart
    //타입학습 
      int n1 =1;
      double d1 = 10.1;
      bool b1 = true; //false
      String s1 = "홍길동";
      
      //프린트
      print("정수 : $n1");
      print("실수 : $d1");
      print("부울값 : $b1");
      print("문자열 : $s1");
    ```
    
    ```
    //console 실행시 결과
    
    정수 : 1
    실수 : 10.1
    부울값 : true
    문자열 : 홍길동
    ```
    

### 03. 타입추론

- 타입 추론 var
    
    *한번 초기화된 데이터 타입을 다른 타입으로 변경할 수 없다 
    
    ```dart
    var n1 = 1;
      var d1 = 10.1;
      var b1 = true;
      var s1 = "홍길동";
      
      print(n1);
      print(d1);
      print(b1);
      print(s1);
      
      print(n1.runtimeType); //실제로 실행될때의 타입을 확인할 수 있다
      
      n1 = 2;
      print(n1);
      n1 = 10.2; // error*
    ```
    

### 04. Dynamic

- 다이나믹하게 모든 타입을 다 받을 수 있는 자료형
    
    ```dart
    dynamic n1 =1;
      print(n1);
      print(n1.runtimeType);
      
      n1 = 10.5;
      print(n1);
      print(n1.runtimeType);
    ```
    
    출력형태
    
    ```
    1
    int
    10.5
    double
    ```
    

### 05. 연산자

- 산술, 비교, 논리 연산자 학습
- 주석처리 학습
    
    ```
    //산술연산자
    //   print(1+2);
    //   print(1-2);
    //   print(2*3);
    //   print(3/2);
    //   print(3%2);
    //   print(5~/2); //몫 연산자
      
      //비교연산자 (bool 리턴)
    //   print(2==3);
    //   print(2!=3);
    //   print(2<3);
    //   print(2>3);
    //   print(2<=3); 
    //   print(2>=3); 
      
      //논리연산자
      print(!true);
      print(true && false); //두 조건 모두 만족할때 true
      print(true || false); //둘 중 하나라도 만족하면 true
    ```
    

### 06. 조건문

- IF문
    - 체인이 걸려있다<< 라고 표현한다
    - 상위 코드가 실행되면 아래 코드는 중복으로 만족하더라도 실행되지않는다
    
    ```dart
    int point = 70;
     
      if(point >= 90){ 
        print("A");
      }else if(point >= 80){
        print("B");
      } else{
        print("F");
      }
    ```
    
- 삼항연산자
    - 한줄로 간단하게 적을 수 있는 조건문
    - 플러터에서 if문보다 더 자주 사용함
    
    ```dart
    int point = 60;
      print( point>= 60 ? "합격":"불합격");
    ```
    
- null 대체언어
    - '??' 이라고 적고
    - null일 경우 해당 값을 출력 아니면 그냥 원래 값을 출력함