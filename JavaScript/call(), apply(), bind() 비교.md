# call(), apply(), bind() 비교

## this를 바인딩하기 위해 사용

call(), apply(), bind()는 첫번째 인수 값으로 this를 바인딩할 수 있다.

<br/>

### **call()**

this 값을 지정하는 동시에 함수를 호출한다.

```javascript
const obj = {
  name: "obj",
};

function printThis() {
  console.log(this);
}

printThis.call(obj); // {name: 'obj'}
```

<br/>

### **apply()**

this 값을 지정하는 동시에 함수를 호출한다.

```javascript
const obj = {
  name: "obj",
};

function printThis() {
  console.log(this);
}

printThis.apply(obj); // {name: 'obj'}
```

<br/>

### **bind()**

this 값을 지정할 수 있지만 함수를 호출하지는 않는다.

```javascript
const obj = {
  name: "obj",
};

function printThis() {
  console.log(this);
}

printThis.bind(obj)(); // {name: 'obj'}
```

<br/>

## 인수 전달 방식의 차이

### **call()**

인수 목록을 받는다.

```javascript
const kim = {
  name: "kim",
};

function updatePerson(age, job) {
  this.age = age;
  this.job = job;
}

updatePerson.call(kim, 40, "teacher");
console.log(kim); // {name: 'kim', age: 40, job: 'teacher'}
```

<br/>

### **apply()**

인수 배열 하나를 받는다.

```javascript
const kim = {
  name: "kim",
};

function updatePerson(age, job) {
  this.age = age;
  this.job = job;
}

updatePerson.apply(kim, [40, "teacher"]);
console.log(kim);
// {name: 'kim', age: 40, job: 'teacher'}
```

<br/>

### **bind()**

인수 목록을 받는다.

```javascript
const kim = {
  name: "kim",
};

function updatePerson(age, job) {
  this.age = age;
  this.job = job;
}

updatePerson.bind(kim, 40, "teacher")();
console.log(kim); // {name: 'kim', age: 40, job: 'teacher'}
```

<br/>

## 함수의 arguments를 조작할 때 사용

<br/>

### **arguments**

- 함수가 가지고 있는 숨겨진 속성
- 함수에 들어온 인자를 배열 형식으로 반환
- 이때 arguments는 배열 형식이지만, 배열이 아니라 유사 배열이기 때문에 배열의 메서드를 사용할 수 없다.

```javascript
function example() {
  console.log(arguments);
}

example(1, 2, 3); // [1, 2, 3]
```

<br/>

call(), apply(), bind()를 사용하면 arguments에 배열 메서드를 쓸 수 있다.

<br/>

### **예시**

```javascript
function example() {
  console.log(Array.prototype.pop.call(arguments));
}

example(1, 2, 3); // 3
```

```javascript
const numbers = [1, 2, 3];

const maxNum = Math.max.apply(null, numbers);

console.log(maxNum); // 3
```

<br/>

## 참고

- call, apply, bind [https://www.zerocho.com/category/JavaScript/post/57433645a48729787807c3fd](https://www.zerocho.com/category/JavaScript/post/57433645a48729787807c3fd)
- call [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/call](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
- apply [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/apply](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
- bind [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- arguments [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments)
