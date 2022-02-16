# scope

스코프의 예시를 간단히 알아보고 시작하겠다.

```js
function add(x, y) {
  console.log(x, y); // 2 5
  return x + y;
}

add(2, 5);

console.log(x, y); // ReferenceError: x is not defined
```

이 코드는 당연하게 보일것이다.
x와 y는 함수 add의 매개변수이므로 유효범위 즉 스코프는 add 함수 내부이다.
이처럼 스코프란 유효범위를 뜻한다

```js
var var1 = 1;

if (true) {
  var var2 = 2;
  if (true) {
    var var3 = 3;
  }
}

function foo() {
  var var4 = 4;

  function bar() {
    var var5 = 5;
  }
}

console.log(var1); // 1
console.log(var2); // 2
console.log(var3); // 3
console.log(var4); // ReferenceError: var4 is not defined
console.log(var5); // ReferenceError: var5 is not defined
```

이처럼 다시 말해 모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 이를 스코프라 한다. 즉 스코프는 식별자가 유효한 범위를 말한다.

```js
var x = "global";

function foo() {
  var x = "local";
  console.log(x); // 1
}

foo();

console.log(x); // 2
```

다음 코드는 바깥 영역과 foo 함수 내부에 같은 이름에 갖는 x 변수를 선언했을 때 1과 2에서 x 변수를 참조한다.  
이때 자바스크립트 엔진은 이름이 같은 두 개의 변수 중에서 어떤 변수를 참조해야 할 것인지를 결정해야한다. 이를 식별자 결정(identifier resolution)이라 한다. 자바스크립트 엔진은 스코프를 통해 어떤 변수를 참조해야 할 것인지 결정한다. 따라서 스코프란 자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙이라고도 할 수 있다.

자바스크립트 엔진은 코드를 실행할 때 코드의 문맥(context)을 고려한다. 코드가 어디서 실행되며 주변에 어떤 코드가 있는지에 따라 위 예제의 1과 2처럼 동일한 코드도 다른 결과를 만들어 낸다.

위 예제에서 코드의 가장 바깥 영역에 선언된 x 변수는 어디서든 참조할 수 있다. 하지만 foo 함수 내부에서 선언된 x 변수는 foo 함수 내부에서만 참조할 수 있고 foo 함수 외부에서는 참조할 수 없다. 이때 두 개의 x 변수는 식별자 이름이 동일하지만 자신이 유효한 범위, 즉 스코프가 다른 별개의 변수다.

만약 스코프라는 개념이 없다면 같은 이름을 갖는 변수는 충돌을 일으키므로 프로그램 전체에서 하나밖에 사용할 수 없다.

var 키워드로 변수를 선언하면 중복 선언이 허용된다. 이는 의도치 않게 변수값이 재할당되어 변경되는 부작용을 발생시킨다.

```js
function foo() {
  var x = 1;
  var x = 2;
  console.log(x); // 2
}

function bar() {
  let x = 1;
  let x = 2; // SyntaxError: Identifier 'x' has already been declared
}
```

## 스코프의 종류
