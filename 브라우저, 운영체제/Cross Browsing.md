# Cross Browsing(크로스 브라우징)
웹 페이지 제작 시에 모든 브라우저에서 깨지지 않고 의도한 대로 올바르게(호환성) 나오게 하는 작업을 말합니다.

HTML5, CSS, JavaScript 작성 시 W3C의 웹 규격에 맞는 코딩을 함으로써 어느 브라우저, 기기에서 사이트가 의도된 대로 보여지고 작동되는 기법입니다.

<br>

## 💡 크로스 브라우징이 필요한 이유
> 브라우저마다 렌더링 엔진이 다르기 때문입니다.

> 렌더링 엔진이란
페이지를 렌더할 때에 실질적으로 페이지를 작업해주는 브라우저의 엔진들을 의미합니다.
엔진의 종류로는 트라이던트, 게코, 웹킷, 프레스토, 블링크, 듀얼 엔진 등 다양합니다.
각 엔진은 사용되는 브라우저의 버전 혹은 지원하는 회사(ex.구글,MS,애플...)등에 따라 다르게 사용됩니다.

- 작동하지 않은 HTML5, JavaScript 코드가 존재
- 해석하지 못하는 CSS 코드 존재
- 브라우저 버그들이 존재 
- 브라우저 자체적인 CSS 스타일

<br>

## 💡 그렇다면 어떻게 대응해야 하는가?
타겟이 되는 (가장 점유율이 높은) 브라우저부터 맞추는 것이 좋습니다.
보통 기준이 되는 %이하인 브라우저는 지원에서 제외하기도 합니다.

각 나라별로 사용자들의 순위가 다르며 모바일과 데스크탑 등 다양한 환경에 따라 점유율 또한 달라집니다.
그래서 프로젝트 진행시에 타겟과 정책을 잘 잡아야 하며,
아래와 같은 방법으로 크로스 브라우징 작업을 진행할 수 있습니다.

<br>

### 1. 호환성 있는 HTML, CSS, JavaScript 작성
크로스 브라우징을 위해서는 호환성 있는 HTML, CSS, JavaScript 코드를 작성해야 합니다.
이를 위해서는 W3C에서 권장하는 웹 표준을 준수하고, 브라우저마다 지원하는 기능을 고려하여 코드를 작성해야 합니다.

[캔아이유즈](https://caniuse.com) 를 통해 각 브라우저의 호환성을 검토

### 2. CSS reset
각 브라우저마다 기본적으로 적용되는 CSS 스타일이 다르기 때문에, 이를 초기화하고 일관된 스타일을 적용해야 합니다. 
이를 위해서는 CSS reset을 사용하거나, 일관된 스타일을 적용하는 CSS 프레임워크를 사용할 수 있습니다.

### 3. 브라우저 버그 대응
브라우저마다 버그가 존재할 수 있으므로, 이를 대응해야 합니다. 
이를 위해서는 브라우저마다 발생할 수 있는 버그를 파악하고, 해당 버그에 대한 대응 방법을 찾아서 코드를 수정해야 합니다.

### 4. 브라우저 테스트
크로스 브라우징을 위해서는 브라우저마다 웹 페이지가 정상적으로 동작하는지 테스트해야 합니다. 
이를 위해서는 다양한 브라우저와 운영체제를 사용하여 테스트를 진행하거나, 크로스 브라우징 테스트 툴을 사용할 수 있습니다.

### 5. polyfill 사용
호환성 있는 코드를 작성하더라도, 브라우저마다 지원하지 않는 기능이 있을 수 있습니다. 
이를 해결하기 위해서는 폴리필(polyfill)을 사용하여 브라우저에서 지원하지 않는 기능을 구현할 수 있습니다.

> 폴리필(Polyfill)은 브라우저에서 지원하지 않는 기능을 대신하는 코드로, 기존 코드에 추가하여 지원하지 않는 기능을 구현할 수 있습니다. 
이를 통해 다양한 브라우저에서 동일한 기능을 제공할 수 있습니다.

 

