# Virtual DOM
Virtual DOM은 웹 어플리케이션에서 DOM 조작을 최적화하는 기술로, 리액트의 주요 특징은 Virtual DOM을 사용하는 것입니다. 

<br/>

## DOM
DOM은 Document Object Model의 약어로, 객체로 문서 구조를 표현하는 방법입니다. 

DOM은 트리 형태로, 특정 노드를 찾아서 수정/제거 하거나 원하는 곳에 삽입할 수 있습니다. 

웹 브라우저는 DOM을 활용하여 객체에 자바스크립트와 CSS를 적용합니다. 

<img src="https://velog.velcdn.com/images/boniteterain/post/7806cb5f-4d29-410d-a3dd-f1ce995fe90b/image.png"/>

<br/>

## Virtual DOM 도입 배경
- HTML은 자체적으로 정적이나, 자바스크립트를 이용하여 동적으로 만들 수 있습니다. 하지만 DOM은 동적 UI에 최적화되어 있지 않다는 문제점이 있습니다.

- 큰 규모의 웹 애플리케이션은 DOM에 직접 접근하여 변화를 주다 보면 성능 이슈가 발생합니다.

- DOM 자체는 빠르지만, 웹 브라우저 단에서 DOM을 조작할때마다 엔진이 웹 페이지를 새로 그리기 때문에, 잦은 업데이트로 성능이 저하될 수 있습니다.

- 개선방안으로, DOM을 최소한으로 조작하여 작업을 처리하는 방식을 들 수 있습니다.

- 리액트는 Virtual DOM 방식을 사용하여 DOM 업데이트를 추상화함으로써 DOM 처리 횟수를 최소화하고 효율적으로 진행합니다.

<br/>

## Virtual DOM
Virtual DOM은 실제 DOM과 동일한 구조를 가지고 있지만, 실제로 브라우저에 렌더링되지 않습니다.

Virtual DOM을 사용하면 실제 DOM에 접근하여 조작하는 대신, 이를 추상화한 자바스크립트 객체를 구성하여 사용합니다. 

DOM의 가벼운 사본과 비슷하다고 볼 수 있습니다. 

<br/>

다음과 같은 세가지 절차로 실제 DOM을 업데이트합니다.

1. 데이터를 업데이트하면 전체 UI를 Virtual DOM에 리렌더링합니다.
2. 이전 Virtual DOM에 있던 내용과 현재 내용을 비교합니다.
3. 바뀐 부분만 실제 DOM에 적용합니다.

<img src="https://velog.velcdn.com/images/boniteterain/post/9f78eb8e-4884-4938-8f00-44df19bbf81f/image.webp"/>

<br/>

> Virtual DOM을 사용한다고 해서 사용하지 않을 때와 비교하여 무조건 빠른 것은 아닙니다. 적절한 곳에 사용해야 리액트가 지닌 진가를 비로소 비로소 발휘할 수 있습니다. 리액트와 Virtual DOM이 언제나 제공할 수 있는 것은 바로 업데이트 처리 간결성입니다. UI를 업데이트하는 과정에서 생기는 복잡함을 모두 해소하고, 더욱 쉽게 업데이트에 접근할 수 있습니다.

<br/>


## 정리
Virtual DOM은 웹 애플리케이션에서 DOM 조작을 최적화하는 기술입니다. Virtual DOM을 사용하면 DOM 조작을 최소화할 수 있어서 브라우저 성능이 향상되고, 애플리케이션의 반응성이 더욱 빨라집니다. 
이러한 이점으로 인해 React와 같은 프론트엔드 라이브러리에서 Virtual DOM을 기본적으로 제공하고 있습니다.
<br/>
