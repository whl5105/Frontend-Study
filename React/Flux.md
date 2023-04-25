# Flux
Flux는 데이터의 흐름과 변화를 관리하기 위한 애플리케이션 아키택처 패턴입니다. 기존 MVC 모델의 단점을 보완하기 위해 페이스북에서 발표한 아키텍처입니다.

<br/>

## MVC 패턴이란?
MVC : Model/ View/ Controller

![images_aeong98_post_2c86077a-0a05-4302-86a6-e0d692b32299_image](https://user-images.githubusercontent.com/113877276/231186858-8f8a5e58-9f9f-4c24-bca3-10b70905ccfa.png)

- Controller는 Model의 데이터를 조회하거나 업데이트 하는 역할
- Model이 업데이트 되면, View는 화면에 반영
- View가 Model을 업데이트 할 수 있음
- 업데이트 된 View가 다른 Model을 업데이트 한다면 또 다른 View가 업데이트 될 수 있음

<br/>

> 💡 MVC 에서는 어플리케이션이 복잡해질수록 양방향 데이터 흐름이 복잡해지고 버그가 많이 발생하게 됩니다.

<br/>

## Flux
![img](https://user-images.githubusercontent.com/113877276/231188398-01de5c5b-7d01-4a37-92f4-3688761758b6.png)

Flux는 단방향으로 데이터가 흐르게 됩니다.

데이터 흐름은 항상 Dispatcher 에서 Store로, Store에서 View로 View에서는 Action 을 통해 Dispatcher 로 데이터가 흐르게 됩니다. 

이런 단방향 데이터 흐름은 데이터 변화를 훨씬 예측하기 쉽게 만듭니다.

Flux는 크게 Dispatcher, Store, View 세 부분으로 구성됩니다.

<br/>

> Dispatcher

Dispatcher는 Flux의 모든 데이터 흐름을 관리하는 허브 역할을 하는 부분입니다. 
Action 이 발생되면 Dispatcher 로 메시지(액션 또는 객체)가 전달되고, Dispatcher는 Action 을 보고 등록된 콜백 함수를 실행하여 Store에 데이터를 전달합니다. 
Dispatcher 는 전체 어플리케이션에서 한 개의 인스턴스만 사용됩니다. (동기적으로 실행)

> Store

어플리케이션의 모든 상태 변경은 Store에 의해 결정이 됩니다. Dispatcher로부터 메시지를 수신 받기 위해서는 Dispatcher에 콜백함수를 등록해야 합니다.
Store가 변경되면 View에 변경되었다는 사실을 알려줘야 합니다. Store는 싱글톤으로 관리됩니다. 무조건 디스패처를 통해 액션을 보내야만, 데이터 변경이 가능합니다.
  - 싱글톤이란?
  객체의 인스턴스가 오직 1개만 생성되는 패턴. 즉, 인스턴스가 필요할 때, 똑같은 인스턴스를 만들어 내는 것이 아니라, 동일 인스턴스를 사용하게 하는 것. 
  어플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고 그 메모리에 인스턴스를 만들어 사용하는 디자인 패턴입니다. 즉 데이터 공유가 쉽습니다. 
  다른 클래스의 인스턴스들이 접근해서 사용할 수 있습니다.
  
> View

Flux의 View 는 화면에 나타내는 것 뿐만 아니라, 자식 View 로 데이터를 흘려 보내는 뷰 컨트롤러의 역할도 함께 합니다. 
특히 중첩된 뷰 레이어의 최상위 뷰는 스토어에서 데이터를 가져와 이를 자식 뷰로 배분하는 역할을 하고 있기 때문에, 컨트롤러-뷰(controller-view)라고도 부릅니다. 
즉, 자식 뷰에서는 직접 데이터를 가져오는 대신 props 형태로 상위 뷰에서 전달받는 방식을 주로 사용합니다.

뷰는 스토어의 변경 사항을 감지할 수 있는 이벤트 리스너를 스토어에 등록하고, 스토어에 변경 사항이 발생하면 이를 뷰에 반영합니다.

> Action

Dispatcher 에서 콜백함수가 실행 되면 Store가 업데이트 되는데, 이 콜백 함수를 실행 할 때 데이터가 담겨 있는 객체가 인수로 전달 되어야 합니다. 
이 전달되는 객체를 Action 이라고 하는데 Action 은 대체로 액션 생성자 (Action Creator)에서 만들어집니다.

<br/>

## 📍 요약
Flux는 기존 MVC 모델의 단점을 보완하기 위해 페이스북에서 발표한 아키텍처 입니다.
MVC패턴에서는 Model 에 상태변화가 있을 때, View 와 Model 사이에서 무수히 많은 양방향 통신이 발생하게 됩니다. 이는 데이터의 흐름을 예측하기 어렵게 만들고, 많은 버그의 원인이 되었습니다.
따라서 이를 해결하기 위해 나타난 방법이 단방향 데이터 흐름 아키텍처인 Flux 입니다. 
데이터 흐름은 항상 Dispatcher 에서 Store로, Store 에서 View로 View 에서는 Action 을 통해 다시 Dispatcher 로 데이터가 흐르게 됩니다. 
이런 단방향 데이터 흐름은 데이터 변화를 훨씬 예측하기 쉽게 만듭니다.

[참고](https://velog.io/@aeong98/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-Redux-Flux-MVC-%ED%8C%A8%ED%84%B4-%EB%B9%84%EA%B5%90)
