---
title: How to implement a promise-based API
slug: Learn/JavaScript/Asynchronous/Implementing_a_promise-based_API
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Asynchronous/Promises", "Learn/JavaScript/Asynchronous/Introducing_workers", "Learn/JavaScript/Asynchronous")}}

지난 글에서는 프로미스를 반환하는 API를 사용하는 방법에 대해 설명했습니다. 이번 글에서는 다른 측면, 즉 프로미스를 반환하는 API를 구현하는 방법을 살펴보겠습니다. 이는 프로미스 기반 API를 사용하는 것보다 훨씬 덜 일반적인 작업이지만 여전히 알아둘 가치가 있습니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        기본적인 컴퓨터 활용 능력, 이벤트 처리 및 프로미스의 기초를 포함한 자바스크립트 기본 사항에 대한 합리적인 이해.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>프로미스 기반 API를 구현하는 방법을 이해합니다.</td>
    </tr>
  </tbody>
</table>

일반적으로 프로미스 기반 API를 구현할 때는 이벤트, 일반 콜백 또는 메시지 전달 모델을 사용할 수 있는 비동기 작업을 래핑하게 됩니다. `Promise` 객체가 해당 작업의 성공 또는 실패를 적절히 처리하도록 준비합니다.

## alarm() API 구현하기

이 예제에서는 `alarm()`이라는 프로미스 기반 알람 API를 구현하겠습니다. 이 함수는 깨울 사람의 이름과 사람을 깨우기 전에 기다릴 지연 시간(밀리초)을 인자로 받습니다. 지연 시간이 지나면 함수는 깨워야 하는 사람의 이름을 포함하여 "일어나세요!" 메시지를 보냅니다.

### setTimeout() 래핑하기

`alarm()` 함수를 구현하기 위해 {{domxref("setTimeout()")}} API를 사용하겠습니다. `setTimeout()` API는 콜백 함수와 밀리초 단위로 지정된 지연을 인자로 받습니다. `setTimeout()`이 호출되면 지정된 지연으로 설정된 타이머를 시작하고 시간이 만료되면 지정된 함수를 호출합니다.

아래 예시에서는 콜백 함수와 1000밀리초의 지연을 사용하여 `setTimeout()`을 호출합니다:

```html
<button id="set-alarm">Set alarm</button>
<div id="output"></div>
```

```css hidden
div {
  margin: 0.5rem 0;
}
```

```js
const output = document.querySelector('#output');
const button = document.querySelector('#set-alarm');

function setAlarm() {
  setTimeout(() => {
    output.textContent = 'Wake up!';
  }, 1000);
}

button.addEventListener('click', setAlarm);
```

{{EmbedLiveSample("Wrapping setTimeout()", 600, 100)}}

### Promise() 생성자

`alarm()` 함수는 타이머가 만료될 때 이행되는 `Promise`를 반환합니다. 이 함수는 "Wake up!" 메시지를 `then()` 핸들러에 전달하고 호출자가 음수 지연 값을 제공하면 프로미스를 거부합니다.

여기서 핵심 구성 요소는 {{jsxref("Promise/Promise", "Promise()")}} 생성자입니다. `Promise()` 생성자는 하나의 함수를 인자로 받습니다. 이 함수를 `executor`라고 부르겠습니다. 새 프로미스를 생성할 때 executor의 구현을 제공하면 됩니다.

이 실행자 함수 자체는 두 개의 인수를 받는데, 둘 다 함수이며 일반적으로 `resolve` 및 `reject`라고 합니다. 실행자 구현에서는 기본 비동기 함수를 호출합니다. 비동기 함수가 성공하면 `resolve`를 호출하고, 실패하면 `reject`를 호출합니다. 실행자 함수가 오류를 던지면 자동으로 `reject` 함수가 호출됩니다. 모든 유형의 단일 매개변수를 `resolve`와 `reject`에 전달할 수 있습니다.

따라서 다음과 같이 `alarm()`을 구현할 수 있습니다:

```js
function alarm(person, delay) {
  return new Promise((resolve, reject) => {
    if (delay < 0) {
      throw new Error('Alarm delay must not be negative');
    }
    setTimeout(() => {
      resolve(`Wake up, ${person}!`);
    }, delay);
  });
}
```

이 함수는 새 `Promise`를 생성하고 반환합니다. 프로미스에 대한 실행자 내부에서 우리는

- `delay`이 음수가 아닌지 확인하고 음수인 경우 오류를 발생시킵니다.

- 콜백 및 `delay`을 전달하면서 `setTimeout()`을 호출합니다. 타이머가 만료되면 콜백이 호출되고, 콜백에서 `resolve`를 호출하여 "Wake up!" 메시지를 전달합니다.

## alarm() API 사용하기

이 부분은 지난 글에서 꽤 익숙할 것입니다. `alarm()`을 호출하고 반환된 프로미스에서 `then()` 및 `catch()`를 호출하여 프로미스 이행 및 거부에 대한 핸들러를 설정할 수 있습니다.

```html hidden
<div>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" size="4" value="Matilda" />
</div>

<div>
  <label for="delay">Delay:</label>
  <input type="text" id="delay" name="delay" size="4" value="1000" />
</div>

<button id="set-alarm">Set alarm</button>
<div id="output"></div>
```

```css hidden
button {
  display: block;
}

div,
button {
  margin: 0.5rem 0;
}
```

```js
const name = document.querySelector('#name');
const delay = document.querySelector('#delay');
const button = document.querySelector('#set-alarm');
const output = document.querySelector('#output');

function alarm(person, delay) {
  return new Promise((resolve, reject) => {
    if (delay < 0) {
      throw new Error('Alarm delay must not be negative');
    }
    setTimeout(() => {
      resolve(`Wake up, ${person}!`);
    }, delay);
  });
}

button.addEventListener('click', () => {
  alarm(name.value, delay.value)
    .then((message) => output.textContent = message)
    .catch((error) => output.textContent = `Couldn't set alarm: ${error}`);
});
```

{{EmbedLiveSample("Using the alarm() API", 600, 160)}}

"Name"과 "Delay"에 다른 값을 설정해 보세요. "Delay"에 음수 값을 설정해 보세요.

## API alarm() API로 async 및 await 사용

`alarm()`은 `Promise`를 반환하기 때문에 다른 프로미스로 할 수 있는 모든 것을 할 수 있습니다: 프로미스 체인, `Promise.all()`, `async` / `await`:

```html hidden
<div>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" size="4" value="Matilda" />
</div>

<div>
  <label for="delay">Delay:</label>
  <input type="text" id="delay" name="delay" size="4" value="1000" />
</div>

<button id="set-alarm">Set alarm</button>
<div id="output"></div>
```

```css hidden
button {
  display: block;
}

div,
button {
  margin: 0.5rem 0;
}
```

```js
const name = document.querySelector('#name');
const delay = document.querySelector('#delay');
const button = document.querySelector('#set-alarm');
const output = document.querySelector('#output');

function alarm(person, delay) {
  return new Promise((resolve, reject) => {
    if (delay < 0) {
      throw new Error('Alarm delay must not be negative');
    }
    setTimeout(() => {
      resolve(`Wake up, ${person}!`);
    }, delay);
  });
}

button.addEventListener('click', async () => {
  try {
    const message = await alarm(name.value, delay.value);
    output.textContent = message;
  }
  catch (error) {
    output.textContent = `Couldn't set alarm: ${error}`;
  }
});
```

{{EmbedLiveSample("Using async and await with the alarm() API", 600, 160)}}

## 참고 항목

- [`Promise()` 생성자](/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/Promise)
- [프로미스 사용하기](/ko/docs/Web/JavaScript/Guide/Using_promises)

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Asynchronous/Promises", "Learn/JavaScript/Asynchronous/Introducing_workers", "Learn/JavaScript/Asynchronous")}}
