# undefined 와 null의 차이

JavaScript에서 `undefined` 와 `null` 은 모두 값이 없음을 나타내는데 사용됩니다. 

그러나 두 값 사이에는 몇 가지 중요한 차이점이 있습니다.

<br/>

## undefined

원시자료형으로서, 변수나 객체의 속성이 값을[ 할당받지 않은 경우에 자동으로 지정되는 값입니다.]() 

예를 들어, 변수를 선언하지만 초기값을 할당하지 않은 경우, 해당 변수의 값은 `undefined` 가 됩니다. 

또한 함수에서 반환값을 지정하지 않은 경우에도 자동으로 `undefined` 가 반환됩니다.

> 자료형 - undefined

```javascript
const word

console.log(word) // undefined
```

```javascript
Boolean(undefined) // false
Number(undefined) // NaN
String(undefined) // 'undefined'

typeof(undefined) // 'undefined'
```

<br/>

## null

원시자료형으로서, [의도적으로]() 값이 없음을 나타내는데 사용됩니다. 

아무것도 참조하고 있지 않다라는 의미가 담겨 있으며 주로 객체를 담을 변수를 초기화할 때 많이 사용합니다.


> 자료형 - object

```javascript
const word = null

console.log(word) // null
```

```javascript
Boolean(null) // false
Number(null) // 0
String(null) // 'null'

typeof(null) // 'object'
```
<br/>

## 차이점

1. 할당
- undefined는 개발자가 의도적으로 할당하기 위한 값이 아닌, 자바스크립트 엔진이 변수를 초기화할 때 사용하는 값이다.
- null은 변수에 값이 없다는 것을 의도적으로 명시할 때 사용하는 값이다.

2. 타입
- undefined - undefined
- null - object

3. 비교
- null과 undefined는 == 연산자로 비교할 때는 true
- === 연산자로 비교할 때는 타입이 다르기 때문에 false
