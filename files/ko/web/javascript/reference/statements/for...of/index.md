---
title: for...of
slug: Web/JavaScript/Reference/Statements/for...of
page-type: javascript-statement
browser-compat: javascript.statements.for_of
---

{{jsSidebar("Statements")}}

**`for...of`** 문은 [이터러블 객체](/ko/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)에서 가져온 값의 시퀀스에 대해 연산하는 루프를 실행합니다. 이터러블 객체에는 {{jsxref("Array")}}, {{jsxref("String")}}, {{jsxref("TypedArray")}}, {{jsxref("Map")}}, {{jsxref("Set")}}, {{domxref("NodeList")}}(및 기타 DOM 컬렉션)와 같은 내장 객체의 인스턴스와 {{jsxref("Functions/arguments", "arguments")}} 객체, [Generator function](/ko/docs/Web/JavaScript/Reference/Statements/function*)에 의해 생성된 [Generator](/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator), 사용자 정의 이터러블이 포함됩니다.

{{EmbedInteractiveExample("pages/js/statement-forof.html")}}

## Syntax

```js-nolint
for (variable of iterable)
  statement
```

- `variable`
  - : 각 반복마다 시퀀스에서 값을 받습니다. [`const`](/ko/docs/Web/JavaScript/Reference/Statements/const), [`let`](/ko/docs/Web/JavaScript/Reference/Statements/let), [`var`](/ko/docs/Web/JavaScript/Reference/Statements/var)가 포함된 선언이거나 [할당](/ko/docs/Web/JavaScript/Reference/Operators/Assignment) 대상(예: 이전에 선언된 변수 또는 객체 프로퍼티)일 수 있습니다.
- `iterable`
  - : 이터러블 객체입니다. 루프가 작동하는 값 시퀀스의 소스입니다.
- `statement`
  - : 모든 반복에서 실행할 문입니다. `variable`을 참조할 수 있습니다. [블록 문](/ko/docs/Web/JavaScript/Reference/Statements/block)을 사용하여 여러 문을 실행할 수 있습니다.

## 설명

`for...of` 루프는 이터러블에서 가져온 값에 대해 순차적으로 하나씩 연산합니다. 값에 대한 루프의 각 연산을 이터레이션이라고 하며, 루프는 이터러블을 반복한다고 합니다. 각 반복은 현재 시퀀스 값을 참조할 수 있는 문을 실행합니다.

`for...of` 루프가 이터러블을 반복할 때는 먼저 이터러블의 [`[@@iterator]()`](/ko/docs/Web/JavaScript/Reference/Global_Objects/Symbol/iterator) 메서드를 호출하여 [iterator](/ko/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol)를 반환한 다음 결과 iterator의 [`next()`](/ko/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol) 메서드를 반복적으로 호출하여 `variable`에 할당할 값의 시퀀스를 생성합니다.

iterator가 완료되면 `for...of` 루프가 종료됩니다(iterator의 `next()` 메서드는 `done: true`를 포함하는 객체를 반환합니다). 제어 흐름 문을 사용하여 일반적인 제어 흐름을 변경할 수도 있습니다. [`break`](/ko/docs/Web/JavaScript/Reference/Statements/break)는 루프를 종료하고 루프 본문 뒤의 첫 번째 문으로 이동하며, [`continue`](/ko/docs/Web/JavaScript/Reference/Statements/continue)는 현재 반복의 나머지 문을 건너뛰고 다음 반복으로 진행합니다.

`for...of` 루프가 일찍 종료되는 경우(예: `break` 문이 발생하거나 오류가 발생하는 경우) iterator의 [`return()`](/ko/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol) 메서드가 호출되어 정리를 수행합니다.

`for...of` 의 `variable` 부분은 `=` 연산자 앞에 올 수 있는 모든 것을 허용합니다. 변수가 루프 본문 내에서 재할당되지 않는 한 {{jsxref("Statements/const", "const")}}를 사용하여 변수를 선언할 수 있습니다(두 변수는 별개의 변수이므로 반복 사이에 변경될 수 있습니다). 그렇지 않으면 {{jsxref("Statements/let", "let")}}을 사용할 수 있습니다.

```js
const iterable = [10, 20, 30];

for (let value of iterable) {
  value += 1;
  console.log(value);
}
// 11
// 21
// 31
```

> **참고:** 반복할 때마다 새 변수가 생성됩니다. 루프 본문 내에서 변수를 재할당해도 이터러블(이 경우 배열)의 원래 값에는 영향을 주지 않습니다.

[destructuring](/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)이나 `for (x.y of iterable)`과 같은 객체 프로퍼티를 사용할 수도 있습니다.

그러나 특수 규칙에 따라 변수 이름으로 `async`를 사용하는 것은 금지되어 있습니다. 이는 잘못된 구문입니다:

```js example-bad
let async;
for (async of [1, 2, 3]); // SyntaxError: for-of 루프의 왼쪽은 'async'가 아닐 겁니다.
```

이는 [`for`](/ko/docs/Web/JavaScript/Reference/Statements/for) 루프인 `for (async of => {};;)`의 유효한 코드와의 구문 모호성을 피하기 위한 것입니다.

## 예제

### 배열 반복하기

```js
const iterable = [10, 20, 30];

for (const value of iterable) {
  console.log(value);
}
// 10
// 20
// 30
```

### 문자열 반복하기

문자열은 [유니코드 코드 포인트별로 반복](/ko/docs/Web/JavaScript/Reference/Global_Objects/String/@@iterator)됩니다.

```js
const iterable = "boo";

for (const value of iterable) {
  console.log(value);
}
// "b"
// "o"
// "o"
```

### TypedArray 반복하기

```js
const iterable = new Uint8Array([0x00, 0xff]);

for (const value of iterable) {
  console.log(value);
}
// 0
// 255
```

### 맵 반복하기

```js
const iterable = new Map([
  ["a", 1],
  ["b", 2],
  ["c", 3],
]);

for (const entry of iterable) {
  console.log(entry);
}
// ['a', 1]
// ['b', 2]
// ['c', 3]

for (const [key, value] of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```

### Set 반복하기

```js
const iterable = new Set([1, 1, 2, 2, 3, 3]);

for (const value of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```

### arguments 객체 반복하기

{{jsxref("Functions/arguments", "arguments")}} 객체를 반복하여 함수에 전달된 모든 매개변수를 검사할 수 있습니다.

```js
function foo() {
  for (const value of arguments) {
    console.log(value);
  }
}

foo(1, 2, 3);
// 1
// 2
// 3
```

### NodeList 반복하기

다음 예는 [`NodeList`](/ko/docs/Web/API/NodeList) DOM 컬렉션을 반복하여 [`<article>`](/ko/docs/Web/HTML/Element/article) 요소의 직계 자손인 paragraph들에 `read` 클래스를 추가하는 예제입니다.

```js
const articleParagraphs = document.querySelectorAll("article > p");
for (const paragraph of articleParagraphs) {
  paragraph.classList.add("read");
}
```

### 사용자 정의 이터러블 반복하기

사용자 정의 이터레이터를 반환하는 `@@iterator` 메서드를 사용하여 객체를 반복합니다:

```js
const iterable = {
  [Symbol.iterator]() {
    let i = 1;
    return {
      next() {
        if (i <= 3) {
          return { value: i++, done: false };
        }
        return { value: undefined, done: true };
      },
    };
  },
};

for (const value of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```

`@@iterator` generator 메서드를 사용하여 객체를 이터레이션합니다:

```js
const iterable = {
  *[Symbol.iterator]() {
    yield 1;
    yield 2;
    yield 3;
  },
};

for (const value of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```

반복 가능한 이터레이터(`this`를 반환하는 `[@@iterator]()` 메서드가 있는 이터레이터)는 `for...of`와 같이 이터러블을 기대하는 구문에서 이터레이터를 사용할 수 있도록 하는 매우 일반적인 기법입니다.

```js
let i = 1;

const iterator = {
  next() {
    if (i <= 3) {
      return { value: i++, done: false };
    }
    return { value: undefined, done: true };
  },
  [Symbol.iterator]() {
    return this;
  },
};

for (const value of iterator) {
  console.log(value);
}
// 1
// 2
// 3
```

### generator 반복하기

```js
function* source() {
  yield 1;
  yield 2;
  yield 3;
}

const generator = source();

for (const value of generator) {
  console.log(value);
}
// 1
// 2
// 3
```

### 조기 종료

첫 번째 루프에서 `break` 문을 실행하면 루프가 조기 종료됩니다. iterator가 아직 완료되지 않았으므로 두 번째 루프는 첫 번째 루프가 중지된 지점에서 계속됩니다.

```js
const source = [1, 2, 3];

const iterator = source[Symbol.iterator]();

for (const value of iterator) {
  console.log(value);
  if (value === 1) {
    break;
  }
  console.log("이 문자열은 로그에 기록되지 않습니다.");
}
// 1

// 동일한 반복자를 사용하는 다른 루프는
// 마지막 루프가 중단된 지점에서 시작됩니다.
for (const value of iterator) {
  console.log(value);
}
// 2
// 3

// iterator가 모두 사용됩니다.
// 이 루프는 반복을 실행하지 않습니다.
for (const value of iterator) {
  console.log(value);
}
// [No output]
```

제너레이터는 [`return()`](/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator/return) 메서드를 구현하여 루프가 종료될 때 제너레이터 함수가 조기에 반환되도록 합니다. 따라서 루프 간에 제너레이터를 재사용할 수 없습니다.

```js example-bad
function* source() {
  yield 1;
  yield 2;
  yield 3;
}

const generator = source();

for (const value of generator) {
  console.log(value);
  if (value === 1) {
    break;
  }
  console.log("이 문자열은 로그에 기록되지 않습니다.");
}
// 1

// generator가 모두 사용됩니다.
// 이 루프는 반복을 실행하지 않습니다.
for (const value of generator) {
  console.log(value);
}
// [No output]
```

### for...of와 for...in의 차이점

`for...in`과 `for...of` 문은 모두 어떤 대상을 반복합니다. 이 둘의 주요 차이점은 반복하는 대상에 있습니다.

{{jsxref("Statements/for...in", "for...in")}} 문은 객체의 [열거 가능한 문자열 속성](/ko/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)을 반복하는 반면, `for...of` 문은 [이터러블 객체](/ko/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)가 반복하도록 정의한 값에 대해 반복합니다.

다음 예제는 {{jsxref("Array")}}와 함께 사용할 때 `for...of` 루프와 `for...in` 루프의 차이점을 보여줍니다.

```js
Object.prototype.objCustom = function () {};
Array.prototype.arrCustom = function () {};

const iterable = [3, 5, 7];
iterable.foo = "hello";

for (const i in iterable) {
  console.log(i);
}
// "0", "1", "2", "foo", "arrCustom", "objCustom"

for (const i in iterable) {
  if (Object.hasOwn(iterable, i)) {
    console.log(i);
  }
}
// "0" "1" "2" "foo"

for (const i of iterable) {
  console.log(i);
}
// 3 5 7
```

객체 `iterable`은 [prototype chain](/ko/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)에 `Object.prototype`과 `Array.prototype`을 모두 포함하므로 객체 이터러블은 `objCustom`과 `arrCustom` 속성을 상속합니다.

`for...in` 루프는 `iterable` 객체의 [enumerable 속성](/ko/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)만 로깅합니다. 배열 요소 `3`, `5`, `7` 또는 `"hello"`는 프로퍼티가 아니라 값이기 때문에 로깅하지 않습니다. 배열 인덱스는 물론 실제 프로퍼티인 arrCustom과 objCustom도 기록합니다. 이러한 프로퍼티가 왜 반복되는지 잘 모르겠다면 [배열 반복과 `for...in`](/ko/docs/Web/JavaScript/Reference/Statements/for...in#array_iteration_and_for...in)이 어떻게 작동하는지에 대한 자세한 설명이 나와 있습니다.

두 번째 루프는 첫 번째 루프와 비슷하지만, 찾은 열거 가능한 프로퍼티가 객체 자체의 프로퍼티인지, 즉 상속되지 않았는지 확인하기 위해 O{{jsxref("Object.hasOwn()")}}을 사용합니다. 만약 그렇다면 프로퍼티가 기록됩니다. 속성 `0`, `1`, `2` 및 `foo`는 자체 속성이므로 로깅됩니다. `arrCustom` 및 `objCustom` 속성은 상속되었기 때문에 기록되지 않습니다.

`for...of` 루프는 반복할 수 있는 배열([iterable](/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/@@iterator))로 정의된 값을 반복하고 기록합니다. 객체의 "요소" `3`, `5`, `7`은 표시되지만 객체의 "속성"은 표시되지 않습니다.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{jsxref("Array.prototype.forEach()")}}
- {{jsxref("Map.prototype.forEach()")}}
- {{jsxref("Object.entries()")}} – Useful when using `for...of` over an object.
