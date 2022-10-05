# Flutter, 그것이 알고싶다

본격 의식의 흐름대로 알아보는 flutter
지금 시작합니다.

</br>

## 🤔 Flutter가 모죠

공식문서에 따르면

> Flutter는 고성능, 고품질의 iOS, Android, 웹 앱을 단일 코드 베이스로 개발할 수 있는 모바일 앱 SDK
> 

위키백과에 따르면

> Flutter (이하 플러터) 는 구글이 출시한 <span style="background-color:#fffd91;">오픈 소스 크로스 플랫폼 GUI 애플리케이션 프레임워크</span>!
안드로이드, iOS, 윈도우즈, 리눅스 및 웹용 애플리케이션과 구글 퓨시아용 앱의 주된 소스 코드로 사용된다.
> 
</br>

# 모바일 앱 개발 방법들

크게 네이티브 앱, 웹 앱, 하이브리드 앱, 크로스 플랫폼 앱으로 나눌 수 있다.(PWA도 있다.)

</br>

## 🤔 크로스 플랫폼이 모죠

크로스 플랫폼 (멀티 플랫폼이라고도 함) 이란 

컴퓨터 프로그램, 운영 체제, 컴퓨터 언어, 프로그래밍 언어, 컴퓨터 소프트웨어 등

여러 종류의 컴퓨터 플랫폼에서 동작할 수 있다는 것을 뜻한다.

크로스 플랫폼 응용 프로그램은 둘 이상의 플랫폼에서 실행할 수 있다.

대표적인 예로 facebook에서 만든 ReactNatvie와 google에서 만든 flutter가 있다.

크로스 플랫폼, 하이브리드 앱..

두가지가 가지는 의미는 비슷해 보여 항상 혼동해서 쓰곤 했는데, 도대체 어떤 차이일까?



</br>

## 🤔 하이브리드 앱은 모죠

네이티브 앱과 웹 앱의 기능을 결합한 것이라고 보면 된다.

주로 웹 앱 기반으로 개발된 앱을 뜻하며,

프레임 워크를 이용해 개발하면 각 OS 별로 웹 앱이 만들어지는 형태를 뜻한다.

JavaScript, HTML 및 CSS 와 같이 

잘 알려진 언어와 프레임 워크를 사용해 

다양한 플랫폼에서 사용할 수 있는 앱을 만들 수 있다.

비용과 시간이 덜 들고 유지보수가 쉽지만

오프라인으로는 동작하지 않고 똑같은 코드를 베이스로 두고 있기 때문에

각 디바이스의 특정 기능을 원활하게 사용할 수 있는건 아니다.


</br>


엄연히 다른 의미를 가졌지만

모바일 앱 개발 방법에 대해 설명할 때는 혼용되어 쓰기도 하는 듯 하다.

그러나 크로스 플랫폼 프레임워크가 플러터를 설명하기엔 더 적합해 보인다.

</br>

# 플러터 주요 특징

## 다트 플랫폼

구글에서 나온 멀티 플랫폼 프로그래밍 언어

```dart
main() {
	print('Hello World!');
}
```

대표적인 특징은 type safe, null safety가 있다.

자세한 것은 다트 문법을 살펴볼 때 알아보도록 하자.

</br>

## Skia 엔진

오픈 소스 2D 그래픽 라이브러리

2005년 11월에 구글에 인수되었고 플러터는 Skia엔진을 통해 렌더링을 한다.

</br>

### Skia 의 특징

1. AOT (Ahead of Time) Complie
    
    프로덕션 모드에서는 사전 컴파일을 통해 네이티브 수준의 성능으로 앱을 구동할 수 있다.
    
2. JIT (Just in Time) Compile
    
    프로그램을 실제 실행하는 시점에 기계어로 번역하는 컴파일 기법
    
    개발 모드에서는 JIT 컴파일 기법을 통해 변경 사항만을 컴파일한다.
    
    이러한 맥락으로 Hot reload 기능 또한 제공하고 있다.
    
</br>

ReactNative 가 bridge를 통해 Native 위젯을 연결(맵핑)하는 것이었다면,

Flutter는 skia 엔진을 통해 해당 위젯을 디바이스에 바로 그려버린다.

</br>

# References

[플러터 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9F%AC%ED%84%B0)


[크로스 플랫폼 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%ED%81%AC%EB%A1%9C%EC%8A%A4_%ED%94%8C%EB%9E%AB%ED%8F%BC)



[모바일 앱 개발 방법들 (네이티브,웹앱,하이브리드,크로스플랫폼,WPA)](https://dalgonakit.tistory.com/165#4.%20%ED%95%98%EC%9D%B4%EB%B8%8C%EB%A6%AC%EB%93%9C%20%EC%95%B1%20(Hybrid%20App))



[네이티브 앱(Native App) vs 하이브리드 앱(Hybrid App) vs 프로그레시브 웹 앱(PWA) - 정의와 장단점 | 하늘네트](https://www.hanl.tech/blog/native-vs-hybrid-vs-pwa/)

[2021년 주목받는 하이브리드 앱 프레임워크 5가지](https://rich-informer.tistory.com/5)


[하이브리드 앱이란? 하이브리드 앱의 정의 및 장/단점](https://post.naver.com/viewer/postView.nhn?volumeNo=6642508&memberNo=33802574)

[기술 개요](https://flutter-ko.dev/docs/resources/technical-overview)

[CH.1 플러터](https://catsbi.oopy.io/dbe067c8-0ff1-484a-ad34-8b9051c0b6d5)

[플러터의 동작 원리](https://www.hanbit.co.kr/media/channel/view.html?cms_code=CMS7432670479)