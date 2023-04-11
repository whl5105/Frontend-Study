# Props Drilling ?

props drilling은 props를 오로지 하위 컴포넌트로 전달하는 용도로만 쓰이는 컴포넌트들을 거치면서 React Component 트리의 한 부분에서 다른 부분으로 데이터를 전달하는 과정입니다.

즉, props를 통해 데이터를 전달하는 과정에서 중간 컴포넌트는 그 데이터가 필요하지 않음에도 자식 컴포넌트에 전달하기 위해 props를 전달해야하는 과정을 말합니다.

아래는 props drilling의 예시 코드입니다.

```javascript
import React from "react";
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <FirstComponent content="Who needs me?" />
    </div>
  );
}

function FirstComponent({content}) {
  return (
    <div>
      <h3>I am the first component</h3>;
      <SecondComponent content={content} />|
    </div>
  );
}

function SecondComponent({content}) {
  return (
    <div>
      <h3>I am the second component</h3>;
      <ThirdComponent content={content} />
    </div>
  );
}

function ThirdComponent({content}) {
  return (
    <div>
      <h3>I am the third component</h3>;
      <ComponentNeedingProps content={content} />
    </div>
  );
}

function ComponentNeedingProps({content}) {
  return <h3>{content}</h3>;
}
```

`content`는 `App > FirstComponent > SecondComponent > ThirdComponent > ComponentNeedingProps` 순으로 전달합니다.

## 문제점

props drilling은 2~3 단계의 데이터를 통과하는 것은 문제가 되지 않습니다. 하지만 5~10단계 혹은 15단계를 거쳐야하는 drilling이라면 데이터를 추적하기 힘들고, 유지보수도 힘들게 됩니다.

## 해결방법

1. 전역 상태관리 라이브러리 사용

- Redux, Recoil, MobX 등 사용하여 해당 값이 필요한 컴포넌트에서 직접 불러서 사용할 수 있습니다.

2. `children` 활용하기

- `children`은 태그와 태그 사이에 모든 내용을 표시하기 위해 사용되는 특수한 Props입니다. 아래는 `children`을 사용하여 props drilling을 해결한 예시 코드입니다.

```javascript
import React from "react";
import "./styles.css";

function FirstComponent({children}) {
  return (
    <div>
      <h3>I am the first component</h3>
      {children}
    </div>
  );
}

function SecondComponent({children}) {
  return (
    <div>
      <h3>I am the second component</h3>
      {children}
    </div>
  );
}

function ThirdComponent({children}) {
  return (
    <div>
      <h3>I am the third component</h3>
      {children}
    </div>
  );
}

function ComponentNeedingProps({content}) {
  return <h3>{content}</h3>;
}

export default function App() {
  const content = "Who needs me?";
  return (
    <div className="App">
      <FirstComponent>
        <SecondComponent>
          <ThirdComponent>
            <ComponentNeedingProps content={content} />
          </ThirdComponent>
        </SecondComponent>
      </FirstComponent>
    </div>
  );
}
```

출처 : https://javascript.plainenglish.io/how-to-avoid-prop-drilling-in-react-using-component-composition-c42adfcdde1b
