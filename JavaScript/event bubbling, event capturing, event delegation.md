# **이벤트 플로우**

1. capture phase: 상위 요소에서 하위 요소로 이벤트가 전달된다.
2. target phase: 이벤트가 발생한 요소에서 이벤트가 실행된다.
3. bubble phase: 하위 요소에서 상위 요소로 이벤트가 전달된다.

![event flow](https://user-images.githubusercontent.com/110284486/228160062-beaf1fcb-3f81-45d7-a215-d3d2ba460052.png)

<br/>

# **이벤트 캡처링**

이벤트가 상위 요소에서 하위 요소로 전달되는 방식을 말한다.

`addEventListener()` 의 마지막 인자로 `true` 를 전달하면 capture phase 때 해당 이벤트가 실행된다. 기본값은 `false`로 설정되어 있기 때문에 기본적으로 이벤트는 bubble phase 때 실행된다. (예외 有)

 <br/>

# **이벤트 버블링**

이벤트가 하위 요소에서 상위 요소로 전파되는 현상을 말한다.

<br/>

### **예시**

```html
<body>
  <div>
    <button>예시</button>
  </div>
</body>
```

```jsx
document
  .querySelector("button")
  .addEventListener("click", () => console.log("button"));

// 캡처링 때 실행하도록 설정
document
  .querySelector("div")
  .addEventListener("click", () => console.log("div"), true);

document
  .querySelector("body")
  .addEventListener("click", () => console.log("body"));
```

```jsx
// div
// button
// body
```

<br/>

# **이벤트 위임**

이벤트 핸들링 패턴 중 하나로, 요소들의 공통된 상위 엘리먼트에 이벤트 핸들러를 할당하여 여러 하위 요소를 한꺼번에 다룬다.

```jsx
<div onclick={handleOnClick}>
  <button>첫번째</button>
  <button>두번째</button>
  <button>세번째</button>
</div>
```

<br/>

### **장점**

- 엘리먼트를 추가할 때마다 핸들러를 할당하는 코드를 작성할 필요가 없다.
- 엘리먼트를 자유롭게 추가하고 제거할 수 있어 html 구조가 유연해진다.
- 상위 엘리먼트에 하나의 이벤트 핸들러만 추가하면 되기 때문에 코드가 짧아진다.
- 메모리가 절약된다.

<br/>

### **단점**

- 이벤트 위임을 사용하려면 이벤트가 반드시 버블링 되어야 한다.
- 낮은 레벨에 할당한 핸들러엔 `event.stopPropagation()` 을 쓸 수 없다.

<br/>

# **참고**

- [https://www.youtube.com/watch?v=7gKtNC3b_S8](https://www.youtube.com/watch?v=7gKtNC3b_S8)
- [https://ko.javascript.info/event-delegation](https://ko.javascript.info/event-delegation)
