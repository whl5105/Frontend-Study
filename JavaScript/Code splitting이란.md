## Code splitting(코드분할) 이란 

[코드분할은](https://developer.mozilla.org/ko/docs/Glossary/Code_splitting) 번들한 여러 코드 혹은 컴포넌트를 분리하는 것입니다. 이렇게하면 필요에 따라 특정한 컴포넌트만 로딩하거나, 병렬로 로딩할 수 있습니다.

싱글페이지 어플리케이션의 단점은 자바스크립트 번들 파일에 어플리케이션에 대한 모든 로직을 불러와서, 규모가 커지면 용량이 커지기 때문에, 로딩속도가 지연 될 수 있습니다. 

코드분할을 통해 큰 파일을 다운로드하지 않도록 스크립트를 작게 여러 파일로 분할할 수 있습니다. 

그렇게하면 화면 로딩할 때 필요한 기능은 바로 다운로드할 수 있으며, 추가 스크립트는 화면이나 애플리케이션 상호 작용시에 지연 로딩해서 기능 향상할 수 있습니다. 

코드 총량은 같지만(파일 숫자나 용량은 늘어납니다.), 초기 로딩에 필요한 코드는 적어집니다.


**App**
```js
// app.js
import { add } from './math.js';

console.log(add(16, 26)); // 42
```
```js
// math.js
export function add(a, b) {
  return a + b;
}
```
**Bundle**
```js
function add(a, b) {
  return a + b;
}

console.log(add(16, 26)); // 42 a + b;
```
<hr/>

### import() : 비동기적으로 코드 불러오기 
- 코드 분할을 도입하는 가장 좋은 방법은 동적 import() 문법을 사용하는 방법입니다.

**Before**
```js
import { add } from './math';

console.log(add(16, 26));
```

**After**
```js
import("./math").then(math => {
  console.log(math.add(16, 26));
});
```
- Webpack이 해당 구문을 만나게 되면 앱의 코드를 분할합니다. Create React App을 사용하고 있다면 이미 Webpack이 구성이 되어 있기 때문에 즉시 사용할 수 있습니다. Next.js 역시 지원합니다.

<hr/>

### [React.lazy](https://react.dev/reference/react/lazy#usage)
- React.lazy 함수를 사용하면 동적 import를 사용해서 컴포넌트를 렌더링 할 수 있습니다.
Before

```js
import MarkdownPreview from './MarkdownPreview';
```

After
```js
import { lazy } from 'react';

const MarkdownPreview = lazy(() => import('./MarkdownPreview.js'));
```
- 처음 렌더링 될 때 MarkdownPreview 포함한 번들을 자동으로 불러옵니다.
- lazy 컴포넌트는 Suspense 컴포넌트 하위에서 렌더링되어야 하며, Suspense는 lazy 컴포넌트가 로드되길 기다리는 동안 로딩 화면과 같은 예비 컨텐츠를 보여줄 수 있게 해줍니다.
- fallback prop은 컴포넌트가 로드될 때까지 기다리는 동안 렌더링하려는 React 엘리먼트를 받아들입니다.
```js
import React, { Suspense } from 'react';
import Spinner from './Spinner';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<Spinner>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </div>
  );
}

```


<hr/>

참고


https://zereight.tistory.com/969

https://velopert.com/3421

https://webpack.kr/guides/code-splitting/

https://create-react-app.dev/docs/code-splitting/

https://hoons-up.tistory.com/63