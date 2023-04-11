# Context API

## context api란?

react는 16.3 버전부터 정식적으로 context api (opens new window)를 지원하고 있습니다. 일반적으로 부모와 자식간 props를 날려 state를 변화시키는 것과는 달리 context api는 컴포넌트 간 간격이 없습니다. 즉, 컴포넌트를 건너띄고 다른 컴포넌트에서 state, function을 사용할 수 있습니다.

<br/>

## 언제 쓰는가
일반적으로 리액트에서 데이터를 전달하는 기본 원칙은 **단방향**성입니다. 그 말은 **부모 컴포넌트에서 자식 컴포넌트 방향으로만 데이터를 전달**할 수 있다는 의미입니다.

단방향성은 애플리케이션의 안전성을 높이고 흐름을 단순화하는데 유용하지만 떄때로 너무 많은 단계를 거쳐서 자식 컴포넌트에 데이터를 전달해야 한다는 문제점을 야기하기도 합니다.

예를들어 5단계 아래에 위치한 자식 컴포넌트에게 데이터를 넘겨야 한다면, 중간에 4개의 컴포넌트는 해당 데이터를 사용하지 않을지라도 props를 계속해서 넘겨줘야하는 문제가 발생하는 것입니다. 또한, 형제 관계나 특정 범위 안에 있는 컴포넌트들에게 데이터를 넘기기 위해서는 더 복잡한 상황이 발생하기도 합니다.

컴포넌트의 구조를 잘 설계하고 합성을 적극적으로 활용해 데이터를 계속해서 넘겨줘야 하는 상황을 안만드는 것이 1옵션이지만, 해당 방법으로 해결이 안될 때는 Context API를 사용할 수 있습니다.

<br/>

## 사용법
### 1.createContext
Context API를 사용하기 위해서는 먼저 공유할 Context를 만들어줘야 합니다. Context는 `createContext` 라는 함수를 통해서 사용할 수 있습니다.
```
const UserContext = createContext(null);
```
- createContext 함수를 호출하면 Context 객체가 리턴됩니다.
- 함수를 호출할 때는 defaultValue를 인자로 전달할 수 있습니다.

이때 defaultValue는 Context Value의 초기값이 아닌, 다른 컴포넌트에서 Context에 접근하려고 하지만 Provider로 감싸져 있지 않은 상황에서 사용될 값을 의미합니다.

<br/>

### 2.Provider
만들어진 Context를 통해서 특정한 값을 전달하기 위해서는 Provider 컴포넌트를 이용해야 합니다.

Context 객체에는 Provider라는 프로퍼티가 있으며 이는 리액트 컴포넌트입니다.

Provider 컴포넌트는 value라는 props을 가지고 있으며, value에 할당된 값을 Provider 컴포넌트 하위에 있는 어떤 컴포넌트든 접근할 수 있게 해주는 기능을 가지고 있습니다.
```
const UserContext = createContext(null);

const user = {name: "mhh"};

<UserContext.Provider value={user}>
	<Child />
</UserContext.Provider>
```

<br/>

### 3.useContext
Class 컴포넌트에서 Context를 통해 공유된 값에 접근하려면, Consumer라는 다소 복잡한 방식을 통해서 접근해야 합니다. 하지만 함수 컴포넌트에서는 useContext라는 내장 Hook을 이용해 Context Value에 접근할 수 있습니다.
```
const UserContext = createContext(null);

const user = {name: "mhh"};

<UserContext.Provider value={user}>
	<Child />
</UserContext.Provider>


function Child() {
	const user = useContext(UserContext);
	
	return <h1>{user.name}</h1>
}
```

<br/>

## Context vs Redux
1. Context 와 Redux 는 같은 일을 하나?

    둘은 다른 도구이며, 다른 목적을 가지고 있다.
2. Context 는 상태관리 도구인가?
    
    아니다. Context API 는 단지 종속성 주입의 한 형태일뿐 아무것도 관리하지 않는다. 상태관리는 일반적으로 useState 와 useReducer 를 통해 일어난다.
3. useReducer 는 Redux 의 대체품인가?
    
    그렇지 않다. 유사한 부분들이 있지만 기능에는 큰 차이가 존재한다.
4. 언제 Context 를 사용해야하나?
    
    props drilling 을 피하고자 할 때
5. 언제 Context 와 useReducer 를 사용해야 하나?
    
    특정 컴포넌트에서 어느정도 복잡한 상태 관리가 필요한경우
6. Redux 는 언제 사용해야하나
- 여러 위치에 많은 양의 상태 값이 존재 할 때
- 업데이트 로직이 복잡 할 때
- 거대한 코드 베이스를 여러 사람이 작업 할 때
- 상태 변경 시각화가 필요 할 때
- 사이드이펙트, 메모이제이션, 데이터 직렬화등 관리를 위해 더 강력한 기능이 필요 할 때

## 참고
https://olaf-go.medium.com/context-api-vs-redux-e8a53df99b8