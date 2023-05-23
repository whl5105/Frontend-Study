# **Callback, Promise, async/await**

## **동기 비동기**

자바스크립트는 기본적으로 동기적으로 동작합니다.

<br/>

```javascript
console.log('1'); 
console.log('2'); 
console.log('3'); 

// 1
// 2
// 3
// console.log함수가 끝나고 다음 console.log함수가 순서대로 실행되는것 예측할수있습니다.
```
<br/>

어떤 동작이 끝날때까지 기다렸다가 다음 동작을 순차적으로 하는것을 동기적이다 라고 할 수 있습니다.

```javascript
console.log('1'); 
setTimeout(function() {
	console.log('2'); 
}, 1000);
console.log('3');

// 1
// 3
// 2
// 브라우저의 api setTimeout함수로 1초뒤에 console.log를 호출하는 콜백함수를 동작했을때
// 1다음 2를 기다리지 않고 3이 호출되는것을 확인 할 수 있습니다.
```

병렬적으로 동작하는것을 비동기적이라 라고 할 수 있습니다.

<br/>

# **Callback 함수**

**매개변수로 전달하고 내부에서 실행되는 함수**

<br/>


```javascript
function callback() {
  console.log('콜 해줘');
}

function fn(arg) {
  arg();
}

fn(callback); // 콜백함수
```

callback이라는 함수자체는 callback함수가 아니지만

**매개변수로 전달하고 내부에서 함수를 호출된 시점의 함수를 Callback함수 라고합니다.**

<br/>

```javascript
function goToSchool() {
  console.log("학교에 갑니다.");
}

function study() {
  console.log("열심히 공부를 합니다.");
}

function arriveAtSchool_asis() {
  setTimeout(function () {
    //콜백함수가 실행되고 study함수 실행
    console.log("학교에 도착했습니다.");
    study(); 
  }, 1000);
}

goToSchool();
arriveAtSchool_asis();

// 학교에 갑니다.
// 학교에 도착했습니다.
// 열심히 공부를 합니다.
```

비동기적인 동작을 **동기적으로 동작** 하고싶을때 사용합니다.

<br/>

![image](https://user-images.githubusercontent.com/90454621/228174337-8c137fb9-b068-4866-b3aa-127bc659c508.png)

비동기적인 작업을 수행하기 위해 콜백함수를 익명함수로 전달하는 과정에서 생기는 콜백지옥을 **Promise, async/await** 등을 사용해 방지할 수 있습니다.

<br>

# **Promise**

비동기 함수를 동기 처리하기 위해 고안한 객체입니다.

<br/>


**비동기 작업이 완료된 이후에 다음 작업을 연결시켜 진행**할 수 있는 기능을 가지고 있습니다.

작업 결과 따라 **성공 또는 실패를 리턴하며 결과 값을 전달** 받을 수 있습니다.

<br/>

### **Promise의 3가지 상태 및 처리 흐름**

**pending(대기)** : 처리가 완료되지 않은 상태

**fulfilled(이행)** : 성공적으로 처리가 완료된 상태

**rejected(거부)** : 처리가 실패로 끝난 상태


![image](https://user-images.githubusercontent.com/90454621/228187554-384107fb-73a5-4dd6-bfe0-46eee55ca69b.png)

<br/>

### **Promise 기본 예제**

```javascript
let myFirstPromise = new Promise((resolve, reject) => {
  // 우리가 수행한 비동기 작업이 성공한 경우 resolve(...)를 호출하고, 
  // 실패한 경우 reject(...)를 호출합니다.
  // 이 예제에서는 setTimeout()을 사용해 비동기 코드를 흉내냅니다.
  // 실제로는 여기서 XHR이나 HTML5 API를 사용할 것입니다.
  setTimeout(function () {
    resolve("성공!")  // 와! 문제 없음!
  }, 250)
})

console.log(myFirstPromise); // Promise { <pending> }

myFirstPromise.then((successMessage) => {
  // successMessage는 위에서 resolve(...) 호출에 제공한 값입니다.
  // 문자열이어야 하는 법은 없지만, 위에서 문자열을 줬으니 아마 문자열일 것입니다.
  console.log("와! " + successMessage)
});

// 와! 성공!
```

-   Promise엔 then() catch() finally()함수를 사용합니다.
-   then()은 **fulfilled상태 일때** 생성한 프로미스 객체에서 인수로 전달한 resolve가 실행됩니다.
-   catch()는 **rejected상태 일때** 생성한 프로미스 객체에서 인수로 전달한 reject가 실행됩니다.
-   finally()는 성공 실패 여부와 상관없이 마지막에 실행됩니다.

<br/>

### **Promise 고급 예제**

Promise 객체는 **2가지의 콜백 함수**를 가집니다.

하나는 앞서 언급한 **fulfilled 상태에서 실행되는 resolve 함수**이고 다른 하나는 **rejected 상태일 경우 실행되는 reject 함수**입니다.

```javascript
function goToSchool() {
  console.log("학교에 갑니다.");
}

function study() {
    console.log("열심히 공부를 합니다.");
}

function cure() {
  console.log("양호실에 가서 약을 발랐습니다.");
}

function arriveAtSchool_tobe_adv() {
  return new Promise(function(resolve, reject){
      setTimeout(function() {
          var status = Math.floor(Math.random()*2);
          if(status === 1) {
              resolve("학교에 도착했습니다.");
          } else {
              reject("중간에 넘어져 다쳤습니다.");
          }
      }, 1000);
  });
}

goToSchool();
arriveAtSchool_tobe_adv()
.then(function(res){
    console.log(res);
    study();
})
.catch(function(err){
    console.log(err);
    cure();
});
```

reject일 때는 then 메서드가 실행되지 않으므로 **성공, 실패를 각각 분리해서 처리**할 수 있게 됩니다.

<br/>

### **Promise의 장점 : Promise Chaining**

```javascript
const fectNumber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000);
});

fectNumber
  .then(num => num * 2) // 1 * 2 = 2
  .then(num => num * 3) // 2 * 3 = 6
  .then(num => {
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000);
    })
  })
  .then(num => console.log(num)); // 6 - 1 = 5
```

이렇게 연속적으로 묶어서 처리 할수있습니다.

하지만 이런방식은 콜백지옥과 유사해집니다.

<br>

# **async/await**

Promise 객체를 간결하고 간편하고 동기적으로 실행되는것 처럼 보이게 해 줍니다.

### **async 기본 예제**

```javascript
async function greet() {
    return 'hello';
} // 해당 스코프는 promise입니다.

greet().then(console.log); // hello

console.log(greet()); // Promise { 'hello' }
```

function 앞에 async 키워드만 붙여주면 됩니다. async 함수에서는 Promise가 아닌 값을 리턴하더라도 resolved promise가 반환됩니다.

function 앞에 **async를 선언한 함수는 항상 Promise 객체를 반환**합니다. Promise가 아닌 값을 리턴하더라도 내부적으로 Promise로 감싸서 리턴합니다.

<br/>

### **await 기본 예제**

```javascript
function greet() {
    return new Promise(function(resolve){
        setTimeout(function() {
            resolve('hello');
        }, 1000);
    });
}

(async function() {
    var result = await greet(); //resolved 될 때까지 대기
    console.log(result);
})();
```

async가 붙은 함수 내부에서만 사용 할수있습니다.

await 키워드만 붙여주면 비동기 작업의 순차 처리가 **일반 순차 프로그래밍과 동일하게 가능**합니다.

<br/>


```javascript
function fectNumber () { 
  return new Promise(resolve => {
   setTimeout(() => resolve(1), 1000);
 })
}

async function firstDeps () {
  const result = await fectNumber();  
  return result * 2;
}

async function secondDeps () {
  const result = await firstDeps();  
  return result * 3;
}

async function last () {
  const result = await secondDeps();  
  return result - 1;
}

last().then(console.log)
```

이런식으로 가독성이 좋게처리 할수 있고 콜백,then지옥에서 벗어날수 있습니다.

<br/>

## 💡 setState()는 await와 사용이 가능할까?
setState에는 await를 사용할 수 없습니다.

setState 메소드는 React의 클래스형 컴포넌트에서 사용되는 함수로, 컴포넌트의 상태(state)를 업데이트할 때 사용됩니다.
setState 메소드는 일반적으로 비동기로 작동하지만, await는 비동기 작업을 동기적으로 처리하기 위해 사용됩니다.

async / await 의 기반은 promise 입니다. async 함수는 promise를 반환하고 promise가 함수로부터 반환할 값을 resolve 합니다.

setState는 promise를 리턴하지 않기에 await와 함께 사용할 수 없습니다.

<br>

### 그렇다면 setState는 어떤식으로 작동할까요?
setState는 componentDidUpdate 나 setState 콜백을 사용해야 원하는 결과를 얻을 수 있습니다.

```javascript
this.setState({ myCabinet: "beer"});
console.log(this.state.myCabinet) // Not beer
```

```javascript
this.setState({ myCabinet: "beer"}, () => console.log(this.state.myCabinet)); // beer
```

참고

Callback  
혼자 공부하는 자바스크립트 p221   
[https://www.youtube.com/watch?v=s1vpVCrT8f4&t=772s](https://www.youtube.com/watch?v=s1vpVCrT8f4)  
[https://www.youtube.com/watch?v=TAyLeIj1hMc&t=683s](https://www.youtube.com/watch?v=TAyLeIj1hMc)  
  
Promise   
[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global\_Objects/Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)  
[https://sangminem.tistory.com/284](https://sangminem.tistory.com/284)  
[https://www.youtube.com/watch?v=JB\_yU6Oe2eE&t=1041s](https://www.youtube.com/watch?v=JB_yU6Oe2eE)

[https://www.youtube.com/watch?v=Sn0ublt7CWM&t=680s](https://www.youtube.com/watch?v=Sn0ublt7CWM&t=680s)

async/await   
[https://sangminem.tistory.com/479](https://sangminem.tistory.com/479)

[https://www.youtube.com/watch?v=aoQSOZfz3vQ&t=611s](https://www.youtube.com/watch?v=aoQSOZfz3vQ&t=611s) 

[https://www.youtube.com/watch?v=1z5bU-CTVsQ](https://www.youtube.com/watch?v=1z5bU-CTVsQ)

[setState()는 await와 사용이 가능할까?](https://dodokim.medium.com/setstate-%EB%8A%94-await%EC%99%80-%EC%82%AC%EC%9A%A9%EC%9D%B4-%EA%B0%80%EB%8A%A5%ED%95%A0%EA%B9%8C-7b02581f6df4)
