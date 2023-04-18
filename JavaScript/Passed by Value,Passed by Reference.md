PBV와 PVR의 주요 차이점은 **메모리에 저장되는 방식**입니다.

<br />

### Value & Reference 가 값을 저장하는 방식

Passed by Value : 실제 매개변수 값의 복사본이 메모리에 생성됨을 의미합니다.

Passed by Reference : 메모리에 새로운 공간을 만들지 않고 대신 실제 매개변수의 참조/주소를 전달하므로 함수가 변수의 원래 값에 액세스 할 수 있습니다. 따라서 함수 내에서 변수의 값을 변경하면 원래 값도 변경됩니다.

![image](https://user-images.githubusercontent.com/73993670/232743166-5c2043eb-90f9-4d53-a0e9-979547f2188f.png)


```js
let num1 = 10;

let obj1 = {
  firstName: "Allie",
  lastName: "Grater",
};
```

두 개의 메모리 위치가 있습니다. 하나는 스택(왼쪽)이고 다른 하나는 힙(오른쪽)입니다.

Javascript는 크기가 작고 변경되지 않기 때문에 기본 값을 스택에 저장합니다. 그러나 객체의 크기는 동적이며 변경될 수 있습니다. 따라서 별도의 힙 메모리 위치에 저장합니다.

value유형과 reference유형의 유일한 차이점입니다. 그러나 이것은 변수를 복사할 때 결정적인 차이를 만듭니다.

<br />

### Value Types are copied

![image](https://user-images.githubusercontent.com/73993670/232743188-6d811786-eed5-4797-8b3c-c736cc03f0a6.png)


```js
let num1 = 10;
let num2 = num1;
```

메모리에 두 개의 변수 num1& 가 있고 num2 둘 다 값 10을 포함하지만 둘 다 서로 독립적입니다

```js
num2 = 20;

console.log(num1); //10
console.log(num2); //20
```

num2의 값을 변경해도 num1에 영향을 주지 않습니다.

<br />

### Reference Types are copied

![image](https://user-images.githubusercontent.com/73993670/232743212-bc9a7f4d-e2fd-4cd6-81c5-7de2596d59a6.png)


```js
let obj1 = {
  firstName: "Allie",
  lastName: "Grater",
};

let obj2 = obj1;
```

obj1두 obj2개의 다른 변수이지만 동일한 메모리 위치를 가리킵니다.

```js
obj2.firstName = "John";

console.log(obj1.firstName); //John
console.log(obj2.firstName); //John
```

firstName의 속성을 변경하면 둘 다 동일한 개체를 참조하기 때문에 속성도 변경되는 obj2 것을 볼 수 있습니다

<br />

Passed by Value 언제 사용하는가

변수에서 이루어진 모든 변경 사항은 원래 변수와 독립적이므로 초기 변수를 추적하고 싶지 않을 때 유용합니다.

Pass by Reference 언제 사용하는가

큰 크기의 인수를 전달할 때, 호출된 함수에서 별도의 복사본이 만들어지지 않으므로 메모리가 낭비되지 않습니다.
