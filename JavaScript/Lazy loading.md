# Lazy loading

## Lazy loading이란?

웹 페이지 전체를 불러와서 한 번에 사용자에게 렌더링하는 대신, 필요한 부분만 불러오고 나머지 부분은 사용자가 필요할 때 불러오는 기법이다.

<br>

## 장단점

### 장점

필요한 웹페이지 중 일부만 먼저 로드되기 때문에 로딩 시간이 단축되어 사용자 경험에 유리하고 저장공간이 절약된다.

<br>

### 단점

아직 로드되지 않은 컨텐츠의 부적절한 인덱싱으로 검색 엔진에서 웹사이트의 순위에 영향을 미칠 수 있다.

사진이나 영상처럼 크기가 크거나 사용자에게 바로 보여지지 않는 페이지 등 중요도가 낮은 요소에 사용하는 것이 좋다.

<br>

## 구현 방법

**| img, iframe 태그의 loading 속성**

img, iframe 태그의 loading 속성에 lazy를 사용해서 구현할 수 있다.

```html
<img src="..." loading="lazy" alt="..." />

<iframe src="..." loading="lazy" />
```

<br>

**| IntersectionObserver**

IntersectionObserver를 이용해서 특정 요소가 화면에 노출되었을 때 리소스를 로드하도록 구현할 수 있다.

```javaScript
const config = {
  rootMargin: "0px 0px 50px 0px",
  threshold: 0,
};

let observer = new intersectionObserver(function (entries, self) {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      preloadImage(entry.target);
      self.unobserve(entry.target);
    }
  });
}, config);

const imgs = document.querySelectorAll("[data-src]");

imgs.forEach(img => {
  observer.observe(img);
});
```

<br>

**| React lazy, Suspense**

큰 규모의 React 애플리케이션의 경우 사용자가 첫 페이지를 로드하는 즉시 대규모 단일 JavaScript 번들이 사용자에게 전송되어 페이지 성능을 저하할 수 있다.

React에서 제공하는 lazy 메서드와 Suspense 컴포넌트를 활용할 수 있다.

```javascript
import { Suspense, lazy } from "react";
import Loading from "./Loading.js";

const LazyComponent = lazy(() => import("./LazyComponent.js"));

export default function MyComponent() {
  return (
    <Suspense fallback={<Loading />}>
      <LazyComponent />
    </Suspense>
  );
}
```

<br>

## 참고

- lazy loading

  https://www.sitepoint.com/five-techniques-lazy-load-images-website-performance/

  https://www.stackpath.com/edge-academy/what-is-lazy-loading/

- React lazy https://react.dev/reference/react/lazy

- React suspense https://react.dev/reference/react/Suspense
