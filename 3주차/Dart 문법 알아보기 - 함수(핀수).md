# Dart 문법 알아보기2 - 함수

## 함수 method

코드의 재사용을 용이하게 해준다.

### 기본 형태

```dart
리턴타입 함수이름(){
  내용..
}
```

### 매개변수가 있는 함수

```dart
void add(int x, int y){
  int sum = x + y;
  print("$x + $y = $sum");
}
```

### 리턴 값이 있는 함수

```dart
int add (int x, int y){
  return x + y;
}
```
</br>

# 익명함수와 람다 (화살표 함수)

</br>

어떤 행위를 정의하는 함수들이 있다고 생각해보자.

```dart
void run(){
	print("달리기");
}

void study(){
	print("공부하기");
}

..
```

하루의 계획을 세우는 함수 `setTodayPlan()`를 정의해야한다고 생각해보자.

하루의 계획은 매일 매일 달라지는데 

그때마다 해당하는 함수를 만들어 호출하는 것은 너무 비효율적이다.

그리고 그때마다 `setTodayPlan()` 내부는 변경되어야 한다.

```dart
void setTodayPlan(){
	run();
}

void main (){
	setTodayPlan();
}
```
</br>

## 익명함수
</br>

이렇게 호출하는 시점에 어떠한 행위가 결정되어야 한다면

함수를 만들어 호출하는 것보다 익명함수를 사용하는 것이 효율적이다.

```dart
void setTodayPlan(Function makePlan){
	makePlan();
}
```

함수도 `Function` 타입의 객체이기 때문에 함수를 변수에 할당할 수 있다.

또한, 인자로도 제공할 수 있다.

참고 : `var` 는 모든 타입을 넣을 수 있기 때문에 함수도 넣을 수 있다.

</br>

### 익명함수의 형태

</br>

- 리턴 타입과 이름이 없다.
- 함수의 이름이 없어도 실행되는 이유는 makePlan 이라는 이름의 함수가 인자로 넘어가기 때문

```dart
void main () {
	setTodayPlan((){
	    print("친구 만나기");
	});
}
```

 </br>

### 리턴 값이 있는 경우

</br>

```dart
void setTodayPlan(Function makePlan){
		String plan = makePlan();
		print(plan); // 장보기
}

void main () {
		setTodayPlan((){
			return "장보기";
	});
}

```

</br>

## 람다식 (화살표 함수)

</br>

위의 경우처럼 함수가 한줄일 경우에는 람다식을 사용하여 처리할 수도 있다.

화살표 다음이 return 값이 된다.

```dart
void main () {
	setTodayPlan(() => "장보기");
}
```

# References
[이지업클래스 | 모두를 위한 온라인 IT CLASS](https://easyupclass.e-itwill.com/classroom/index.jsp?cuid=2354)

[Dart 익명함수와 화살표 함수](https://velog.io/@ruinak_4127/Dart-%EC%9D%B5%EB%AA%85%ED%95%A8%EC%88%98%EC%99%80-%ED%99%94%EC%82%B4%ED%91%9C-%ED%95%A8%EC%88%98)