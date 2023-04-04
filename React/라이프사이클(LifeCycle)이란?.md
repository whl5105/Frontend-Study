### **컴포넌트 생명주기( React LifeCycle) 이란?**

개발을 할때 어떤 타이밍에 어떤 순차적으로 동작들이 일어나는가 , 즉 **화면에 컴포넌트가 나타났다가 사라지기 까지의 모든 과정** 을 라이프 사이클이라 하며 생명주기를 통해 불필요한 업데이트를 방지할 수 있다

<br/>

**클래스형 컴포넌트와 함수형 컴포넌트의 비교**
| **분류** | **클래스형 컴포넌트** | **함수형 컴포넌트** |
|--|--|--|
|Mounting| constructor() |  |
|Mounting| render() |return() |
|Mounting| ComponenDidMount() |useEffect()|
|Updating|  componentDidUpdate() | useEffect()|
|UnMounting|  componentWillUnmount() | useEffect()|


<br/>


**클래스형 컴포넌트**의 경우 특정 라이프 사이클 메소드를 사용하며 **함수형 컴포넌트**에서는 Hook을 사용하여  클래스형 component 의  lifeCycle처럼 관리가 가능하다


## **클래스형 Component** **Life Cycle**
![](https://blog.kakaocdn.net/dn/mNLWI/btrmmd4U124/IlHt7FyQHzJk1QNieFKWx1/img.png)
그때그때 어떤 변경에 따라 그려질때 마다 자기가 선언해놓은 메소드를 사용한다.

**constructor()**
	- 컴포넌트가 마운트되기 전에 호출
	- 메서드를 바인딩하거나 state를 초기화하는 작업이 없다면, 해당 React 컴포넌트에는 생성자를 구현하지 않아도 된다
  
**render()**
	- 클래스 컴포넌트에서 반드시 구현돼야하는 유일한 메서드
	- React.Component의 하위 class에서 반드시 정의해야 하는 메서드
  
**componentDidMount()** 
	-  컴포넌트가 화면에 나타나는 것을 마운트(Mount)한다고 표현한다.
	- 첫 렌더링 후에 호출 되는 함수
  
 **componentDidUpdate**(prevProps, prevState, snapshot)
	-   리렌더링을 완료한 후 실행되는 함수
  
**componentWillUnmount()**
 - 컴포넌트가 사라지기 바로 직전에 호출

<br/>

### **Mounting (생성)**
컴포넌트의 인스턴스가 생성되어 DOM 상에 삽입될 때에 순서대로 호출이 되는 메서드

constructor() > render() > componentDidMount()

### **Updating(state값이 변경될때)**
props 또는 state가 변경되면 갱신이 발생되며 순서대로 호출이 되는 메서드

render() > componentDidUpdate()

### **UnMounting (컴포넌트가 사라질때)**
컴포넌트가 DOM 상에서 제거될 때에 호출되는 메서드

componentWillUnmount()

<br/>

**Class Component Life Cycle code**
  ```jsx  
import React from "react";

// 클래스형 컴포넌트
class LifecycleEx extends React.Component {
  // constructor: 생성자 함수 - 초기값의 설정
  constructor(props) {
    super(props);
    this.state = {cat_name: "나비",};
    console.log("in constructor!");
  }

  changeCatName = () => {
    //state값 변경 
    this.setState({ cat_name: "바둑이" });
    console.log("고양이 이름을 바꾼다!");
  };

  //componentDidMount() 
  componentDidMount() {
    console.log("in componentDidMount!");
  }

  //componentDidUpdate
  componentDidUpdate(prevProps, prevState) {
    console.log(prevProps, prevState);
    console.log("in componentDidUpdate!");
  }

  // componentWillUnmount
  componentWillUnmount() {
    console.log("in componentWillUnmount!");
  }

  //render
  render() {
    console.log("in render!");
    return (
      <div>
        <h1>제 고양이 이름은 {this.state.cat_name}입니다.</h1>
        <button onClick={this.changeCatName}>고양이 이름 바꾸기</button>
      </div>
    );
  }
}

export default LifecycleEx;
```


## **함수형 Component** **Life Cycle**
React Hook에서는 useEffect를 통해 react클래스의 componentDidMount나 componentDidUpdate, componentWillUnmount와 같은 목적으로lifeCycle를 관리한다.

![](https://blog.kakaocdn.net/dn/bF6rTe/btrEvNPPvFs/kfuXlK3dGF4bJUpKXQcjH1/img.png)

**useEffect()** 
- 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook , class 컴포넌트의 componentDidMount와 componentDidUpdate,componentWillUnmount 처럼 사용이 가능

**cleanup()**
-  useEffect 에 대한 뒷정리를 해주는 메소드
- deps 가 비어있는 경우에는 컴포넌트가 사라질 때 cleanup 함수가 호출된다.


#### **useEffect()**
```jsx
useEffect(() => { },[]);
```

#### **useEffect() 를 사용하여 클래스 컴포넌트 라이프 사이클 처럼 구현 **

```jsx
useEffect(() => { //componentDidMount :첫 렌더링 후 실행
    	            //componentDidUpdate :리렌더링을 완료한 후 실행 
  return function cleanup() {
                 // componentWillUnmount :컴포넌트가 사라지기 바로 직전에 호출
  };
});
```
useEffect 에서는 함수를 반환 할 수 있는데 이를  **cleanup**  함수라고 부른다

-   useEffect return 함수 == componentWillUnmount
