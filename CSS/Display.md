# [Display](https://developer.mozilla.org/ko/docs/Web/CSS/display)
CSS 속성 중 display는 어떠한 요소에 대한 레이아웃을 결정합니다.   
외부적으로는 이 요소가 어디에, 어떻게, 얼마 만큼의 공간을 차지하며 배치될 지를 결정하고, 내부적으로는 자식 요소들의 레이아웃 또한 결정합니다.

<br/>

## 기본적인 속성
- display : block
- display : inline
- display : inline-block
- display : none

<br/>

## display : block
div 태그, p 태그, h 태그, li 태그 등이 이에 해당됩니다.

항상 새로운 라인에 요소가 배치되고 화면 크기의 전체 가로폭을 영역으로 차지합니다.    
width, height 지정을 통해 가로 세로폭을 조절할 수 있습니다.   

`ex)`
```
<style>
.block1{ width: 300px; border: 3px solid #333 }
.block2{ width: 200px; border: 3px solid #999 }
</style>

<div class="block1">1</div>
<div class="block2">2</div>
hello
```
![image](https://user-images.githubusercontent.com/90454621/235596436-b5f263dd-f1bb-4fc9-9bb5-2216ff230ad6.png)

<br/>

## display : inline
span 태그, b 태그, i 태그, a 태그 등이 이에 해당됩니다.

block 과 달리 줄 바꿈이 되지 않고, width와 height를 지정 할 수 없습니다.   
문서에서 특정 부분에 색상을 입힌다고 다음에 나오는 글이 줄바꿈 되지 않듯이 inline 요소 뒤에 나오는 태그 또한 줄바꿈 되지 않고 바로 오른쪽에 표시됩니다.   

`ex)`
```
<style>
.inline1{
	background: #09c;
}
.inline2{
	width: 200px; /* 이 값은 무시됩니다 */
	border: 3px solid #999;
}
</style>

<p>
	Lorem ipsum dolor sit amet, <span class="inline1">consectetur adipiscing elit</span>,
	sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
	Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
	Duis aute irure dolor in <span class="inline2">reprehenderit</span>
	in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
	Excepteur sint occaecat cupidatat non proident,
	sunt in culpa qui officia deserunt mollit anim id est laborum.
</p>
```
![image](https://user-images.githubusercontent.com/90454621/235597122-2b4668f8-8de5-4146-8b00-2e4cf885ec54.png)

<br/>

## display : inline-block
block과 inline의 중간 형태라고 볼 수 있는데, 줄 바꿈이 되지 않지만 크기를 지정 할 수 있습니다.   
Internet Explorer 7 이하에서는 사용할 수 없습니다.   

`ex)`
```
<style>
.inline-block1{
	display: inline-block;
	background: #09c;
	height: 45px;
	/* 원래 inline 요소의 높이는 글자(폰트)의 높이를 바탕으로 설정되지만,
	inline-block을 이용하면 임의로 높이 또한 설정을 할 수 있습니다. */
}
.inline-block2{
	display: inline-block;
	width: 200px; /* 이 값은 이제 정상 작동합니다 */
	border: 3px solid #999;
}
</style>

<p>
	Lorem ipsum dolor sit amet, <span class="inline-block1">consectetur adipiscing elit</span>,
	sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
	Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
	Duis aute irure dolor in <span class="inline-block2">reprehenderit</span>
	in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
	Excepteur sint occaecat cupidatat non proident,
	sunt in culpa qui officia deserunt mollit anim id est laborum.
</p>
```
![image](https://user-images.githubusercontent.com/90454621/235597446-969920d0-c700-462d-a585-b1209307ab0c.png)

<br/>

## display : none
요소를 렌더링하지 않도록 설정합니다.   
visibility 속성을 hidden으로 설정한 것과 달리, 영역도 차지하지 않습니다.   

`ex)`
```
<style>
.display-none{ display: none }
.invisible{ visibility: hidden }
</style>

<div class="display-none">1</div>
<div>2</div>

<div class="invisible">3</div>
<div>4</div>
```
![image](https://user-images.githubusercontent.com/90454621/235597790-cacb6588-b058-4697-a66b-a9ce19f0fe40.png)

<br/>

## 참고
https://ofcourse.kr/css-course/display-%EC%86%8D%EC%84%B1

https://mber.tistory.com/42
