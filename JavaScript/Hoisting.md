### **호이스팅(Hoisting)?**

JavaScript에서 **호이스팅**(hoisting)이란, **변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징**입니다.

```jsx
console.log(score); // undefined
var score; // 변수 선언
```

위 예제를 살펴보면 변수 선언문보다 변수를 참조하는 코드가 앞에 있습니다. 자바스크립트 코드는 인터프리터에 의해 한 줄씩 순차적으로 실행되므로 console.log(socre)가 가장 먼저 실행되고 순차적으로 다음 줄에 있는 코드를 실행합니다.

따라서 console.log(score);가 실행되는 시점에는 아직 score 변수의 선언이 실행되지 않았으므로 ReferenceError가 발생할 것처럼 보입니다. 하지만 참조에러가 발생하지 않고 undefined가 출력됩니다.

그 이유는 변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문입니다.

자바스크립트 엔진은 소스코드를 한 줄씩 순차적으로 실행하기에 앞서 먼저 소스코드의 평가 과정을 거치면서 소스코드를 실행하기 위한 준비를 합니다. 이때 소스코드 실행을 위한 준비 단계인 소스코드의 평가 과정에서 자바스크립트 엔진은 변수 선언을 포함한 모든 선언문을 소스코드에서 찾아내 면저 실행합니다. 그리고 소스코드의 평가과정이 끝나면 비로소 변수 선언을 포함한 모든 선언문을 제외하고 소스코드를 한 줄씩 순차적으로 실행합니다.

즉 **자바스크립트 엔진은 변수 선언이 소스코드의 어디에 있든 상관없이 다른 코드보다 먼저 실행합니다. 따라서 변수 선언이 소스코드의 어디에 위치하는지와 상관없이 어디서든지 변수를 참조할 수 있습니다.**

### **함수 호이스팅**

```jsx
// 함수 참조
console.dir(add); // f add(x,y)
console.dir(sub); // undefined;

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}
// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

자바스크립트에서 함수는 함수 표현식과 함수 선언식으로 나눌 수 있습니다. 위 예제와 같이 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있습니다. 그러나 함수 표현식의 경우 호출할 수 없습니다. 이는 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르기 때문입니다.

함수 선언문으로 함수를 정의하면 런타임 이전에 함수 객체가 먼저 생성됩니다. 그리고 자바스크립트 엔진은 이름과 동일한 이름의 식별자를 암묵적으로 생성하고 생성된 함수 객체를 할당합니다. 즉, 코드가 한 줄씩 순차적으로 실행되기 시작하는 런타임에는 이미 함수 객체가 생성되어 있고 함수 이름과 동일한 식별자에 할당까지 완료된 상태입니다. 따라서 함수 선언문 이전에 함수를 참조할 수 있으며 호출할 수도 있습니다.

함수 표현식은 변수에 할당되는 값이 함수 리터럴인 문입니다. 따라서 함수 표현식은 변수 선언문과 변수 할당문을 한 번에 기술한 축약 표현과 동일하게 동작합니다. 변수 선언은 런타임 이전에 실행되어 undefined로 초기화되지만 변수 할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 됩니다.

**따라서 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생합니다.**

---

**Reference : 모던 자바스크립트 Deep Dive**
