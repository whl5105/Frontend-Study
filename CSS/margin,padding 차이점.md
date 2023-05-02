
### CSS에서 margin과 padding이란?

![Update css margin vs padding-2](https://user-images.githubusercontent.com/73993670/235619872-50248d6b-06ee-4112-b065-da25e5d7f3c3.jpeg)

**Margin**
- Object와 화면과의 여백(외부여백)
- 주변 요소와 거리를 두기 위한 영역입니다.
**Padding**
- Object 내의 내부여백
- Content와 Border 사이의 여백을 나타낸는 영역이므로  Content 영역이 배경색이나 배경 이미지를 가질 때,  Padding 영역까지도 영향을 미칩니다.



#### Margin과 Padding의 사용법
1. 전체 공통 속성  
- margin : 15px, padding :15px
- 위, 오른쪽, 아래, 왼쪽 모두 같은 값을 나타냅니다.

2. 상하, 좌우 공통 속성
- margin : 15px 20px, padding :15px 20px
- 첫번째 값은 위와 아래 / 두번째 값은 오른쪽과 왼쪽 여백을 의미합니다.

3. 개별 속성 
- margin: 10px 5px 10px 5px, padding: 10px 5px 10px 5px
- 시계방향(위, 오른쪽, 아래, 왼쪽) 순서로 값을 나타냅니다.

5. 공통속성 + 개별 속성 
- margin: 10px 4px 6px 
  (top:10px , right:4px , bottom:6px , left:4px)
- 위, 좌우, 아래 차례로 값을 나타냅니다.


### 주의 사항 
- border 사이즈는 margin 과 padding 사이즈에 속하지 않기 때문에 정확한 의도한 content 사이즈보다 커질 수 있다. 
![스크린샷 2023-05-02 오후 5 37 15](https://user-images.githubusercontent.com/73993670/235619845-db246622-16ed-4d0e-830e-0380af640b80.png)


```html
<div>
  Our height/width box-sizing box.
</div>
```
```css
div {
  border: 5px solid darkblue;
  padding: 10px;
  width: 200px;
  box-sizing: border-box;
  background-color: lightblue;
}
```
  페이지내의 모든 요소에 box-sizing을 border-box 로 지정하고 싶으면 다음 스타일을 사용한다 :  **box-sizing: border-box;**
