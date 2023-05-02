# TypeScript의 interface와 type alias의 차이점

1.둘 다 타입에 이름을 부여해주는 것이지만 **type alias**는 **모든(any) 타입**에 이름을 달아줄 수 있지만, **interface**는 오직 **객체** 타입에만 가능합니다.

2.interface는 선언적 확장이 가능합니다.

ex)  
![image](https://user-images.githubusercontent.com/90454621/234167812-63a1f736-e062-48d0-b314-7026c54b9044.png)

![image](https://user-images.githubusercontent.com/90454621/234168267-d14230b4-3a41-4b96-b9e2-11c8db75a605.png)

3.interface는 확장할때 속성을 단순히 합성하지만 type alias는 재귀적으로 순회하며 속성을 머지합니다.

ex)   
![image](https://user-images.githubusercontent.com/90454621/234170434-2d3a4e79-bf85-49d2-8f1d-1a0c69849378.png)

![image](https://user-images.githubusercontent.com/90454621/234170985-932e1446-a6b6-47e3-a5f9-32dc9ab26b93.png)


## 결론

프로젝트를 설계하기 전에 type을 쓸지 interface를 쓸지 통일을 하면 좋을 것 같습니다. 객체, type간의 합성등을 고려해 보았을 때 interface를 쓰는 것이 더 나을 것같습니다. 공식문서에서도 특별한 경우를 제외하고는 type보단 interface를 사용하는 것이 더 좋다고 합니다.

## 참고

https://tecoble.techcourse.co.kr/post/2022-11-07-typeAlias-interface/

https://yceffort.kr/2021/03/typescript-interface-vs-type

https://bny9164.tistory.com/48