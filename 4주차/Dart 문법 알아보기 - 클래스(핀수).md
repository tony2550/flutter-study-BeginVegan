# Dart 문법 알아보기3 - 클래스

## 클래스

- 객체를 정의하는 설계도

### 객체

- 클래스(설계도)를 통해 현실 세계에 뿌리내릴 수 있는 것
- 아직 현실 세계에 존재하진 않지만 존재할 수 있는 가능성이 있는 것

⇒ 메모리에 로드할 수 있는 것

형태

```dart
class Dog {
	String name = "happy";
	int age = 4;
	String color = "white";
}
```

- 이때 클래스는 메모리에 로드 (객체 생성) 되지 않은 상태이다.

객체 생성하기

- Dart는 new 키워드를 생략할 수 있다.

```dart
void main(){
	// java에서는 익숙한 형태
	// new : 클래스를 메모리에 로드하겠다는 것을 의미
	// Dog dog = new Dog();
	Dog dog = Dog();
	print("강아지 이름은 ${dog.name}입니다."); // 클래스의 멤버 변수에 접근이 가능해진다.

	// 강아지 이름은 happy입니다.
}
```

### 생성자

위 클래스처럼 모든 강아지의 이름이 happy일 수는 없는법

생성 시 강아지의 속성을 정의해야한다면 어떡해야할까?

```dart
class Dog {
	String name;
	int age;
	String color;

	// 생성자의 매개변수를 인스턴스의 변수로 할당
	Dog(this.name, this.age, this.color);

	// 생성자의 매개변수로 값을 받아 생성자 본문에서 변수를 초기화
	Dog(String name, int age, String color) {
		this.name = name;
		this.age = age;
		this.color = color;
	}
}

void main() {
	Dog dog1 = Dog("toto", 4, "black");
	Dog dog2 = Dog("happy", 2, "yellow");

	print("강아지 이름은 ${dog1.name}입니다."); // 강아지 이름은 toto입니다.
	print("강아지 이름은 ${dog2.name}입니다."); // 강아지 이름은 happy입니다.
}
```

- 생성자가 없는 경우 기본 생성자 `클래스()` 가 자동으로 제공된다.
- 생성자가 존재하는 경우 기본 생성자는 제공되지 않는다. → 자바의 특징과 동일
    - 그러나 선택적 매개변수를 사용할 경우 기본생성자도 제공이 된다.

### 선택적 매개변수

- 매개변수를 선택형으로 설정하는 것을 의미
- 앞에 매개변수 명을 명시해야하므로 이름 있는 매개변수라고 부르기도 한다.
- 클래스에서 선택적 매개변수를 사용할 경우 초기값을 지정해줘야한다.
    - 안그러면 다음과 같은 오류가 난다.
        
        The parameter 'color' can't have a value of 'null' because of its type, but the implicit default value is 'null'.
        
        이럴 경우 non-null임을 명시해주면 되는듯한데 이는 나중에 알아보도록 하자.
        
- 매개변수 명을 명시하므로 순서를 틀려도 상관없다.
- 메소드에서도 사용할 수 있다.

```dart
class Dog {
	String name;
	int age = 4;
	String color = "black";

	Dog({this.name = "", this.age = 0, this.color = ""});

	void addAge(String name, int age, {String color=""}){
    print("$name 강아지는 올해로 $age살입니다. 털 색깔은 $color입니다.");
  }
}

void main() {
	Dog dog1 = Dog(name: "toto", age: 4, color: "black");
	Dog dog2 = Dog(age: 4, color: "yellow", name: "happy");

	print("강아지 이름은 ${dog1.name}입니다.");
	print("강아지 이름은 ${dog2.name}입니다.");
}
```

## 상속

- 부모가 가진 상태와 행위를 자식이 물려받는 것과 동시에 다형성이 성립해야 한다.

### 다형성

- 여러 가지 형태를 가질 수 있는 능력

```dart
class Burger{
	Burger(){
		print("맛있는 버거");
	}
}

class CheeseBurger extends Burger{
	CheeseBurger(){
		print("더 맛있는 치즈버거");
	}
}

void main(){
	Burger b = CheeseBurger();
	CheeseBurger cb = CheeseBurger();
	// 맛있는 버거
	// 더 맛있는 치즈버거
}
```

- 부모의 내부를 먼저 실행하고 자식의 내부가 실행된다.

### 이니셜라이저 키워드

- 자식클래스에서 부모클래스로 값을 할당할 때 사용
- `: super(해당 멤버 변수)`

```dart
class Burger{
	// 버전 3.3.6에서는 초기화해주지 않으면 오류가 난다.
	// 자세한 것은 null safty를 다루면서 알아보자.
  String name="";
  Burger(this.name){
    print("${this.name}은/는 버거다.");
  }
  
}

class CheeseBurger extends Burger{
  CheeseBurger(String name) : super(name);
}

void main() {
  CheeseBurger cb = CheeseBurger("치즈햄버거");
	// 치즈햄버거은/는 버거다.
}
```

## cascade notation (계단 표기법)

- 동일한 개체에 대해 일련의 작업을 수행할 수 있다.
- 함수 호출 외에 동일한 개체의 필드에도 액세스할 수 있다.

예시를 통해 알아보도록 하자.

Chef 라는 클래스가 있다.

Chef는 손도 씻고, 요리도 한다.

```dart
class Chef {
	void cook(){
		print("요리를 합니다.");
	}
	
	void handWash(){
		print("손을 씻습니다.");
	}
}
```

Chef 는 출근을 해서 요리를 한다.

이때 출근하는 행위는 Chef에게만 국한된 행동은 아니므로

Chef 클래스 외부에 있다. ← 수정 불가능

```dart
void goCampany(Chef c){
	c.cook();
}
```

```dart
void main(){
	Chef c = Chef();
	goCompany(c); // 요리를 합니다.
}
```

그런데 요리를 하기 전에 손을 씻고 싶다면 어떡하지?

회사를 가기전에 손을 씻게해도 될것이다.

그치만 회사 가는 동안 손이 더러워진다면?

그리고 원래 요리하기 전에..손 씻어야 되지요

이때 사용할 수 있는 것이 cascade이다.

```dart
void main() {
	Chef c = Chef();
  goCompany(Chef()..handWash());
	// 손을 씻습니다.
	// 요리를 시작합니다.
}
```

- 객체를 넘기면서 메소드를 실행할 수 있다.

자세한 것은 Flutter App을 만들면서 알게 될 듯하다.

# References

[이지업클래스 | 모두를 위한 온라인 IT CLASS](https://easyupclass.e-itwill.com/classroom/index.jsp?cuid=2354)

[Flutter - Dart 선택 매개변수(Named Parameter)](https://javariankm.tistory.com/52)

[Dart의 선택적 매개변수](https://lucky516.tistory.com/72)

[[Flutter] Dart 클래스의 생성자 [Constructors, Named Constructors, Initializer List]](https://zakkum.tistory.com/86)

[[OSAM] DART 언어 기초(9) Class [#4] 이니셜라이져 키워드](https://velog.io/@hello_hidi/OSAM-DART-%EC%96%B8%EC%96%B4-%EA%B8%B0%EC%B4%889-Class-4-%EC%9D%B4%EB%8B%88%EC%85%9C%EB%9D%BC%EC%9D%B4%EC%A0%B8-%ED%82%A4%EC%9B%8C%EB%93%9C)

[플러터(Flutter) - ".." 구문(Syntax)에 대해서(Cascade noation) ".."는 연산자(Operator)가 아니다.](https://m.blog.naver.com/chandong83/222051986313)