# let, const, 블록 레벨 스코프

## var 키워드로 선언한 변수의 문제점

ES5까지 변수를 선언할 수 있는 유일한 방법은 var 키워드를 사용하는 것이었다. var 키워드로 선언된 변수는 다음과 같은 특징이 있다. 이는 다른 언어와는 구별되는 독특한 특징으로. 주의를 기울이지 않으면 심각한 문제를 발생시킬 수 있다.

### 변수 중복 선언 허용

var 키워드로 선언한 변수는 중복 선언이 가능하다.

```js
var x = 1;
var y = 1;

var x = 100;
var y; // 초기화문이 없는 변수 선언문은 무시

console.log(x); // 100
console.log(y); // 1
```

위 예제의 var 키워드로 선언한 x 변수와 y 변수는 중복 선언되었다. 이처럼 var 키워드로 선언한 변수를 중복 선언하면 초기화문 유무에 따라 다르게 동작한다. 초기와문이 있는 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작하고 초기화문이 없는 변수 선언문은 무시된다. 이때 에러는 발생하지 않는다.

### 함수 레벨 스코프

var 키워드로 선언한 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정한다. 따라서 함수 외부에서 var 키워드로 선언한 변수는 코드 블록 내에서 선언해도 모두 전역 변수가 된다.

```js
var x = 1;

if (true) {
  var x = 10;
}

console.log(x); // 10
```

for 문의 선언문에서 var 키워드로 선언한 변수도 전역 변수가 된다.

```js
var i = 10;

for (var i = 0; i < 5; i++) {
  console.log(i);
}

console.log(i); // 5
```

### 변수 호이스팅

var 키워드로 변수를 선언하면 변수 호이스팅에 의해 변수 선언문이 스코프의 선두로 끌어 올려진 것처럼 동작한다. 즉, 변수 호이스팅에 의해 var 키워드로 선언한 변수는 변수 선언문 이전에 참조할 수 있다. 단, 할당문 이전에 변수를 참조하면 언제나 undefined를 반환한다.

```js
console.log(foo); // undefined

foo = 123;

console.log(foo); // 123

var foo;
```

변수 선언문 이전에 변수를 참조하는 것은 변수 호이스팅에 의해 에러를 발생시키지는 않지만 프로그램의 흐름상 맞지 않을뿐더러 가독성을 떨어뜨리고 오류를 발생시킬 여지를 남긴다.

## let 키워드

앞에서 살펴본 var 키워드의 단점을 보완하기 위해 ES6에서는 새로운 변수 선언 키워드인 let과 const를 도입했다. var 키워드와의 차이점을 중심으로 let 키워드를 살펴보자.

### 변수 중복 선언 금지

var 키워드로 이름이 동일한 변수를 중복 선언하면 아무런 에러가 발생하지 않는다. 이때 변수를 중복 선언하면서 값까지 할당했다면 의도치 않게 먼저 선언된 변수 값이 재할당되어 변경되는 부작용이 발생한다.

```js
var foo = 123;
var foo = 456;
let bar = 123;
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared
```

### 블록 레벨 스코프

var 키워드로 선언한 변수는 오리지 함수의 코드 블록만을 지역 스코프로 인정하는 함수 레벨 스코프를 따른다. 하지만 let 키워드로 선언한 변수는 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.

```js
let foo = 1;

{
  let foo = 2;
  let bar = 3;
}

console.log(foo); // 1
console.log(bar); // ReferenceError: bar is not defined
```

### 변수 호이스팅

var 키워드로 선언한 변수와 달리 let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작한다.

```js
console.log(foo); // ReferenceError: foo is not defined
let foo;
```

이처럼 let 키워드로 선언한 변수를 변수 선언문 이전에 참조하면 참조 에러가 발생한다.

```js
let foo = 1; // 전역 변수

{
  console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
  let foo = 2; // 지역 변수
}
```

let 키워드로 선언한 변수의 경우 변수 호이스팅이 발생하지 않는다면 위 예제는 진역 변수 foo의 값을 출력해야한다. 하지만 let 키워드로 선언한 변수도 여전히 호이스팅이 발생하기 때문에 참조 에러가 발생한다.

자바스크립트는 es6에서 도입된 let, const를 포함해서 모든 선언(var, let, const, function, function\*, class)을 호이스팅한다. 단 let, const, class를 사용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작한다.

### 전역 객체와 let

var 키워드로 선언한 전역 변수와 전역 함수, 그리고 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역 객체 window의 프로퍼티가 된다. 전역 객체의 프로퍼티를 참조할 때 window를 생략할 수 있다.

```js
// 전역 변수
var x = 1;
// 암묵적 전역
y = 2;
// 전역 함수
function foo() {}

// var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티다.
console.log(window.x); // 1
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(x); // 1

// 암묵적 전역은 전역 객체 window의 프로퍼티다.
console.log(window.y); // 2
console.log(y); // 2

// 함수 선언문으로 정의한 전역 함수는 전역 객체 window의 프로퍼티다
console.log(window.foo); // foo() {}
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(foo);
```

let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. 즉, window.foo와 같이 접근할 수 없다. let 전역 변수는 보이지 않는 개념적인 블록 내에 존재한다.

```js
let x = 1;

console.log(window.x); // undefined
console.log(x); // 1
```

## const 키워드

const 키워드는 상수를 선언하기 위해 사용한다. 하지만 반드시 상수만을 위해 사용하지는 않는다. const 키워드의 특징은 let 키워드와 대부분 동일하다.

### 선언과 초기화

const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다.

```js
const foo = 1;
```

```js
const foo; // SyntaxError: Missing initializer in const declaration
```

const 키워드로 선언한 변수는 let 키워드로 선언한 변수와 마찬가지로 블록 레벨 스코프를 가지며, 변수 호이스팅이 발생하지 않는것처럼 동작한다.

```js
{
  console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
  const foo = 1;
  console.log(foo); // 1
}

console.log(foo); // ReferenceError: foo is not defined
```

### 재할당 금지

const 키워드로 선언한 변수는 재할당이 금지된다.

```js
const foo = 1;
foo = 2; // TypeError: Assignment to constant variable
```

### 상수

const 키워드로 선언한 변수에 원시 값을 할당한 경우 변수 값을 변경할 수 없다. 원시값은 변경 불가능한 값이므로 재할당 없이 값을 변경할 수 있는 방법이 없기 때문이다.

변수의 상대 개념인 상수는 재할당이 금지된 변수를 말한다.

### const 키워드와 객체

const 키워드로 선언된 변수에 원시 값ㅇ르 할당한 경우 값을 변경할 수 없다. 하지만 const 키워드로 선언하된 변수에 객체를 할당한 경우 값ㅇ르 변경할 수 있다. 변경 불가능한 값인 원시 값은 재할당 없이 변경할 수 있는 방법이 없지만 변경 가능한 값인 객체는 재할당 없이도 직접 변경이 가능하기 때문이다.

```js
const person = {
  name: "Lee",
};

person.name = "Kim";

console.log(person); // {name: 'Kim'}
```
