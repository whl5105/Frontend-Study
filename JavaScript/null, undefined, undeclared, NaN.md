> null, undefined, undeclared, NaN 차이점




### null
- null은 **의도적으로 변수에 null을 할당**하여 값이 없다는 것을 나타냅니다.
- type -> object
```js
let a = null;
console.log(a); // null
console.log(typeof a); //object
```
### undefined (미정의 변수)
- **변수를 선언하고** 값을 할당하기 전의 값이며 변수에 **할당되어 있지 않은 상태**입니다.
- 타입이 결정되지 않은 변수
```js
let b;
console.log(b); //undefined
console.log(typeof b); //undefined 

//// var 선언문의 경우, 호이스팅 되었을 때, 변수 선언과 초기화가 동시에 일어나기 때문에, 변수가 undefined 됩니다
console.log(data); // undefined
const data = 'data';
```
### undeclared(미선언 변수)
- 접근 가능한 스코프에 **변수 선언조차 되어있지 않은 상태**입니다.
- type -> undefined
```js
console.log(b); //ReferenceError: b is not defined 
console.log(typeof b); //undefined 
```

### NaN( Not a Number)
- 표현 불가능한 수치형 결과입니다.이 속성은 값이 유효한 숫자가 아니라는 것을 말하며 컴퓨터로는 표현할 수 없는 숫자값입니다.
```js
let a = NaN;
console.log(a); //NaN

typeof 1 / 0; // NaN
```




<br/>
<br/>
<br/>

[참고1](https://velog.io/@lamda/null%EA%B3%BC-undefined-undeclared-%EA%B7%B8%EB%A6%AC%EA%B3%A0-NaN)