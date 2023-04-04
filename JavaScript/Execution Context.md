# **실행 컨텍스트**

자바스크립트 엔진은 코드를 실행하기 위해 변수(전역 변수, 매개 변수 등)와 변수의 스코프, this와 같은 정보들이 필요합니다.

어떤 실행 컨텍스트가 활성화될 때, 자바스크립트 엔진은 해당 컨텍스트의 코드를 실행하는데 필요한 환경 정보들을 수집해서 실행 컨텍스트에 저장합니다.

이 중 식별자, 스코프, this 등은 실행 컨텍스트의 렉시컬 환경을 기반으로 관리되며, 코드의 실행순서는 콜스택(실행 컨텍스트 스택)을 통해서 관리됩니다.

## **소스코드의 타입**

ECMAScript 사양은 소스코드를 4가지 타입으로 구분합니다. 그리고 4가지 타입의 소스코드는 실행 컨텍스트를 생성합니다. 이렇게 4가지 타입으로 구분하는 이유는 소스코드의 타입에 따라 실행 컨텍스트를 생성하는 과정과 관리되는 내용이 다르기 때문입니다.

1. 전역 코드
   - 전역 코드는 전역 변수를 관리하기 위해 최상위 스코프인 전역 스코프를 생성해야 합니다.
   - var 키워드로 선언된 전역 변수와 함수 선언문으로 정의된 전역 함수를 전역 객체의 프로퍼티와 메서드로 바인딩하고 참조하기 위해 전역 객체와 연결되어야 합니다.
   - 전역 코드가 평가되면 전역 실행 컨텍스트가 생성됩니다.
2. 함수 코드
   - 지역 스코프를 생성하고 지역 변수, 매개변수, arguments 객체를 관리해야 합니다.
   - 생성한 지역 스코프를 전역 스코프에서 시작하는 스코프 체인의 일원으로 연결해야 합니다.
   - 함수 코드가 평가되면 함수 실행 컨텍스트가 생성됩니다.
3. eval 코드
   - eval 코드는 strict mode에서 자신만의 독자적인 스코프를 생성합니다.
   - eval 코드가 평가되면 실행 컨텍스트가 생성됩니다.
4. 모듈 코드
   - 모듈별로 독립적인 모듈 스코프를 생성합니다.
   - 모듈 코드가 평가되면 모듈 실행 컨텍스트가 생성됩니다.

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWuQnE%2FbtrC3MpLzDG%2FRbeFjV68Sf64frW0upCib1%2Fimg.png)

## **소스코드의 평가와 실행**

모든 소스코드는 실행에 앞서 평가 과정을 거치며 코드를 실행하기 위해 준비를 합니다. 실행 컨텍스트는 종류별로 세부적인 구성요소와 동작이 다르지만 모든 실행 컨텍스트는 평가, 실행 단계를 거쳐서 생성되고 관리됩니다.

### 평가

실행 컨텍스트를 생성하고 변수, 함수 등의 선언문을 파악해서 현재 스코프 내에서 사용할 수 있는 변수, 함수의 식별자를 실행 컨텍스트에 등록하는 과정입니다.

여기서 호이스팅이라는 개념이 나옵니다. 마치 코드블럭의 제일 상위 부분으로 끌어올려지는 것 같은 현상을 호이스팅이라고 이야기 합니다. 평가과정에서 식별자들에 대한 정보가 먼저 실행 컨텍스트에 기록되는 동작 때문에 일어나는 현상인 것입니다.

### 실행

실행이란 선언문을 제외한 소스코드를 실행하는 과정을 의미합니다. 이 과정에서는 소스코드 실행에 대한 필요한 정보, 즉 변수나 함수의 참조를 실행 컨텍스트에서 찾고 실행과정에서 일어나는 변수값의 변경 등은 다시 실행 컨텍스트에 등록됩니다.

## **실행 컨텍스트 스택**

```javascript
const x = 1;
function foo() {
  const y = 2;

  function bar() {
    const z = 3;
    console.log(x + y + z);
  }
  bar();
}

foo();
```

위 예제에서 소스코드의 타입으로 분류할 때 전역 코드와 함수코드로 이루어져 있스비다. 자바스크립트 엔진은 먼저 전역 코드를 평가하여 전역 실행 컨텍스트를 생성합니다. 그리고 함수가 호출되면 함수 코드를 평가하여 함수 실행 컨텍스트를 생성합니다.

이때 생성된 실행 컨텍스트는 스택 자료구조로 관리되고, 이를 실행 컨텍스트 스택이라고 부릅니다.

위 예제에서 코드의 실행순서를 나타내면 다음과 같습니다.

1. 전역 코드의 평가와 실행
2. foo 함수 코드의 평가와 실행
3. bar 함수 코드의 평가와 실행
4. foo 함수 코드로 복귀
5. 전역 코드로 복귀

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbpO48N%2FbtrC2MDS0bp%2F3px3oIBSjmSIVfxzfse33k%2Fimg.png)

## **LexicalEnvironment**

모든 실행 컨텍스트의 객체와 같이 내부적으로 여러 프로퍼티를 가지고 있으며, 각 프로퍼티들은 고유한 정보를 표현합니다. 실행 컨텍스트의 내부에는 LexicalEnvironment라는 객체가 존재합니다. 실행 컨텍스트 스택이 코드의 실행 순서를 관리한다면 LexicalEnvironment는 스코프와 식별자를 관리합니다.

렉시컬 환경은 키와 값을 갖는 객체 형태의 스코프를 생성하여 식별자를 키로 등록하고 식별자에 바인딩된 값을 관리합니다.

즉, 렉시컬 환경은 스코프를 구분하여 식별자를 등록하고 관리하는 저장소 역할을 합니다.

### **LexicalEnvironment 와 VariableEnvironment**

실행 컨텍스트는 LexicalEnvironment와 VariableEnvironment 컴포넌트로 구성됩니다.

- LexicalEnvironment
  - 변경 사항이 실시간으로 반영됩니다.
- VariableEnvironment
  - 현재 컨텍스트 내의 식별자들에 대한 정보를 가집니다.
  - 외부 환경 정보를 가집니다.
  - 선언 시점의 LexicalEnvironment의 스냅샷을 유지합니다. (변경사항 반영x)

실행 컨텍스트를 생성할 때 VariableEnvironment에 정보를 먼저 담은 다음, 이를 복사해서 LexicalEnvironment를 만듭니다. 즉 VariableEnvironment는 스냅샷 유지를 목적으로 사용합니다.

생성 초기의 실행 컨텍스트와 렉시컬 환경을 그림으로 표현하면 다음과 같습니다.

<center><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F87UrF%2FbtrC4PfjnbH%2FsFqigxccBmL0Pg4eew7Djk%2Fimg.png" width="600" height="150"></center>

생성 초기에 LexicalEnvironment 컴포넌트와 VariableEnvironment 컴포넌트는 하나의 동일한 렉시컬 환경을 참조합니다. 이후 몇 가지 상황을 만나면 VariableEnvironment 컴포넌트를 위한 새로운 렉시컬 환경을 생성하고, 이때부터 VariableEnvironment 컴포넌트와 LexicalEnvironment 컴포넌트는 내용이 달라지는 경우도 있습니다.

렉시컬 환경은 다음과 같이 두 개의 컴포넌트로 구성됩니다.

<center><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaWE9b%2FbtrC3EZwb5X%2FUFCUOnMexhDvfa9ZxdP4m0%2Fimg.png" width="350" height="150"></center>
</br>

1. 환경 레코드(Environment Record)
   - 스코프에 포함된 식별자를 등록하고 등록된 식별자에 바인딩된 값을 관리하는 저장소입니다.
   - 환경 레코드는 소스코드의 타입에 따라 관리하는 내용에 차이가 있습니다.
2. 외부 렉시컬 환경에 대한 참조(Outer Lexical Environment Reference)
   - 외부 렉시컬 환경에 대한 참조는 상위 스코프를 가리킵니다.
   - 상위 스코프란 외부 렉시컬 환경, 즉 해당 실행 컨텍스트를 생성한 소스코드를 포함하는 상위 코드의 렉시컬 환경을 말합니다.
   - 외부 렉시컬 환경에 대한 참조를 통해 단방향 링크드 리스트인 스코프 체인을 구현합니다.

LexicalEnvironemnt는 평가과정에서 일반적으로 크게 3가지의 동작을 수행합니다.

1. 식별자 생성
2. this binding
3. 참조할 외부 환경 결정

## **실행 컨택스트의 생성과 식별자 검색 과정**

먼저, 자바스크립트 코드가 실행되면서 먼저 전역 객체가 생성됩니다. 전역 객체는 자바스크립트에 기본적으로 포함되어 있는 빌트인 객체, 함수, 객체를 포함합니다. 이는 자바스크립트가 실행되는 환경(node, web)등에 따라서 일부 달라집니다.

이해를 돕기 위해 코드 형태로 보자면 먼저, 전역 객체가 생성됩니다.

```javascript
const global = {
  // 전역 객체
  console: {
    log() {},
  },
};
```

그 다음, 전역 코드가 평가되며 GlobalExecutionContext가 생성되며 그 내부에 GlobalLexicalEnvironment가 생성됩니다.

```javascript
const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {},
};
```

GlobalLexicalEnvironment는

let, const로 선언한 변수를 관리하는 Declarative Environment Record
그 외의 영역(var, 전역 함수, 빌트인 프로퍼티 등)을 관리하는 ObjectEnvironmentRecord
두 프로퍼티를 가지고 있습니다.

```javascript
const global = {
  // 전역 객체
  console: {
    log() {},
  },
};

const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {
    GlobalEnvironmentRecord: {
      ObjectEnvironmentRecord: {
        BindingObject: global,
      },
      DeclarativeEnvironmentRecord: {
        // let, const로 선언한 키워드를 저장
        // 선언과 초기화가 분리되서 실행, 초기화전에는 TDZ에 빠지게 됨
      },
    },
  },
};
```

ObjectEnvironmentRecord안에는 BindingObject 프로퍼티에서 전역객체를 참조합니다. 이제 var로 선언된 변수, 전역에 선언된 함수 선언은 BindingObject를 통해서 전역객체의 프로퍼티에 등록되게 됩니다.

그리고 let과 const로 선언된 키워드들은 DeclarativeEnvironmentRecord에 저장되며, 여기에 저장된 식별자들은 선언과 초기화 과정이 분리되서 실행됩니다. 따라서 var로 선언한 변수와 함수선언과는 다르게 초기화전까지는 접근할 수 없게 됩니다.

```javascript
// 👈👈👈(실행중인 코드)

var x = "var"; // var 키워드로 전역변수 x 선언 후 값 "var" 할당
const a = "a"; // const 키워드로 전역변수 a 선언 후 값 "a" 할당

function foo() {
  // 전역함수 foo 선언
  const b = "b";
  bar();

  function bar() {
    const c = "c";
    console.log("Hello, World");
  }
}

foo(); // 전역함수 foo 호출

const global = {
  // 전역 객체
  console: {
    log() {},
  },
  x: undefined, // var로 선언한 전역변수 x, undefined로 초기화
  foo: "<function object>", // 전역함수 foo
};

const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {
    GlobalEnvironmentRecord: {
      ObjectEnvironmentRecord: {
        BindingObject: global,
      },
      DeclarativeEnvironmentRecord: {
        a: "<uninitialized>", // const로 선언한 전역변수 a, 초기화 되지 않음
      },
    },
  },
};
```

그리고 이제 this값에 대한 참조가 결정됩니다. this값에 대한 참조는 GlobalThisValue라는 프로퍼티에 저장됩니다. 전역 코드의 this는 전역 객체를 가리키므로, GlobalThisValue의 값은 global이 됩니다.

```javascript
const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {
    GlobalEnvironmentRecord: {
      ObjectEnvironmentRecord: {
        BindingObject: global,
      },
      DeclarativeEnvironmentRecord: {
        a: "<uninitialized>",
      },
      GlobalThisValue: global, // this 값에 대한 참조를 전역객체 global로 설정
    },
  },
};
```

그리고 마지막으로 외부 환경에 대한 참조가 결정됩니다. 전역 실행 컨텍스트는 그 자체가 최상위 스코프이므로 외부 환경에 대한 참조값은 null이 됩니다.

```javascript
const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {
    GlobalEnvironmentRecord: {
      ObjectEnvironmentRecord: {
        BindingObject: global,
      },
      DeclarativeEnvironmentRecord: {
        a: "<uninitialized>",
      },
      GlobalThisValue: global,
    },
    OuterLexicalEnvironmentReference: null, // 외부환경에 대한 참조를 null로 결정
  },
};
```

이제, 평가과정에서 수행할 식별자 정의, this binding, 외부 환경 참조 결정 과정이 모두 완료되고 실행과정에서 실제 값들이 할당되기 시작합니다.

```javascript
var x = "var";
const a = "a"; // 👈👈👈(실행중인 코드)

function foo() {
  const b = "b";
  bar();

  function bar() {
    const c = "c";
    console.log("Hello, World");
  }
}

foo();

const global = {
  console: {
    log() {},
  },
  x: "var", // x에 "var" 할당
  foo: "<function object>",
};

const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {
    GlobalEnvironmentRecord: {
      ObjectEnvironmentRecord: {
        BindingObject: global,
      },
      DeclarativeEnvironmentRecord: {
        a: "a", // a에 "a" 할당
      },
      GlobalThisValue: global,
    },
    OuterLexicalEnvironmentReference: null,
  },
};
```

전역 실행 컨텍스트를 통해서 코드를 실행하던 중, foo 함수가 호출됩니다. 자바스크립트는 함수가 호출되면 함수 실행 컨텍스트를 생성하고 스택에 푸쉬합니다.

함수 실행컨텍스트도 마찬가지로 내부에 LexicalEnvironment가 생성됩니다. 그리고 LexicalEnvironment안에는 FunctionEnvironmentRecrod가 생성됩니다. 이 안에는 매개변수와 함수 내부에서 생성된 지역변수등이 저장됩니다.

```javascript
var x = "var"
const a = 'a';

function foo() {
	console.log(x);
  const b = 'b';
  bar();

  function bar() {
    const c = 'c';
    console.log("Hello, World")
  }
}

foo(); // 👈👈👈(실행중인 코드)

const FunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      // 매개변수, arguments, 지역 변수, 함수 등록
      b: "<uninitialized>",
      bar: "<function object>"
    },
};
```

그 다음은 함수의 this 참조값을 결정짓습니다. 함수의 this 참조값은 함수가 호출되는 상황에 따라서 결정되는데 여기서 foo 함수는 일반 함수로 호출되었으므로 this값은 전역객체가 됩니다.

```javascript
const FunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      b: "<uninitialized>",
      bar: "<function object>"
      ThisValue:global
    },
};
```

그리고, 함수의 외부 환경에 대한 참조를 결정합니다. 이때 중요한 특징이 있습니다. 바로, 함수의 정의는 함수를 평가 할 때 결정됩니다. 따라서 평가될 시점에 실행중인 실행 컨텍스트가 바로 함수의 OuterEnvironmentRecordReference가 됩니다.

여기서 foo 함수는 전역 실행 컨텍스트에서 평가되었으므로 foo 함수의 외부 참조값은 전역 실행 컨텍스트의 LexicalEnvironment입니다. 따라서, FunctionExecutionContext안에서는 GlobalLexicalEnvironment에 정의된 값들을 접근하고 사용할 수 있습니다.

```javascript
const FunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      b: "<uninitialized>",
      bar: "<function object>",
      ThisValue: global,
    },
    OuterEnvironmentReference: GlobalExecutionContext.GlobalLexicalEnvironment, // 함수가 정의된 시점에 실행중인 실행 컨텍스트의 LexicalEnvironment를 참조
  },
};
```

즉, 함수의 실행 컨텍스트는 함수의 호출 시점에 생성되지만, 함수의 외부 환경에 대한 참조는 어디서 호출했는지가 아니라 어디서 정의되었는지에 따라서 결정됩니다. 좀 더 상세하게 설명하자면 자바스크립트 엔진은 함수 정의를 평가하여 함수 객체를 생성할 때 실행중인 실행 컨텍스트의 렉시컬 환경을 함수 객체의 내부 슬롯 [[Environment]]에 저장하고 함수의 OuterEnvironmentRecord Reference에 할당되는 값은 함수 객체의 내부슬롯 [[Environment]]에 저장된 렉시컬 환경에 대한 참조입니다.

```javascript
const global = {
  // 전역 객체
  console: {
    log() {},
  },
  x: undefined, // var로 선언한 전역변수 x, undefined로 초기화
  foo: {
    [[Environment]]: GlobalExecutionContext.GlobalLexicalEnvironment,
  }, // 전역함수 foo
};

const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {
    GlobalEnvironmentRecord: {
      ObjectEnvironmentRecord: {
        BindingObject: global,
      },
      DeclarativeEnvironmentRecord: {
        a: "<uninitialized>", // const로 선언한 전역변수 a, 초기화 되지 않음
      },
    },
  },
};

const FooFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      b: "<uninitialized>",
      bar: "<function object>",
      ThisValue: global,
    },
    OuterEnvironmentReference: global.foo[[Environment]],
    // 함수 객체의 [[Environment]] 값 참조
  },
};
```

이러한 동작으로 인해서 클로저라는 개념이 성립되게 됩니다. 클로저는 외부 환경을 기억하고 있는 함수입니다.

클로저를 이해하기 위해서는 실행 컨텍스트와 렉시컬 환경이 별개의 존재라는 것을 인식해야 합니다. 실행 컨텍스트는 해당 컨텍스트안의 모든 코드를 실행하고 나면 콜스택에서 제거되지만, 실행 컨텍스트가 제거된다고 반드시 렉시컬 환경이 제거되는 것은 아닙니다. 렉시컬 환경은 실행 컨텍스트에 의해서 참조되기는 하지만, 독립적인 객체로서 그 누구에게도 참조되지 않을 때 비로소 가비지 컬렉팅 대상이 되어서 메모리에서 소멸됩니다

따라서 외부 함수의 실행 컨텍스트 내에서 정의된 내부함수가 외부 함수의 LexicalEnvironment를 계속해서 참조하고 있다면 외부 함수의 LexicalEnvironment는 소멸하지 않습니다.

```javascript
const global = {
  // 전역 객체
  console: {
    log() {},
  },
  x: undefined, // var로 선언한 전역변수 x, undefined로 초기화
  foo: {
    [[Environment]]: GlobalLexicalEnvironment,
  }, // 전역함수 foo
};

const GlobalExecutionContext = {
  GlobalLexicalEnvironment: GlobalLexicalEnvironment,
};

const GlobalLexicalEnvironment = {
  GlobalEnvironmentRecord: {
    ObjectEnvironmentRecord: {
      BindingObject: global,
    },
    DeclarativeEnvironmentRecord: {
      a: "<uninitialized>", // const로 선언한 전역변수 a, 초기화 되지 않음
    },
  },
};

// GlobalExecutionContext를 더이상 참조 하지 않으면
// GlobalExecutionContext는 메모리에서 사라짐
// 하지만, GlobalLexicalEnvironment는 foo[[Environment]]에서 참조하고 있기에 사라지지 않음

const FooFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      b: "<uninitialized>",
      bar: "<function object>",
      ThisValue: global,
    },
    OuterEnvironmentReference: global.foo[[Environment]],
    // 함수 객체의 [[Environment]] 값 참조
  },
};
```

클로저의 예시

```javascript
function outer() {
  let count = 0;

  function counter() {
    return count++;
  }
  // counter는 counter 함수의 평가시점인 outer함수의 실행컨텍스트의 LexicalEnvironment를 참조하고 있음

  return counter;
}

const couter = outer();
couter(); // 0
couter(); // 1
couter(); // 2
couter(); // 3
```

본론으로 돌아와서, 이제 foo 함수 실행 컨텍스트의 평가 과정이 종료되었으니 실행과정으로 넘어갑니다. 그리고 foo 함수의 실행 과정에서 bar 함수가 호출되었으므로 bar 함수의 실행 컨텍스트가 생성됩니다.

```javascript
var x = "var";
const a = "a";

function foo() {
  const b = "b";
  bar(); // 👈👈👈(실행중인 코드)

  function bar() {
    const c = "c";
    console.log("Hello, World");
  }
}

foo();

const FooFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      b: "b",
      bar: "<function object>",
      ThisValue: global,
    },
    OuterEnvironmentReference: GlobalExecutionContext.GlobalLexicalEnvironment,
  },
};
```

bar 함수의 실행 컨텍스트도 마찬가지로 생성되고 똑같이 평가와 실행과정을 거칩니다.

```javascript
const FooFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      b: "b",
      bar: "<function object>",
      ThisValue: global,
    },
    OuterEnvironmentReference: GlobalExecutionContext.GlobalLexicalEnvironment,
  },
};

const BarFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      c: "c",
      ThisValue: global,
    },
    OuterEnvironmentReference: FooFunctionExecutionContext.LexicalEnvironment,
  },
};
```

bar 함수를 실행하는 과정에서 console.log("Hello, World")라는 코드가 실행됩니다. 이 코드를 실행하기 위해서는 console 객체의 log 메서드를 찾아야합니다. 하지만 BarContext안에서는 console 식별자를 찾을 수 없습니다. 자바스크립트에서는 실행 컨텍스트 안에서 원하는 식별자를 찾을 수 없으면 OuterEnvironmentReference에 접근해서 원하는 식별자가 있는지 검색하는 동작을 수행합니다. BarContext의 외부 참조는 FooContext의 LexicalEnvironment이므로 해당 객체에 접근해서 탐색하는 과정을 수행합니다.

하지만, FooContext에도 원하는 값이 없습니다. 이런 경우에는 원하는 값을 찾을때까지 계속해서 참조를 거슬러서 올라갑니다. Foo의 참조는 GlobalLexicalEnvironemnt이므로 해당 객체에 접근합니다.

```javascript
var x = "var";
const a = "a";

function foo() {
  const b = "b";
  bar();

  function bar() {
    const c = "c";
    console.log("Hello, World"); // 👈👈👈(실행중인 코드)
  }
}

foo();
const global = {
  console: {
    log() {},
  },
  x: "var",
  foo: "<function object>",
};

const GlobalExecutionContext = {
  GlobalLexicalEnvironment: {
    GlobalEnvironmentRecord: {
      ObjectEnvironmentRecord: {
        BindingObject: global,
      },
      DeclarativeEnvironmentRecord: {
        a: "a",
      },
      GlobalThisValue: global,
    },
    OuterLexicalEnvironmentReference: null,
  },
};

const FooFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      b: "b",
      bar: "<function object>",
      ThisValue: global,
    },
    OuterEnvironmentReference: GlobalExecutionContext.GlobalLexicalEnvironment,
  },
};

const BarFunctionExecutionContext = {
  LexicalEnvironment: {
    FunctonEnvironmentRecord: {
      c: "c",
      ThisValue: global,
    },
    OuterEnvironmentReference: FooFunctionExecutionContext.LexicalEnvironment,
  },
};
```

GlobalLexicalEnvironment 내부에서는 BindingObject를 통해서 global의 console객체를 찾을 수 있으므로 이제 해당 console객체의 log 메서드를 최종적으로 실행하게됩니다. 이러한 원리를 통해서 자바스크립트의 스코프가 형성되며, 만약 외부 환경에 대한 참조가 null이 될때까지 원하는 값을 찾지 못한다면, 그때는 ReferenceError: {indetifier} is not defined가 발생하게 됩니다.

## 정리

실행 컨텍스트는 **_소스 코드를 실행하는데 필요한 환경을 제공하고, 코드의 실행 결과를 실제로 관리하는 영역_**입니다. 이 실행 컨텍스트를 통해서 스코프, 클로저 등의 동작과 코드의 실행 순서 관리가 구현됩니다. 실행 컨텍스트는 소스코드의 타입에 따라서 실행 컨텍스트를 생성하는 과정과 컨텍스트 내부에서 관리하는 내용이 달라집니다.

또한, **_실행 컨텍스트와 렉시컬 환경은 별도의 객체입니다._** 실행 컨텍스트에서 렉시컬 환경을 참조하고 있지만, 실행 컨텍스트가 종료된 후에도 해당 렉시컬 환경이 어딘가에 참조되고 있다면 렉시컬 환경은 가비지 컬렉팅 대상에서 제외됩니다. 이러한 동작으로 인해 클로저라는 개념이 성립되게 됩니다.

---

Reference : 모던 자바스크립트 Deep Dive,   
원티드 프론트엔드 프리온보딩 인턴쉽
https://pollen-port-115.notion.site/145ce592a18a40dabec08182ed6b4dbf
