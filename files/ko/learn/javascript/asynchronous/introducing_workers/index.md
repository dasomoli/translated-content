---
title: Introducing workers
slug: Learn/JavaScript/Asynchronous/Introducing_workers
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Asynchronous/Implementing_a_promise-based_API", "Learn/JavaScript/Asynchronous/Sequencing_animations", "Learn/JavaScript/Asynchronous")}}

이번 '비동기 자바스크립트' 모듈의 마지막 글에서는 별도의 실행 {{Glossary("Thread", "thread")}}에서 일부 작업을 실행할 수 있는 워커를 소개합니다.

<table>
  <tbody>
    <tr>
      <th scope="row">전제 조건:</th>
      <td>
        기본적인 컴퓨터 활용 능력, 이벤트 처리를 포함한 자바스크립트 기본 사항에 대한 합리적인 이해.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>웹 워커를 사용하는 방법을 이해합니다.</td>
    </tr>
  </tbody>
</table>

이 모듈의 첫 번째 글에서는 프로그램에서 장기간 실행되는 동기식 작업이 있을 때 전체 창이 완전히 응답하지 않을 때 어떤 일이 발생하는지 살펴봤습니다. 근본적으로 그 이유는 프로그램이 단일 스레드이기 때문입니다. 스레드는 프로그램이 따르는 일련의 명령어입니다. 프로그램은 단일 스레드로 구성되어 있기 때문에 한 번에 한 가지 작업만 수행할 수 있으므로 장기 실행 동기 호출이 반환되기를 기다리는 동안에는 다른 작업을 수행할 수 없습니다.

워커는 다른 스레드에서 일부 작업을 실행할 수 있는 기능을 제공하므로 작업을 시작한 다음 다른 처리(예: 사용자 작업 처리)를 계속할 수 있습니다.

하지만 여기에는 대가가 따릅니다. 멀티스레드 코드를 사용하면 언제 내 스레드가 일시 중단되고 다른 스레드가 실행될 기회를 얻을지 알 수 없습니다. 따라서 두 스레드가 동일한 변수에 액세스할 수 있는 경우 변수가 언제든지 예기치 않게 변경될 수 있으며, 이로 인해 찾기 어려운 버그가 발생할 수 있습니다.

웹에서 이러한 문제를 방지하기 위해 메인 코드와 워커 코드는 서로의 변수에 직접 액세스하지 않습니다. 워커 코드와 메인 코드는 완전히 분리된 세계에서 실행되며 서로 메시지를 보내는 방식으로만 상호 작용합니다. 특히, 이는 워커가 DOM(창, 문서, 페이지 요소 등)에 액세스할 수 없음을 의미합니다.

워커에는 세 가지 종류가 있습니다:

- 전용 워커
- 공유 워커
- 서비스 워커

이 문서에서는 첫 번째 유형의 작업자의 예를 살펴본 다음 나머지 두 가지 유형에 대해 간략하게 설명합니다.

## 웹 워커 사용

첫 번째 글에서 소수를 계산하는 페이지를 만들었던 것을 기억하시나요? 소수 계산을 실행하는 데 워커를 사용하여 페이지가 사용자 동작에 반응하는 상태를 유지하도록 하겠습니다.

### 동기식 소수 생성기

먼저 이전 예제의 자바스크립트를 다시 한 번 살펴봅시다:

```js
function generatePrimes(quota) {

  function isPrime(n) {
    for (let c = 2; c <= Math.sqrt(n); ++c) {
      if (n % c === 0) {
          return false;
       }
    }
    return true;
  }

  const primes = [];
  const maximum = 1000000;

  while (primes.length < quota) {
    const candidate = Math.floor(Math.random() * (maximum + 1));
    if (isPrime(candidate)) {
      primes.push(candidate);
    }
  }

  return primes;
}

document.querySelector('#generate').addEventListener('click', () => {
  const quota = document.querySelector('#quota').value;
  const primes = generatePrimes(quota);
  document.querySelector('#output').textContent = `Finished generating ${quota} primes!`;
});

document.querySelector('#reload').addEventListener('click', () => {
  document.querySelector('#user-input').value = 'Try typing in here immediately after pressing "Generate primes"';
  document.location.reload();
});
```

이 프로그램에서 `generatePrimes()`를 호출한 후에는 프로그램이 완전히 응답하지 않습니다.

### 워커를 사용한 프라임 생성

이 예제에서는 <https://github.com/mdn/learning-area/blob/main/javascript/asynchronous/workers/start> 에서 파일의 로컬 복사본을 만드는 것으로 시작합니다. 이 디렉토리에는 4개의 파일이 있습니다:

- index.html
- style.css
- main.js
- generate.js

"index.html" 파일과 "style.css" 파일은 이미 완성되었습니다:

```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>Prime numbers</title>
    <script src="main.js" defer></script>
    <link href="style.css" rel="stylesheet" />
  </head>

  <body>
    <label for="quota">Number of primes:</label>
    <input type="text" id="quota" name="quota" value="1000000" />

    <button id="generate">Generate primes</button>
    <button id="reload">Reload</button>

    <textarea id="user-input" rows="5" cols="62">
Try typing in here immediately after pressing "Generate primes"
</textarea>

    <div id="output"></div>
  </body>
</html>
```

```css
textarea {
  display: block;
  margin: 1rem 0;
}
```

"main.js" 및 "generate.js" 파일은 비어 있습니다. 메인 코드는 "main.js"에, 워커 코드는 "generate.js"에 추가하겠습니다

먼저, 워커 코드가 메인 코드와 별도의 스크립트에 보관되어 있음을 알 수 있습니다. 또한 위의 "index.html"을 보면 메인 코드만 `<script>` 요소에 포함되어 있음을 알 수 있습니다.

이제 다음 코드를 "main.js"에 복사합니다:

```js
// Create a new worker, giving it the code in "generate.js"
const worker = new Worker('./generate.js');

// When the user clicks "Generate primes", send a message to the worker.
// The message command is "generate", and the message also contains "quota",
// which is the number of primes to generate.
document.querySelector('#generate').addEventListener('click', () => {
  const quota = document.querySelector('#quota').value;
  worker.postMessage({
    command: 'generate',
    quota,
  });
});

// When the worker sends a message back to the main thread,
// update the output box with a message for the user, including the number of
// primes that were generated, taken from the message data.
worker.addEventListener('message', (message) => {
  document.querySelector('#output').textContent = `Finished generating ${message.data} primes!`;
});

document.querySelector('#reload').addEventListener('click', () => {
  document.querySelector('#user-input').value = 'Try typing in here immediately after pressing "Generate primes"';
  document.location.reload();
});
```

- 먼저 {{domxref("Worker/Worker", "Worker()")}} 생성자를 사용하여 워커를 생성합니다. 그리고 워커 스크립트를 가리키는 URL을 전달합니다. 워커가 생성되자마자 워커 스크립트가 실행됩니다.

- 다음으로 동기식 버전에서와 마찬가지로 "Generate primes" 버튼에 `click` 이벤트 핸들러를 추가합니다. 하지만 이제는 `generatePrimes()` 함수를 호출하는 대신 {{domxref("Worker/postMessage", "worker.postMessage()")}} 를 사용하여 워커에게 메시지를 보냅니다. 이 메시지는 인수를 받을 수 있으며, 이 경우 두 가지 속성이 포함된 JSON 객체를 전달합니다:
  - `command`: 워커가 수행하기를 원하는 작업을 식별하는 문자열(워커가 두 가지 이상의 작업을 수행할 수 있는 경우)
  - `quota`: 생성할 소수의 개수.

- 다음으로 워커에 `message` 이벤트 핸들러를 추가합니다. 이렇게 하면 워커가 완료된 시점을 알려주고 결과 데이터를 전달할 수 있습니다. 핸들러는 메시지의 `data` 속성에서 데이터를 가져와 output 요소에 씁니다(데이터는 `quota`와 정확히 동일하므로 약간 무의미하지만 원리를 보여줍니다).

- 마지막으로 "Reload" 버튼에 대한 `click` 이벤트 핸들러를 구현합니다. 이것은 동기식 버전과 완전히 동일합니다.

이제 워커 코드를 작성합니다. 다음 코드를 "generate.js"에 복사합니다:

```js
// Listen for messages from the main thread.
// If the message command is "generate", call `generatePrimes()`
addEventListener("message", (message) => {
  if (message.data.command === 'generate') {
    generatePrimes(message.data.quota);
  }
});

// Generate primes (very inefficiently)
function generatePrimes(quota) {

  function isPrime(n) {
    for (let c = 2; c <= Math.sqrt(n); ++c) {
      if (n % c === 0) {
          return false;
       }
    }
    return true;
  }

  const primes = [];
  const maximum = 1000000;

  while (primes.length < quota) {
    const candidate = Math.floor(Math.random() * (maximum + 1));
    if (isPrime(candidate)) {
      primes.push(candidate);
    }
  }

  // When we have finished, send a message to the main thread,
  // including the number of primes we generated.
  postMessage(primes.length);
}
```

메인 스크립트가 워커를 생성하는 즉시 실행된다는 점을 기억하세요.

워커가 가장 먼저 하는 일은 메인 스크립트의 메시지를 수신하기 시작하는 것입니다. 이 작업은 워커의 전역 함수인 `addEventListener()`를 사용하여 수행됩니다. `message` 이벤트 핸들러 내부의 이벤트 `data` 속성에는 메인 스크립트에서 전달된 인수의 복사본이 포함됩니다. 메인 스크립트에서 `generate` 명령을 전달한 경우, 메시지 이벤트의 `quota` 값을 전달하여 `generatePrimes()`를 호출합니다.

`generatePrimes()` 함수는 동기식 버전과 동일하지만 값을 반환하는 대신 완료되면 메인 스크립트에 메시지를 전송합니다. 이를 위해 {{domxref("DedicatedWorkerGlobalScope/postMessage", "postMessage()")}} 함수를 사용하는데, 이 함수는 `addEventListener()`와 마찬가지로 워커의 전역 함수입니다. 이미 살펴본 것처럼 메인 스크립트는 이 메시지를 수신 대기 중이며 메시지가 수신되면 DOM을 업데이트합니다.

> **참고:** file:// URL은 워커를 로드할 수 없으므로 이 사이트를 실행하려면 로컬 웹 서버를 실행해야 합니다. [로컬 테스트 서버 설정 가이드](/ko/docs/Learn/Common_questions/Tools_and_setup/set_up_a_local_testing_server) 를 참조하세요. 이 작업이 완료되면 "Generate primes"을 클릭하고 메인 페이지가 반응형 상태를 유지할 수 있어야 합니다.
>
> 예제를 만들거나 실행하는 데 문제가 있는 경우 [완성된 버전](https://github.com/mdn/learning-area/blob/main/javascript/asynchronous/workers/finished) 을 검토하고 [실시간](https://mdn.github.io/learning-area/javascript/asynchronous/workers/finished) 으로 사용해 볼 수 있습니다.

## 다른 유형의 워커

방금 만든 워커는 전용 워커라고 불리는 워커입니다. 즉, 단일 스크립트 인스턴스에서 사용된다는 뜻입니다.

하지만 다른 유형의 워커도 있습니다:

- [공유 워커](/ko/docs/Web/API/SharedWorker) 는 서로 다른 창에서 실행되는 여러 스크립트에서 공유할 수 있습니다.
- [서비스 워커](/ko/docs/Web/API/Service_Worker_API) 는 프록시 서버처럼 작동하여 사용자가 오프라인 상태일 때 웹 애플리케이션이 작동할 수 있도록 리소스를 캐싱합니다. [프로그레시브 웹 앱](/ko/docs/Web/Progressive_web_apps) 의 핵심 구성 요소입니다.

## 결론

이 글에서는 웹 애플리케이션이 별도의 스레드로 작업을 오프로드할 수 있는 웹 워커에 대해 소개했습니다. 메인 스레드와 워커는 변수를 직접 공유하지 않지만 메시지를 보내면 상대방이 `message` 이벤트로 수신하는 방식으로 통신합니다.

워커는 메인 애플리케이션이 사용할 수 있는 모든 API에 액세스할 수 없고 특히 DOM에 액세스할 수 없지만 메인 애플리케이션의 응답성을 유지하는 데 효과적인 방법이 될 수 있습니다.

## 참고 항목

- [웹 워커 사용](/ko/docs/Web/API/Web_Workers_API/Using_web_workers)
- [서비스 워커 사용하기](/ko/docs/Web/API/Service_Worker_API/Using_Service_Workers)
- [웹 워커 API](/ko/docs/Web/API/Web_Workers_API)

{{PreviousMenuNext("Learn/JavaScript/Asynchronous/Implementing_a_promise-based_API", "Learn/JavaScript/Asynchronous/Sequencing_animations", "Learn/JavaScript/Asynchronous")}}
