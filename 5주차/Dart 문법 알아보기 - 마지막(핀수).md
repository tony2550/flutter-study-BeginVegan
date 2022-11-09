# Dart 문법 알아보기 - 마지막

## mixin

- 여러 클래스 계층에서 클래스의 코드를 재사용하는 방법
- ',' 로 여러 클래스의 코드를 사용할 수 있다.

```dart
class Engine {
  int power = 5000;
}

// 다형성을 만족하지 않으므로 Engine을 상속받을 순 없다.
class BMW with Engine { // with 키워드를 사용한다.

}

void main() {
	BMW b = BMW();
  print(b.power); // 5000
}
```

- 다른 언어에서는 composition이라는 개념을 사용한다.
- composition
  - 클래스 간에 포함 관계(composition)를 맺어주는 것
  - 한 클래스의 멤버 변수로 다른 클래스 타입의 참조 변수를 선언하는 것을 의미

## 추상클래스

- 타입을 일치시키기 위한 용도
- 몸체가 없는 메소드를 만들 수 있음

```dart
abstract class Animal {
  void sound();
}

class Fish implements Animal{
  @override
  void sound() { // 해당 메소드를 반드시 정의해야함
    print("뻐끔뻐끔 배고파");
  }
}

void main() {
	Fish fish = Fish();
	fish.sound(); // 뻐끔뻐끔 배고파

	Animal fish = Fish(); // 이렇게도 가능 (동적 바인딩)

	print(fish is Animal); // true
  print(fish.runtimeType); // Fish
}
```

## Collection

```dart

void main() {

  // List
  List<int> nums = [1,2,3,4];
  print(nums[2]); // 3

  var nums2 = [3,4,5]; // 타입추론 가능
  print(nums2[0]); // 3

  // 이렇게 선언할 수도 있음 (공식문서 권장) -> 컬렉션 리터럴
  var mList = []; // list
  var mMap = <String, String>{};
  var mSet = <int>{}; // set

  // Map
  Map<String, dynamic> user = {
    "id": 1,
    "username" : "cos"
  };

}
```

## 반복문

```dart

void main() {
  // 반복문 기본 형태
  for(int i=0;i<4;i++){
    print(nums[i]);
  }

  // map() -> 값을 하나씩 변형해서 리턴할 때
  var sushi = ["새우초밥", "광어초밥", "연어초밥"];
  var sushiChange = sushi.map((i) => "간장과 $i").toList(); // return
  print(sushiChange); // () Iterable, [] List

  // where -> 필터링할 때
  var findSushi = sushi.where((i)=> i!="광어초밥").toList();
  print(findSushi);

}
```

## 얕은 복사 / 깊은 복사

### 얕은 복사 (Shallow Copy)

- 메모리 주소를 공유함 → 값을 변경하면 복사한 리스트에도 반영됨

```dart
void main() {
	var list1 = [1,2,3,4];
	var list2 = list1;

	list1[0] = 10;

	print(list1); // [10, 2, 3, 4]
	print(list2); // [10, 2, 3, 4]
}
```

### 깊은 복사 (Deep Copy)

- 아예 값 전체를 가져온다. → 이때 메모리 상의 주소도 바뀜

```dart
void main() {
	// 얕은 복사
	var list1 = [1,2,3,4];
	var list2 = list1;

	list1[0] = 10;

	print(list1); // [10, 2, 3, 4]
	print(list2); // [10, 2, 3, 4]

	// 깊은 복사
	var list3 = [...list1];

	list1[0] = 100;

	print(list1); // [100, 2, 3, 4]
	print(list3); // [10, 2, 3, 4]
}
```

- Object를 들고 있으면 깊은 복사가 힘들다. → 주소가 spread 되기 때문
- list와 testList가 가지고 있는 내부 Map<String, int>의 주소는 동일함

```dart
void main() {
  var list = [{"id" : 1}, {"id": 2}];
  var testList = [...list];
  var newList = list.map((i)=>{...i}).toList();

  list[0]["id"] = 10;

  print(list); // [{id: 10}, {id: 2}]
  print(testList); // [{id: 10}, {id: 2}]
  print(newList); // [{id: 1}, {id: 2}]

  print(list[0].hashCode); // 69610927
  print(testList[0].hashCode); // 69610927
  print(newList[0].hashCode); // 201171375
}
```

## final과 const

- 한번 값을 정하면 변경할 수 없다는 점은 동일하다.

### final

- 실행 중에 값이 결정됨 (런타임 시)

### const

- 컴파일 시 값이 결정됨

- 프로그램이 실행될 때의 시간을 남기고 싶다고 가정할 때,
  const는 컴파일 시에 값이 결정되므로 error가 발생한다.

```dart
void main() {
	final log1 = DateTime.now();
	const log2 = DateTime.now(); // error
}
```

## Null Safety

- Flutter 2.0부터 도입
- null로 인해 예상치 못하고 의도하지 않은 예외를 대비하는 것
- null을 허용하는 것(Nullable Type)과 허용하지 않는 것(Non-Nullable Type)으로 나뉨
- 기본적으로 모든 데이터 타입은 null을 허용하지 않는 타입
- `데이터 타입` 뒤에 ‘?’을 붙여 nullable 타입임을 명시한다.
  ~~코틀린은 변수 뒤에 붙이는거라서 헷갈린다..^^~~

```dart
class Dog{
  late String name;
  late int age;
  late String? nickname;

  Dog(String name, int age, String? nickname){
    this.name = name;
    this.age = age;
    this.nickname = nickname ?? "없음";
  }

}
void main() {
  Dog happy = Dog("happy", 1, null);
  Dog toto = Dog("toto", 3, "또또");

  print("${happy.name}는 ${happy.age}살이며 별명은 ${happy.nickname}이다.");
	// happy는 1살이며 별명은 없음이다.
  print("${toto.name}는 ${toto.age}살이며 별명은 ${toto.nickname}이다.");
	// toto는 3살이며 별명은 또또이다.
}
```

- `late` : 필드가 참조되기 전 반드시 할당됨을 의미한다.
- `??` : null 대체 연산자. 해당 변수가 null일 경우 지정된 값을 반환하고 null이 아닐경우 해당 값 반환

# References

[이지업클래스 | 모두를 위한 온라인 IT CLASS](https://easyupclass.e-itwill.com/course/course_view.jsp?id=28&rtype=0&ch=course)

[[Dart] Collection : List & Set & Map](https://joycestudios.tistory.com/70)

[Dart mixin 이란?](https://paulaner80.tistory.com/entry/Dart-mixin-%EC%9D%B4%EB%9E%80-1)

[[Java] Inheritance (vs. composition)](https://velog.io/@janeljs/Java-Inheritance)

[prefer_collection_literals](https://dart-lang.github.io/linter/lints/prefer_collection_literals.html)

[얕은 복사(shallow copy), 깊은 복사(deep copy)](https://nyaongnyaong.com/186)

[Dart final과 const의 차이](https://velog.io/@ruinak_4127/Dart-final%EA%B3%BC-const%EC%9D%98-%EC%B0%A8%EC%9D%B4)

[null-safety](https://cafepurple.tistory.com/72)
