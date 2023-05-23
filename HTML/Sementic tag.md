### Sementic tag란
시맨틱 태그는 의미를 부여한 태그입니다.HTML5에서는 처음 등장했으며 태그들의 이름만으로 문서를 조금 더 쉽게 이해할 수 있습니다 


### 시맨틱 태그 사용의 장점

1. HTML 문서의 가독성과 유지보수
- 만약 모든 태그들을 div로 만들었다고 가정해봅시다. HTML 문서가 길어진다면 어디가 어느 부분인지, 어떤 영역인지 한눈에 파악하기가 힘들어지겠죠. 하지만 시맨틱 태그를 활용하면 유지보수를 할 때나 다른 작업자가 코드를 파악하기가 보다 쉬워집니다.

2. 웹 접근성 시각
- 시맨틱 태그만으로  영역 쉽게 확인할 수 있으며 시각장애인들이 사이트를 사용할 때 사용되는 화면의 텍스트를 읽어주는 스크린 리더기 등을 통해 활용될 수 있습니다.

3. 검색엔진최적화(SEO) 🔍 
검색엔진이 검색을 수행할 때 HTML내의 태그를 분석할 수 있습니다.
또한 태그를 기반우으로 페이지 내 검색 키워드의 선순위를 판단합니다. 따라서 제목은 h1, 중요한 단어는 strong 등 사용하는  의미에 맞는 올바른 태그르 사용하는 것이 중요합니다.

### Sementic tag 예시
![다운로드](https://github.com/whl5105/Frontend-Study/assets/73993670/14c9e2d3-ac73-485c-802a-b67a01689258)
![다운로드](https://github.com/whl5105/Frontend-Study/assets/73993670/e4e9e1cb-7b97-4e58-8a86-34605588d6d1)


```html
<body>
<div id="wrapper">
  <header>
    <nav>
      <ul>
        <li><a href="#">홉</a></li>
        <li><a href="#">장보기</a></li>
      </ul>
    </nav>
  </header>
  <section>
    <h2>이벤트</h2>
    <article class="at1">  
      <h3>이벤트1</h3>
       <p>이벤트1 내용 </p>
    </article>
    <article class="at2"> 
      <h3>이벤트2 </h3>
      <p>이벤트2 내용</p>
     </article>
  </section>
  <aside>
      <img src="images/1.png" alt="">
      <img src="images/2.png" alt="">
      <img src="images/3.png" alt="">
  </aside>
  <footer>
    <p>Copyright 2023 </p>
  </footer>
</div>
</body>
```
### Sementic tag 종류
|태그|설명|
|------|---|
|header|사이트의 머리부분에 사용|
|nav|웹 페이지 메뉴를 만들 때 사용|
|main|메인 콘텐츠를 나타내는데 사용|
|section|제목별로 나눌 수 있는 문서의 콘텐츠 영역을 구성하는 요소|
|article|개별 콘텐츠를 나타내는 요소|
|aside|좌우측의 사이드 영역|
|footer|사이트의 바닥부분, 주로 연락처나 제작자 정보등을 기술하는 부분|
|hgroup|제목과 부제목을 묶어서 나타내는 요소|
|iframe|외부 문서를 나타낼때 사용|
|address|사이트 제작자 정보, 연락처 정보 나타낼때 사용|
|div|콘텐츠를 묶어 시각적 효과를 적용할 때 사용|



<hr/>


[참고1](https://coding-factory.tistory.com/883)
[참고2](https://velog.io/@syoung125/%EC%8B%9C%EB%A7%A8%ED%8B%B1-%ED%83%9C%EA%B7%B8-Semantic-Tag-%EC%9E%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
[참고3](https://sangyeon96.gitbooks.io/do-it-html5-css3/content/Chapter10-2.html)



