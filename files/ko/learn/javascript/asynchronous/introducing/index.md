---
title: Introducing asynchronous JavaScript
slug: Learn/JavaScript/Asynchronous/Introducing
---

{{LearnSidebar}}{{NextMenu("Learn/JavaScript/Asynchronous/Promises", "Learn/JavaScript/Asynchronous")}}

이 글에서는 비동기 프로그래밍이 무엇인지, 왜 비동기 프로그래밍이 필요한지 설명하고, 비동기 함수가 자바스크립트에서 역사적으로 구현된 몇 가지 방법에 대해 간략하게 설명합니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        기본적인 컴퓨터 활용 능력, 함수 및 이벤트 핸들러를 포함한 JavaScript 기본 사항에 대한 합리적인 이해.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        비동기 자바스크립트가 무엇인지, 동기 자바스크립트와 어떻게 다른지, 왜 비동기 자바스크립트가 필요한지 숙지합니다.
      </td>
    </tr>
  </tbody>
</table>

비동기 프로그래밍은 잠재적으로 오래 실행될 수 있는 작업을 시작하면서도 해당 작업이 완료될 때까지 기다릴 필요 없이 해당 작업이 실행되는 동안 다른 이벤트에 계속 반응할 수 있도록 하는 기술입니다. 해당 작업이 완료되면 프로그램에 결과가 표시됩니다.

브라우저에서 제공하는 많은 기능, 특히 가장 흥미로운 기능은 잠재적으로 시간이 오래 걸릴 수 있으므로 비동기식입니다. 예를 들어

- {{domxref("fetch", "fetch()")}} 를 사용한 HTTP 요청 만들기
- {{domxref("MediaDevices/getUserMedia", "getUserMedia()")}} 를 사용하여 사용자의 카메라 또는 마이크에 액세스하기
- {{domxref("window/showOpenFilePicker", "showOpenFilePicker()")}} 를 사용하여 사용자에게 파일 선택 요청하기

따라서 비동기 함수를 자주 구현할 필요는 없더라도 올바르게 사용해야 할 가능성이 매우 높습니다.

이 글에서는 비동기 프로그래밍을 필수로 만드는 장기 실행 동기 함수의 문제점을 살펴보는 것부터 시작하겠습니다.

## 동기식 프로그래밍

다음 코드를 살펴봅시다:

```js
const name = 'Miriam';
const greeting = `Hello, my name is ${name}!`;
console.log(greeting);
// "Hello, my name is Miriam!"
```

이 코드는:

1. `name`이라는 문자열을 선언합니다.
2. `name`을 사용하는 `greeting`이라는 또 다른 문자열을 선언합니다.
3. 인사말을 자바스크립트 콘솔에 출력합니다.

여기서 주목할 점은 브라우저는 프로그램을 작성한 순서대로 한 번에 한 줄씩 효과적으로 실행한다는 것입니다. 각 지점에서 브라우저는 다음 줄로 넘어가기 전에 해당 줄이 작업을 완료할 때까지 기다립니다. 각 줄은 이전 줄에서 수행한 작업에 따라 달라지기 때문에 이렇게 해야 합니다.

이것이 바로 **동기식 프로그램** 입니다. 이렇게 별도의 함수를 호출해도 여전히 동기식입니다:

```js
function makeGreeting(name) {
  return `Hello, my name is ${name}!`;
}

const name = 'Miriam';
const greeting = makeGreeting(name);
console.log(greeting);
// "Hello, my name is Miriam!"
```

호출자는 함수가 작업을 완료하고 값을 반환할 때까지 기다려야 계속할 수 있기 때문에 여기서 `makeGreeting()`은 **동기식 함수** 입니다.

### 오래 실행되는 동기 함수

동기 함수가 시간이 오래 걸리면 어떻게 될까요?

아래 프로그램은 매우 비효율적인 알고리즘을 사용하여 사용자가 "Generate primes"(소수 생성) 버튼을 클릭할 때 여러 개의 큰 소수를 생성합니다. 사용자가 지정하는 소수의 수가 많을수록 연산 시간이 더 오래 걸립니다.

```html
<label for="quota">Number of primes:</label>
<input type="text" id="quota" name="quota" value="1000000" />

<button id="generate">Generate primes</button>
<button id="reload">Reload</button>

<div id="output"></div>
```

```js
const MAX_PRIME = 1000000;

function isPrime(n) {
  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
      return false;
    }
  }
  return n > 1;
}

const random = (max) => Math.floor(Math.random() * max);

function generatePrimes(quota) {
  const primes = [];
  while (primes.length < quota) {
    const candidate = random(MAX_PRIME);
    if (isPrime(candidate)) {
      primes.push(candidate);
    }
  }
  return primes;
}

const quota = document.querySelector('#quota');
const output = document.querySelector('#output');

document.querySelector('#generate').addEventListener('click', () => {
  const primes = generatePrimes(quota.value);
  output.textContent = `Finished generating ${quota.value} primes!`;
});

document.querySelector('#reload').addEventListener('click', () => {
  document.location.reload();
});
```

{{EmbedLiveSample("A long-running synchronous function", 600, 120)}}

"Generate primes"을 클릭해 보세요. 컴퓨터의 속도에 따라 프로그램에 "Finished!" 메시지가 표시되기까지 몇 초 정도 걸릴 수 있습니다.

### 장기 실행 동기 함수의 문제점

다음 예제는 사용자가 입력할 텍스트 상자를 추가했다는 점을 제외하면 마지막 예제와 같습니다. 이번에는 "Generate primes"을 클릭하고 바로 뒤에 있는 텍스트 상자에 입력해 보세요.

`generatePrimes()` 함수가 실행되는 동안 프로그램이 완전히 응답하지 않는 것을 알 수 있습니다. 아무 것도 입력하거나 클릭하거나 다른 작업을 할 수 없습니다.

```html hidden
<label for="quota">Number of primes:</label>
<input type="text" id="quota" name="quota" value="1000000" />

<button id="generate">Generate primes</button>
<button id="reload">Reload</button>

<textarea id="user-input" rows="5" cols="62">
Try typing in here immediately after pressing "Generate primes"
</textarea>

<div id="output"></div>
```

```css hidden
textarea {
  display: block;
  margin: 1rem 0;
}
```

```js hidden
const MAX_PRIME = 1000000;

function isPrime(n) {
  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
      return false;
    }
  }
  return n > 1;
}

const random = (max) => Math.floor(Math.random() * max);

function generatePrimes(quota) {
  const primes = [];
  while (primes.length < quota) {
    const candidate = random(MAX_PRIME);
    if (isPrime(candidate)) {
      primes.push(candidate);
    }
  }
  return primes;
}

const quota = document.querySelector('#quota');
const output = document.querySelector('#output');

document.querySelector('#generate').addEventListener('click', () => {
  const primes = generatePrimes(quota.value);
  output.textContent = `Finished generating ${quota.value} primes!`;
});

document.querySelector('#reload').addEventListener('click', () => {
  document.location.reload();
});
```

{{EmbedLiveSample("The trouble with long-running synchronous functions", 600, 200)}}

이것이 장기 실행 동기 함수의 기본적인 문제입니다. 우리에게 필요한 것은 프로그램을 실행할 수 있는 방법입니다:

1. 함수를 호출하여 장기 실행 작업을 시작합니다.
2. 해당 함수가 연산을 시작하고 즉시 반환하도록 하여 프로그램이 다른 이벤트에 계속 반응할 수 있도록 합니다.
3. 연산이 완료되면 그 결과를 알려줍니다.

이것이 바로 비동기 함수가 할 수 있는 일입니다. 이 모듈의 나머지 부분에서는 비동기 함수가 자바스크립트에서 어떻게 구현되는지 설명합니다.

## 이벤트 핸들러

방금 살펴본 비동기 함수에 대한 설명은 이벤트 핸들러를 떠올리게 할 수 있으며, 그렇다면 맞을 것입니다. 이벤트 핸들러는 실제로 비동기 프로그래밍의 한 형태입니다. 즉시 호출되는 것이 아니라 이벤트가 발생할 때마다 호출될 함수(이벤트 핸들러)를 제공하는 것입니다. "이벤트"가 "비동기 작업이 완료됨"인 경우 해당 이벤트를 사용하여 호출자에게 비동기 함수 호출의 결과를 알릴 수 있습니다.

일부 초기 비동기 API는 이러한 방식으로 이벤트를 사용했습니다. {{domxref("XMLHttpRequest")}} API를 사용하면 JavaScript를 사용하여 원격 서버에 HTTP 요청을 할 수 있습니다. 이 작업은 시간이 오래 걸릴 수 있으므로 비동기 API이며, 이벤트 리스너를 `XMLHttpRequest` 객체에 연결하여 요청의 진행 상황과 최종 완료에 대한 알림을 받습니다.

다음 예는 실제로 작동하는 모습을 보여줍니다. 요청을 보내려면 "Click to start request"을 누릅니다. 새 {{domxref("XMLHttpRequest")}} 를 생성하고 {{domxref("XMLHttpRequest/loadend_event", "loadend")}} 이벤트를 수신 대기합니다. 핸들러는 상태 코드와 함께 "Finished!" 메시지를 기록합니다.

이벤트 리스너를 추가한 후 요청을 전송합니다. 이 후 "Started XHR request"를 기록할 수 있습니다. 즉, 요청이 진행되는 동안 프로그램이 계속 실행될 수 있으며 요청이 완료되면 이벤트 핸들러가 호출된다는 점에 유의하세요.

```html
<button id="xhr">Click to start request</button>
<button id="reload">Reload</button>

<pre readonly class="event-log"></pre>
```

```css hidden
pre {
  display: block;
  margin: 1rem 0;
}
```

```js
const log = document.querySelector('.event-log');

document.querySelector('#xhr').addEventListener('click', () => {
  log.textContent = '';

  const xhr = new XMLHttpRequest();

  xhr.addEventListener('loadend', () => {
    log.textContent = `${log.textContent}Finished with status: ${xhr.status}`;
  });

  xhr.open('GET', 'https://raw.githubusercontent.com/mdn/content/main/files/en-us/_wikihistory.json');
  xhr.send();
  log.textContent = `${log.textContent}Started XHR request\n`;});

document.querySelector('#reload').addEventListener('click', () => {
  log.textContent = '';
  document.location.reload();
});
```

{{EmbedLiveSample("Event handlers", 600, 120)}}

이는 [이전 모듈에서 살펴본 이벤트 핸들러](/ko/docs/Learn/JavaScript/Building_blocks/Events) 와 비슷하지만, 사용자가 버튼을 클릭하는 것과 같은 사용자 액션이 아닌 일부 객체의 상태 변경이라는 점이 다릅니다.

## 콜백

이벤트 핸들러는 콜백의 특정 유형입니다. 콜백은 적절한 시점에 콜백이 호출될 것으로 기대하면서 다른 함수에 전달되는 함수일 뿐입니다. 방금 살펴본 것처럼 콜백은 자바스크립트에서 비동기 함수를 구현하는 주요 방식이었습니다.

하지만 콜백 기반 코드는 콜백 자체가 콜백을 받는 함수를 호출해야 할 때 이해하기 어려울 수 있습니다. 이는 일련의 비동기 함수로 나뉘는 일부 연산을 수행해야 하는 경우 흔히 발생하는 상황입니다. 예를 들어 다음을 생각해 보세요:

```js
function doStep1(init) {
  return init + 1;
}

function doStep2(init) {
  return init + 2;
}

function doStep3(init) {
  return init + 3;
}

function doOperation() {
  let result = 0;
  result = doStep1(result);
  result = doStep2(result);
  result = doStep3(result);
  console.log(`result: ${result}`);
}

doOperation();
```

여기서는 단일 연산이 세 단계로 나뉘며, 각 단계는 마지막 단계에 따라 달라집니다. 이 예제에서 첫 번째 단계는 입력에 1을 더하고, 두 번째 단계는 2를 더하고, 세 번째 단계는 3을 더합니다. 0의 입력으로 시작하여 최종 결과는 6(0 + 1 + 2 + 3)입니다. 동기식 프로그램으로서 이것은 매우 간단합니다. 하지만 콜백을 사용하여 단계를 구현하면 어떨까요?

```js
function doStep1(init, callback) {
  const result = init + 1;
  callback(result);
}

function doStep2(init, callback) {
  const result = init + 2;
  callback(result);
}

function doStep3(init, callback) {
  const result = init + 3;
  callback(result);
}

function doOperation() {
  doStep1(0, (result1) => {
    doStep2(result1, (result2) => {
      doStep3(result2, (result3) => {
        console.log(`result: ${result3}`);
      });
    });
  });
}

doOperation();
```

콜백 내부에서 콜백을 호출해야 하기 때문에 깊게 중첩된 `doOperation()` 함수를 얻게 되는데, 이는 읽고 디버깅하기가 훨씬 더 어렵습니다. 이를 "콜백 지옥" 또는 "파멸의 피라미드"라고 부르기도 합니다(들여쓰기가 옆으로 피라미드처럼 보이기 때문입니다).

이렇게 콜백을 중첩하면 최상위 수준에서 한 번만 오류를 처리하는 대신 "피라미드"의 각 수준에서 오류를 처리해야 하는 경우가 많아 오류 처리가 매우 어려워질 수 있습니다.

이러한 이유로 대부분의 최신 비동기 API는 콜백을 사용하지 않습니다. 대신 자바스크립트 비동기 프로그래밍의 기초는 프로미스이며, 다음 글의 주제는 프로미스({{jsxref("Promise")}})입니다.

{{NextMenu("Learn/JavaScript/Asynchronous/Promises", "Learn/JavaScript/Asynchronous")}}
