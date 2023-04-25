## ES6(ECMAScript6)는 무엇인가요?

ECMAScript 2015로도 알려져 있는 ECMAScript 6는 ECMAScript 표준의 가장 최신 버전입니다. ES6는 새로운 언어 기능이 포함된 주요 업데이트이며, 2009년도에 표준화된 ES5 이후로 언어 기능에 대한 첫 업데이트이기도 합니다. 현재 주요 JavaScript 엔진들에서 [ES6 기능들을 구현 중](https://kangax.github.io/compat-table/es6/)에 있습니다.

ES6는 아래의 새로운 기능들을 포함하고 있습니다.

- const and let
- Arrow functions(화살표 함수)
- Template Literals(템플릿 리터럴)
- Default parameters(기본 매개 변수)
- Array and object destructing(배열 및 객체 비구조화)
- Import and export(가져오기 및 내보내기)
- Promises(프로미스)
- Rest parameter and Spread operator(나머지 매개 변수 및 확산 연산자)
- Classes(클래스)

## ES6 문법

### const and let

const는 변수 선언을 위한 ES6의 새로운 키워드입니다. const는 var보다 강력하고 일단 사용되면 변수를 다시 할당할 수 없습니다. 즉, 객체와 함께 사용할 때를 제외하고는 **변경 불가능한 변수** 입니다.

이 기능은 선택자를 대상으로 하는 데 매우 유용합니다. 예를 들어 이벤트를 실행하는 단일 단추가 있거나 JavaScript에서 HTML 요소를 선택하려면 var 대신 const를 사용하십시오. 이것은 var가 '호이스팅(hoisting)'이기 때문입니다. 변수를 재할당하지 않으려면 항상 상수를 사용하는 것이 좋습니다.

```
// ES5
var MyBtn = document.getElementById('mybtn');

// ES6
const MyBtn = document.getElementById('mybtn');
```

위의 코드에서 const는 변경되지 않으며 재할당할 수 없습니다. 새로운 값을 제공하려고 하면 오류가 반환됩니다.

let은 새로운 값을 가질 수도 있고 재할당할 수도 있습니다. 변경 가능한 변수가 생성됩니다.

```
let name = '철수';

name = '영희';

console.log(name);
// 출력 => 영희
```

let은 const와 동일하게 모두 블럭 범위라는 점입니다. 즉, 변수는 범위 내에서만 사용할 수 있습니다.

### Arrow functions(화살표 함수)

화살표 함수는 정말 멋지고, 코드를 더 읽기 쉽고, 더 체계적이고, 최신 코드처럼 보이게 합니다.

이 방법을 사용하는 대신:

```
// ES5
function myFunc(name) {
	return '안녕' + name;
}

console.log(myFunc('영희'));

// 출력 => 안녕 영희
```

다음을 사용합니다.

```
// ES6 화살표 함수
const myFunc = (name) => {
	return `안녕 ${name}`;
}

console.log(myFunc('영희')); // 출력 => 안녕 영희

// 또는 화살표를 사용하거나 'return' 키워드를 사용하지 않아도 됩니다
const myFunc = (name) => `안녕 ${name}`;

console.log(myFunc('영희')); // 출력 => 안녕 영희
```

보시다시피 화살표 함수가 더 읽기 쉽고 깔끔해 보입니다! 더 이상 이전 구문을 사용할 필요가 없습니다.

또한, 화살표 함수를 map과 filter, reduce 등 내장 함수와 함께 사용할 수 있습니다.

```
// ES5
const myArrary = ['진수', '영철', '영희', 5];

let arr1 = myArrary.map(function(item) {
	return item;
});

console.log(arr1); // 출력 => (4) ["진수", "영철", "영희", 5]

// ES6
let arr2 = myArrary.map((item) => item);

console.log(arr2); // 출력 => (4) ["진수", "영철", "영희", 5]
```

화살표가 있는 map 함수는 ES5의 map보다 더 선명하고 읽기 쉬워 보입니다. ES6를 사용하면 더 짧고 스마트한 코드를 작성할 수 있습니다. filter와 reduce 같은 동일한 함수를 사용할 수 있습니다.

### Template Literals(템플릿 리터럴)

템플릿 리터럴 또는 템플릿 문자열은 꽤 멋집니다. 문자열을 연결하기 위해 더하기(+) 연산자를 사용할 필요는 없으며, 백틱(\`)을 사용하여 문자열 내에서 변수를 사용할 수도 있습니다.

이전 문법:

```
// ES5
function myFunc1() {
	return '안녕' + name + '너의 나이는' + age + '살 이다!';
}

console.log(myFunc1('영희', 22));
// 출력 => 안녕 영희 너의 나이는 22살 이다!
```

새로운 ES6 문법 사용:

```
// ES6
const myFunc = (name, age) => {
	return `안녕 ${name}, 너의 나이는 ${age}살 이다!`;
};

console.log(myFunc1('영희', 22));
// 출력 => 안녕 영희, 너의 나이는 22살 이다!
```

정말 간단합니다! 이것은 이전 문법과 ES6의 큰 차이입니다. 문자열로 구성할 때 ES6의 리터럴 문자열은 ES5보다 더 체계적이고 잘 구성되어 있습니다.

### Default parameters(기본 매개 변수)

매개 변수를 쓰지 않은 경우 매개 변수가 이미 기본값에 정의되어 있으므로 정의되지 않은 오류가 반환되지 않습니다. 따라서 누락된 매개 변수를 사용하여 함수를 실행할 때 기본 매개 변수 t 값을 사용하고 오류를 반환하지 않습니다!

이 예를 살펴보십시오:

```
const myFunc = (name, age) => {
	return `안녕 ${name} 너의 나이는 ${age}살 이니?`;
};

console.log(myFunc1('영희'));
// 출력 => 안녕 영희 너의 나이는 undefined살 이니?
```

위의 함수는 정의되지 않은 상태로 반환됩니다. 두 번째 매개 변수 age를 지정하는 것을 잊어버렸기 때문입니다.

그러나 기본 매개 변수를 사용하면 정의되지 않은 매개 변수가 반환되지 않고 매개 변수 할당을 잊어버렸을 때 해당 값이 사용됩니다!

```
const myFunc = (name, age = 22) => {
	return `안녕 ${name} 너의 나이는 ${age}살 이니?`;
};

console.log(myFunc1('영희'));
// 출력 => 안녕 영희 너의 나이는 22살 이니?
```

보시다시피 함수는 두 번째 매개 변수를 놓쳤더라도 값을 반환합니다. 이제 기본 파라미터를 사용하여 오류를 미리 처리할 수 있습니다.

### Array and object destructing(배열 및 객체 비구조화)

비구조화를 통해 배열 또는 객체의 값을 새 변수에 더 쉽게 할당할 수 있습니다.

이전 문법:

```
// ES5 문법
const contacts = {
	famillyName: '이',
	name: '영희',
	age: 22
};

let famillyName = contacts.famillyName;
let name = contacts.name;
let myAge = contacts.age;

console.log(famillyName);
console.log(name);
console.log(age);
// 출력
// 이
// 영희
// 22
```

ES6 문법 사용:

```
// ES6 문법
const contacts = {
	famillyName: '이',
	name: '영희',
	age: 22
};

let { famillyName, name, age } = contacts;

console.log(famillyName);
console.log(name);
console.log(age);
// 출력
// 이
// 영희
// 22
```

ES5에서는 각 변수에 각 값을 할당해야합니다. ES6에서는 객체의 속성을 얻기 위해 값을 중괄호 안에 넣습니다.

**참고**: 속성 이름과 동일하지 않은 변수를 할당하면 undefined가 반환됩니다. 예를 들어, 속성의 이름이 name이고 username 변수에 할당하면 undefined를 반환합니다.

우리는 항상 속성의 이름과 동일하게 변수 이름을 지정해야합니다. 그러나 변수의 이름을 바꾸려면 콜론을 :대신 사용할 수 있습니다.

```
// ES6 문법
const contacts = {
	famillyName: '이',
	name: '영희',
	age: 22
};

let { famillyName, name: ontherName, age } = contacts;

console.log(ontherName);
// 영희
```

배열의 경우 객체와 동일한 구문을 사용합니다. 중괄호를 대괄호로 바꾸면됩니다.

```
const arr = ['광희', '지수', '영철', 20];

let [value1, value2, value3] = arr;

console.log(value1);
console.log(value2);
console.log(value3);
// 출력
// 광희
// 지수
// 영철
```

### Import and export(가져오기 및 내보내기)

JavaScript 응용프로그램에서 import 및 export를 사용하면 성능이 향상됩니다. 이를 통해 별도의 재사용 가능한 구성요소를 작성할 수 있습니다.

JavaScript MVC 프레임워크에 익숙한 경우, 대부분의 경우 import 및 export를 사용하여 구성요소를 처리합니다. 그렇다면 실제로 어떻게 작동할까요?

간단합니다! export를 사용하면 다른 JavaScript 구성 요소에 사용할 모듈을 내보낼 수 있습니다. 우리는 그 모듈을 우리의 컴포넌트에 사용하기 위해 가져오기 import를 사용합니다.

예를 들어, 두 개의 파일이 있습니다. 첫 번째 파일은 detailComponent.js이고 두 번째 파일은 homeComponent.js입니다.

detailComponent.js에서는 detail 함수를 내보낼 예정입니다.

```
// ES6
export default function detail(name, age) {
	return `안녕 ${name}, 너의 나이는 ${age}살 이다!`;
}
```

그리고 homeComponent.js에서 이 기능을 사용하려면 import만 사용합니다.

```
import detail from './detailComponent';

console.log(detail('영희', 20));
// 출력 => 안녕 영희, 너의 나이는 20살 이다!
```

둘 이상의 모듈을 가져오려는 경우, 중괄호에 넣기만 하면 됩니다.

```
import { detail, userProfile, getPosts } from './detailComponent';

console.log(detail('영희', 20));
console.log(userProfile);
console.log(getPosts);
```

정말 멋지지 않습니까?!

### Promises(프로미스)

Promise는 ES6의 새로운 특징입니다. 비동기 코드를 쓰는 방법입니다. 예를 들어 API에서 데이터를 가져오거나 실행하는데 시간이 걸리는 함수를 가지고 있을 때 사용할 수 있습니다. Promise는 문제를 더 쉽게 해결할 수 있으므로 첫 번째 Promise를 만들어 봅시다!

```
const myPromise = () => {
	return new Promise((resolve, reject) => {
		resolve('안녕하세요 Promise가 성공적으로 실행했습니다');
	});
};

cosole.log(myPromise());
// Promise {<resolved>: "안녕하세요 Promise가 성공적으로 실행했습니다"}
```

콘솔을 기록하면 Promise가 반환됩니다. 따라서 데이터를 가져온 후 함수를 실행하려면 Promise를 사용합니다. Promise는 두 개의 매개 변수를 사용하며 resolve및 reject 예상 오류를 처리 할 수 있습니다.

**참고** : fetch 함수는 Promise 자체를 반환합니다!

```
const url = 'https://jsonplaceholder.typicode.com/posts';
const getData = (url) => {
	return fetch(url);
};

getData(url).then(data => data.json()).then(result => console.log(result));
```

이제 콘솔을 기록하면 데이터 배열이 반환됩니다.

### Rest parameter and Spread operator(나머지 매개 변수 및 확산 연산자)

Rest parameter는 배열의 인수를 가져오고 새 배열을 반환하는데 사용됩니다.

```
const arr = ['영희', 20, '열성적인 자바스크립트', '안녕', '지수', '어떻게 지내니?'];

// 비구조화를 이용한 값을 얻기
const [ val1, val2, val3, ...rest ] = arr;

const Func = (restOfArr) => {
	return restOfArr.filter((item) => {return item}).join(" ");
};

console.log(Func(rest)); // 안녕 지수 어떻게 지내니?
```

Spread operator는 Rest parameter와 구문이 동일하지만 Spread operator는 인수뿐만 아니라 배열 자체를 가집니다. for 반복문이나 다른 메서드를 사용하는 대신 Spread operator를 사용하여 배열의 값을 가져올 수 있습니다.

```
const arr = ['영희', 20, '열성적인 자바스크립트', '안녕', '지수', '어떻게 지내니?'];

const Func = (...anArray) => {
	return anArray;
};

console.log(Func(arr));
// 출력 => ["영희", 20, "열성적인 자바스크립트", "안녕", "지수", "어떻게 지내니?"]
```

### Classes(클래스)

class는 객체 지향 프로그래밍(OOP)의 핵심입니다. 코드를 더욱 안전하게 캡슐화할 수 있습니다. class를 사용하면 코드 구조가 좋아지고 방향을 유지합니다.

class를 만들려면 class 키워드 뒤에 두 개의 중괄호가 있는 class 이름을 사용합니다.

```
class myClass {
	constructor() {

	}
}
```

이제 new 키워드를 사용하여 class 메서드와 속성에 액세스할 수 있습니다.

```
class myClass {
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}
}

const user = new myClass('영희', 22);

console.log(user.name); // 영희
console.log(user.age); // 22
```

다른 class에서 상속하려면 extends 키워드 다음에 상속할 class의 이름을 사용합니다.

```
class myClass {
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}

	sayHello() {
		console.log(`안녕 ${this.name} 너의 나이는 ${this.age}살이다`);
	}
}

// myClass 메서드 및 속성 상속
class UserProfile extends myClass {
	userName() {
		console.log(this.name);
	}
}

const profile = new UserProfile('영희', 22);

profile.sayHello(); // 안녕 영희 너의 나이는 22살이다.
profile.userName(); // 영희
```

출처

- [https://velog.io/@kimhscom/JavaScript-%EC%9E%90%EC%A3%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-ES6-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%A6%AC](https://velog.io/@kimhscom/JavaScript-%EC%9E%90%EC%A3%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-ES6-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%A6%AC)
- [https://github.com/lukehoban/es6features](https://github.com/lukehoban/es6features)
- [https://www.freecodecamp.org/news/write-less-do-more-with-javascript-es6-5fd4a8e50ee2/](https://www.freecodecamp.org/news/write-less-do-more-with-javascript-es6-5fd4a8e50ee2/)
