## **자바스크립트의 상속**

자바스크립트에서 상속이나 캡슐화 같은 개념이 명시적으로 존재하지는 않기 때문에 자바나 C++ 기반 클래스 기반 언어를 사용하던 개발자(OOP에 익숙한 개발자)들이 자바스크립트에서 이런 개념을 가져다 사용하기 위해 프로토타입을 사용하여 이를 유사하게 구현한 일종의 디자인 패턴입니다.

상속은 프로토타입 체인을 사용하여 구현하고, 캡슐화는 클로저를 사용해서 구현합니다.

### Prototype이란?

JavaScript는 프로토타입 기반의 언어이며, 프로토타입이란 객체의 원형을 뜻합니다. 즉, 모든 객체는 프로토타입이라는 객체를 가지고 각각의 프로토타입으로부터 property와 method를 상속 받습니다.

### Prototype을 왜 사용해야 할까 ?

생성자 함수 이야기를 해보자면, 생성자 함수를 쓰는 이유는 객체 리터럴로만 객체를 생성하기엔 비효율적이기 때문입니다. 따라서 생성자 함수를 이용해서 인스턴스를 생성하는 방식으로 객체를 생성하는 방식의 단점을 보완할 수 있습니다.

프로토타입의 사용이유는 코드 재사용과 효율성을 위해서입니다. 만약 생성자 함수로 새로 생성되는 인스턴스에 공통된 메서드가 포함된 경우를 생각하면 모든 인스턴스들이 중복으로 생성이되고, 불필요하게 메모리가 낭비됩니다. 이를 위해 프로토타입에 해당 메서드를 등록해서 인스턴스들이 공유해 사용할 수 있게 만들어 줍니다.

### Prototype Chain이란?

자바스크립트는 특정 property나 method에 접근하려고 할 때, 해당 property나 method가 없을 시 [[Prototype]]이 가리키는 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 property나 method를 차례대로 검색합니다. 이를 프로토타입 체인이라고 합니다.

## prototype vs **proto**

prototype: 내가 원형일 때 존재함.

- 함수 객체만 가지고 있다.
- 생성자를 가지는 원형으로 선언 가능

**proto**: 나의 원형을 가리킴

- 모든 객체가 가지고 있다.
- 하나의 링크라고 할 수 있다.

### Prototype 예제

Person 개체에 대한 생성자 함수를 만들고 싶다고 가정하고, 이 생성자 함수를 다음과 같이 정의할 수 있습니다.

```jsx
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.introduce = function () {
    console.log(`Hi, my name is ${name}, ${age}`);
  };
}
```

위의 코드로 new 생성자를 통해 객체를 생성하게 되면, 인스턴스는 매개변수를 이용해 객체 내부를 구성합니다. 그리고 introduce라는 함수도 공통적으로 가지고 있어, 함수를 새롭게 생성하지 않아도 됩니다.

```jsx
const kim = new Person("kim", 20);
const park = new Person("park", 40);

kim.introduce();
park.introduce();

// Hi, my name is kim, 20// Hi, my name is park, 40
```

하지만 위의 코드로 작성되었을때 Person이라는 생성자 함수를 불러올 때 마다  introduce라는 함수가 생성되며 불필요한 메모리 공간을 차지하게 됩니다. 이것을 개선하기 위해 우리는 프로토타입을 활용하여 introduce 함수를 재사용할 수 있도록 하겠습니다.

```jsx
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.introduce = function () {
  console.log(`hi my name is ${this.name}, ${this.age}`);
};

const kim = new Person("kim", 20);
const park = new Person("park", 40);

kim.introduce();
park.introduce();

// Hi, my name is kim, 20
// Hi, my name is park, 40
```

Person이라는 생성자 객체에는 introduce라는 메서드는 없지만, 부모역할을 하는 프로토타입에서 메서드를 찾아 호출합니다. 이것은 프로토타입 체인에 해당되며, introduce라는 메서드가 상속됩니다. 이렇게 프로토타입으로 선언한 경우 인스턴스가 생성될 때마다 introduce를 생성하는 것이 아니라 Person 원형의 메서드를 찾아 실행되는 것이므로, 중복되는 생성으로 일어나는 불필요한 메모리 소모를 줄일 수 있습니다.

---

Reference : 모던 자바스크립트 Deep Dive
