# this란?

자바스크립트에서 모든 함수는 실행될 때마다 함수 내부에 `this`라는 객체가 추가된다. 그렇기 때문에 `this`는 함수가 어떻게 호출되었는지에 따라 다르게 바인딩된다.

<br/>

## 호출 방법에 따라 달라지는 this

### 1. 객체의 메서드로 호출할 경우 (A.b 형태) 해당 메서드를 호출한 객체로 바인딩된다.

```jsx
const obj = {
  value: 1,
  printValue: function () {
    console.log(this);
  },
};

obj.printValue();

// {value: 1, printValue: f}
// obj가 printValue를 호출했기 때문
```

```jsx
const obj = {
  value: 1,
  printValue: function () {
    console.log(this);
  },
};

const obj2 = {
  value: 2,
  printValue: obj.printValue,
};

obj2.printValue();

// {value: 2, printValue: f}
// obj2가 호출했기 때문
```

<br/>

### 2. 함수를 직접 호출할 경우 this는 전역 객체에 바인딩된다.

```jsx
const obj = {
  value: 1,
  printValue: function () {
    console.log(this);
  },
};

const global = obj.printValue;

global();

// window 객체
// global함수가 호출될 때 A.b의 형태로 호출되지 않고, window 객체가 호출했기 때문
```

```jsx
const obj = {
  value: 1,
  printValue: function () {
    const innerFunc = function () {
      console.log(this);
    };
    innerFunc();
  },
};

obj.printValue();

// window 객체
// innerFunc 함수가 호출될 때 A.b의 형태로 호출되지 않고, window 객체가 호출했기 때문
```

### 3. ES5에서 추가된 `call`, `apply`, `bind` 와 같은 메서드를 활용하면, 함수를 어떻게 호출했는지와 상관 없이 직접 `this`를 설정할 수 있다.

```jsx
const func = function () {
  console.log(this);
};

const obj = {
  value: 1,
};

func.call(obj); // {value: 1}
func.apply(obj); // {value: 1}
func.bind(obj)(); // {value: 1}
```

<br/>

### 4. 화살표 함수에서의 this는 함수가 속해있는 곳의 상위 this를 계승받는다.

```jsx
const obj = {
  value: 1,
  printValue: function () {
    const innerFunc = () => {
      console.log(this);
    };
    innerFunc();
  },
};

obj.printValue();

// {value: 1, printValue: f}
// 화살표 함수에서의 this는 함수가 속해있는 곳의 상위 this를 계승받기 때문
```

화살표 함수는 `call`, `bind`, `apply`를 사용하여 `this`의 값을 정할 수 없다.

<br/>

### 5. `new` 키워드를 통해 생성자 함수를 호출할 경우, this는 생성된 객체인 자신이 된다.

```jsx
function Func(value) {
  this.value = value;
  this.printValue = function () {
    console.log(this);
  };
}

let a = new Func(2);
a.printValue();

// Func {value: 2, printValue: ƒ}
```

<br/>

### 6. strict mode에서는 this가 `undefined` 로 초기화된다.

<br/>

## this 사용법

- this를 예측 가능하게 사용하기 위해서 일반 함수와 this 바인딩 메서드를 함께 사용한다.

- 함수 내부의 함수에서 this를 사용할 때는 상위의 this를 함께 사용하는 경우가 많기 때문에 화살표 함수를 사용하기도 한다.

<br/>

## 참고

- [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)
- [https://youtu.be/tDZROpAdJ9w](https://youtu.be/tDZROpAdJ9w)
