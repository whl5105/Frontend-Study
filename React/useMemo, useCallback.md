# useMemo 와 useCallback
React는 컴포넌트를 렌더링 한 뒤, 이전 렌더된 결과와 비교하여 Dom 업데이트를 결정합니다.
이 때 재렌더가 필요없는 컴포넌트의 렌더를 방지하여 이 업데이트 속도를 높일 수 있는 방법들이 있는데 정확한 역할과 차이점을 구분하기 위해 정리해 보고자 합니다.

<br>

## 💡 Memoization
메모이제이션은 기존에 수행한 연산의 결과값을 어딘가에 저장해두고 동일한 입력이 들어오면 재활용하는 프로그래밍 기법입니다.
이것을 적절하게 활용하면 중복 연산을 피할 수 있기 때문에 메모리를 조금 더 쓰더라도 애플리케이션의 성능을 최적화 할 수 있습니다.

<br>

# useMemo
useMemo는 메모이제이션된 [값]()을 반환하는 함수입니다.

```javascript
useMemo(() => fn, [deps]) 
```
여기서 deps로 지정된 값이 변하게 된다면 () => fn 함수를 실행하고, 그 함수의 반환 값을 반환해줍니다.
deps는 dependency의 약어로, 의존성을 뜻하며 useMemo가 이 deps에 의존하고 있다는 것을 말합니다.

<br>

```javascript
import React, { useState, useCallback, useMemo } from "react";

export default function App() {
  const [ex, setEx] = useState(0);
  const [why, setWhy] = useState(0);

  // useMemo 사용하기
  useMemo(() => {console.log(ex)}, [ex]);

  // 두 개의 버튼을 설정했다. X버튼만이 ex를 변화시킨다.
  return (
    <>
      <button onClick={() => setEx((curr) => (curr + 1))}>X</button>
      <button onClick={() => setWhy((curr2) => (curr2 + 1))}>Y</button>
    </>
  );
}
```
한 가지 예로 위와 같이 useMemo를 사용할 수 있습니다.

여기서 X라는 버튼을 클릭했을 때 setEx에 의해서 ex의 값을 1씩 증가시키는데, 
ex의 값이 변하기 때문에 useMemo에서  의존성으로 등록한 ex가 변화된 것을 감지해 지정한 함수가 실행되고, console.log로 인해 ex값이 출력되게 됩니다.

<br>

# useCallback
useCallback은 메모이제이션 된 [함수]()를 반환하는 특징을 가지고 있습니다.

```javascript
useCallback(fn, [deps]) 
```
useCallback 또한 deps, 의존성이 있는 값이 변하면 fn에 등록한 함수를 반환하는 기능을 가지고 있습니다.

<br>

```javascript
useMemo(() => console.log(), [test])
const memoizedCallback = useCallback(() => console.log(), [test])
```
일단은 useMemo와 useCallback의 모양은 위와 같습니다.
useCallback이 함수를 반환하기 때문에 그 함수를 가지는 const 변수에 초기화하는 것이 일반적인 모양입니다.

useMemo같은 경우는 deps값이 변하면 이 함수를 실행해라! 라는 느낌으로 활용이 가능한데,
useCallback은 어떨 때 사용해야 할까요?
useCallback 사용처는 아래와 같습니다.

<br>

## 1) 자식 컴포넌트에 props로 함수를 전달하는 경우
먼저 함수는 값이 아닌 참조로 비교된다는 점을 알고 있어야 합니다.
```javascript
const functionOne = function() {
  return 5;
};
const functionTwo = function() {
  return 5;
};
// 서로의 참조가 다르기 때문에 false
console.log(functionOne === functionTwo);
```
동일한 값을 반환하지만 참조가 다르기 때문에 false가 나옵니다.
위와 같이 컴포넌트에서 특정 함수를 정의할 경우 각각의 함수들은 모두 고유한 함수가 됩니다.
이런 고유한 함수가 생성될 경우, 부모를 통해 props에 함수를 전달받는 자식 컴포넌트에서는 props가 변경되었다고 판단해 리렌더링이 발생하게 됩니다.

<br>

```javascript
// 🚫
function App() {
  const [name, setName] = useState('');
  const onSave = () => {};

  return (
    <div className="App">
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <Profile onSave={onSave} />
    </div>
  );
}
```
useCallback을 사용하지 않을 경우, name이 변경되어 리렌더링이 발생하면 onSave함수가 새로 만들어지고, Profile 컴포넌트의 props로 onSave함수가 새로 전달되게 됩니다.
이때 Profile 컴포넌트에서 useMemo를 사용해도 이전 onSave와 이후 onSave가 같은 값을 반환하지만 참조가 다른 함수가 되어버리기 때문에 리렌더링이 일어나게 됩니다.

<br>

```javascript
// ✅
import React, { useCallback, useState } from 'react';
import Profile from './Profile';


function App() {
  const [name, setName] = useState('');
  const onSave = useCallback(() => {
    console.log(name);
  }, [name]);

  return (
    <div className="App">
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <Profile onSave={onSave} />
    </div>
  );
}
```
useCallback을 사용해서 onSave라는 함수를 재사용하는 것으로 자식 컴포넌트의 리렌더링을 방지할 수 있습니다.

<br>

## 2) 외부에서 값을 가져오는 API를 호출하는 경우

```javascript
// 🚫
import React, { useState, useEffect } from "react";

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = () =>
    fetch(`https://your-api.com/users/${userId}`)
      .then((response) => response.json())
      .then(({ user }) => user);

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```
위의 코드는 fetchUser 함수가 변경될 때만 외부에서 api를 가져와 useEffect가 실행됩니다.

사실 위 코드는 정상적인 코드가 아닙니다.
Profile이라는 컴포넌트가 리렌더링이 발생할 경우 fetchUser 함수에는 새로운 함수가 할당되게 됩니다. 그러면 useEffect()함수가 호출되어 user 상태값이 바뀌고, state 값이 바뀌었기 때문에 다시 리렌더링이 일어납니다.
무한루프에 빠져버리게 됩니다.

이때 useCallback을 사용할 경우 fetchUser 함수의 참조값을 동일하게 유지시킬 수 있습니다.

<br>

```javascript
// ✅
import React, { useState, useEffect } from "react";

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = useCallback(
    () =>
      fetch(`https://your-api.com/users/${userId}`)
        .then((response) => response.json())
        .then(({ user }) => user),
    [userId]
  );

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```
api의 옵션으로 사용되는 userId가 변동될 때만 fetchUser에 새로운 함수가 할당되도록 설정하고, 
그것이 아니면 동일한 함수가 실행되게 되서 무한 루프에 빠지지 않도록 할 수 있습니다.

[참고](https://narup.tistory.com/273)
