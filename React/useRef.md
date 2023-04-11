# useRef ?

React 컴포넌트는 기본적으로 내부 상태(state)가 변할 때마다 다시 렌더링이 됩니다. 대부분의 경우에는 상태가 변할 때마다 React 컴포넌트가 함수가 호출되어 화면이 갱신되기를 바랍니다. 하지만 그에 따른 부작용으로 함수 내부의 변수들이 기존에 저장하고 있는 값들을 잃어버리고 초기화하는데, 간혹 다시 렌더링이 되더라도 기존에 참조하고 있던 컴포넌트 함수 내의 값이 그대로 보존되어야 하는 경우가 있습니다. 이때 사용할 수 있는 Hook이 useRef입니다.

useRef 함수는 .current 프로퍼티로 전달된 인자로 초기화된 변경 가능한 ref 객체를 반환합니다. 이 current 속성의 값은 상태를 변경할 때처럼 React 컴포넌트가 다시 렌더링 되지 않습니다. 또한 다시 렌더링 될 때도 마찬가지로 current 값이 유실되지 않습니다.

## useRef의 활용

useRef에 대한 활용 예시를 정리하면 다음과 같습니다.

1. DOM 요소에 접근: useRef는 DOM요소에 접근하는 데 사용할 수 있습니다. useRef로 ref 객체를 생성하면 ref 객체의 현재 속성에 접근하여 DOM요소를 조작할 수 있습니다.
2. 다시 렌더링 되어도 동일한 참조값을 유지하기

대표적으로 많이 사용되는 활용인 DOM 요소에 접근하는 예제입니다.

```javascript
function App() {
  const inputEl = useRef < HTMLInputElement > null;
  const onButtonClick = () => {
    inputEl.current?.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

이 경우 useRef를 사용하여 inputEl이라는 ref 객체를 만듭니다. 그런 다음 inputEL을 ref 속성으로 input 엘리먼트에 전달합니다. 버튼을 클릭하면 onButtonClick 함수가 호출되어 inputEl의 현재 속성을 업데이트하여 입력 요소에 포커스를 맞춥니다.

다시 렌더링 되어도 동일한 참조 값을 유지하는 예제는 다음과 같습니다.

```javascript
const MyComponents = () => {
  const [count, setCount] = useState(0);
  const intervalId = useRef<NodeJS.Timeout>();
  console.log(`렌더링... count: ${count}`);

  const startCounter = () => {
    intervalId.current = setInterval(
      () => setCount((count) => count + 1),
      1000
    );
    console.log(`시작... intervalId: ${intervalId.current}`);
  };

  const stopCounter = () => {
    clearInterval(intervalId.current);
    console.log(`정지... intervalId: ${intervalId.current}`);
  };

  return (
    <>
      <p>자동 카운트: {count}</p>
      <button onClick={startCounter}>시작</button>
      <button onClick={stopCounter}>정지</button>
    </>
  );
};
```

setInterval 함수는 intervalId를 반환합니다. count의 state가 변하면서 리렌더링이 되는 상황에서 이 반환된 Id를 유실되지 않게 useRef에 저장하여 해당 id의 Interval을 clear 할 수 있도록 합니다. 만약 useRef를 사용하지 않고 일반 변수로 선언할 경우, 리렌더링 시에 intervalId의 참조 값이 바뀌어 정지 버튼을 눌러도 카운터가 멈추지 않습니다.
