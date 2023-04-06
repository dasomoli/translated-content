---
title: How to use promises
slug: Learn/JavaScript/Asynchronous/Promises
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Asynchronous/Introducing", "Learn/JavaScript/Asynchronous/Implementing_a_promise-based_API", "Learn/JavaScript/Asynchronous")}}

**프로미스** 는 최신 자바스크립트에서 비동기 프로그래밍의 기초입니다. 프로미스는 비동기 함수가 반환하는 객체로, 작업의 현재 상태를 나타냅니다. 프로미스가 호출자에게 반환될 당시에는 작업이 완료되지 않은 경우가 많지만, 프로미스 객체는 작업의 최종 성공 또는 실패를 처리하는 메서드를 제공합니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        기본적인 컴퓨터 활용 능력, 이벤트 처리를 포함한 JavaScript 기본 사항에 대한 합리적인 이해.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>자바스크립트에서 프로미스를 사용하는 방법을 이해합니다.</td>
    </tr>
  </tbody>
</table>

지난 글에서 비동기 함수를 구현하기 위해 콜백을 사용하는 방법에 대해 이야기했습니다. 이 설계에서는 콜백 함수를 전달하면서 비동기 함수를 호출합니다. 함수는 즉시 반환하고 작업이 완료되면 콜백을 호출합니다.

프로미스 기반 API를 사용하면 비동기 함수가 작업을 시작하고 {{jsxref("Promise")}} 객체를 반환합니다. 그런 다음 이 프로미스 객체에 핸들러를 연결할 수 있으며, 작업이 성공하거나 실패할 때 이러한 핸들러가 실행됩니다.

## fetch() API 사용하기

> **참고:** 이 문서에서는 페이지에서 브라우저의 JavaScript 콘솔로 코드 샘플을 복사하여 프로미스를 살펴봅니다. 이를 설정하려면

> 1. 브라우저 탭을 열고 <https://example.org>
> 2. 해당 탭에서 [브라우저의 개발자 도구](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools) 에서 JavaScript 콘솔을 엽니다.
> 3. 예제가 표시되면 콘솔에 복사합니다. 새 예제를 입력할 때마다 페이지를 새로 고침해야 하며, 그렇지 않으면 콘솔에서 `fetchPromise`를 다시 선언했다고 불만을 표시합니다.

이 예제에서는 <https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json> 에서 JSON 파일을 다운로드하고 이에 대한 몇 가지 정보를 기록하겠습니다.

이를 위해 서버에 **HTTP 요청** 을 합니다. HTTP 요청에서는 원격 서버에 요청 메시지를 보내면 서버가 응답을 보냅니다. 이 경우 서버에서 JSON 파일을 가져오는 요청을 보내겠습니다. 지난 글에서 {{domxref("XMLHttpRequest")}} API를 사용하여 HTTP 요청을 했던 것을 기억하시나요? 이 글에서는 `XMLHttpRequest`를 대체하는 최신 프로미스 기반 API인 {{domxref("fetch", "fetch()")}} API를 사용하겠습니다.

이 코드를 브라우저의 자바스크립트 콘솔에 복사하세요:

```js
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

console.log(fetchPromise);

fetchPromise.then((response) => {
  console.log(`Received response: ${response.status}`);
});

console.log("Started request…");
```

여기서 우리는:

1. `fetch()` API를 호출하고 반환값을 `fetchPromise` 변수에 할당합니다.
2. 바로 뒤에 `fetchPromise` 변수를 로깅합니다. 이렇게 하면 다음과 같은 내용이 출력됩니다: `Promise { <state>: "pending" }`으로, `Promise` 개체가 있고 값이 `"pending"`인 `state`를 가지고 있음을 알려줍니다. `"pending"` 상태는 가져오기 작업이 아직 진행 중이라는 것을 의미합니다.
3. 핸들러 함수를 프로미스의 **`then()`** 메서드에 전달합니다. 불러오기 작업이 성공하면(그리고 성공하면), 프로미스는 처리기를 호출하여 서버의 응답이 포함된 {{domxref("Response")}} 객체를 전달합니다.
4. 요청을 시작했다는 메시지를 로깅합니다.

전체 출력은 다음과 같아야 합니다:

```plain
Promise { <state>: "pending" }
Started request…
Received response: 200
```

`Started request…`은 응답을 받기 전에 기록된다는 점에 유의하세요. 동기식 함수와 달리 `fetch()`는 요청이 계속 진행되는 동안 반환되므로 프로그램이 계속 응답할 수 있습니다. 응답에는 `200` (OK) [상태 코드](/ko/docs/Web/HTTP/Status) 가 표시되며, 이는 요청이 성공했음을 의미합니다.

이 예제는 {{domxref("XMLHttpRequest")}} 객체에 이벤트 핸들러를 추가했던 지난 글의 예제와 비슷해 보일 수 있습니다. 그 대신 반환된 프로미스의 `then()` 메서드에 핸들러를 전달합니다.

## 프로미스 연결

`fetch()` API를 사용하면 `Response` 객체를 가져온 후 다른 함수를 호출하여 응답 데이터를 가져와야 합니다. 이 경우 응답 데이터를 JSON으로 가져오고 싶으므로 `Response` 객체의 {{domxref("Response/json", "json()")}} 메서드를 호출합니다. `json()` 역시 비동기식이라는 것이 밝혀졌습니다. 따라서 두 개의 비동기 함수를 연속적으로 호출해야 하는 경우입니다.

이렇게 해보세요:

```js
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

fetchPromise.then((response) => {
  const jsonPromise = response.json();
  jsonPromise.then((data) => {
    console.log(data[0].name);
  });
});
```

이 예제에서는 이전과 마찬가지로 `fetch()`가 반환한 프로미스에 `then()` 핸들러를 추가합니다. 하지만 이번에는 핸들러가 `response.json()`을 호출한 다음 `response.json()`이 반환한 프로미스에 새 `then()` 핸들러를 전달합니다.

이렇게 하면 "baked beans"("products.json"에 나열된 첫 번째 제품의 이름)가 기록됩니다.

하지만 잠깐만요! 지난 글에서 다른 콜백 안에서 콜백을 호출하면 중첩된 코드 레벨이 연속적으로 증가한다고 말씀드렸던 것을 기억하시나요? 그리고 이 "콜백 지옥"이 코드를 이해하기 어렵게 만든다고 말씀드렸었죠? 이번에도 `then()` 호출만 다를 뿐 똑같지 않나요?

물론 그렇습니다. 하지만 프로미스의 우아한 특징은 `then()` 자체가 프로미스를 반환하고, 이 프로미스는 전달된 함수의 결과로 완성된다는 점입니다. 즉, 위의 코드를 다음과 같이 다시 작성할 수 있으며, 당연히 그렇게 해야 합니다:

```js
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

fetchPromise
  .then((response) => response.json())
  .then((data) => {
    console.log(data[0].name);
  });
```

첫 번째 `then()`에 대한 핸들러 내부에서 두 번째 `then()`을 호출하는 대신 `json()`이 반환한 프로미스를 반환하고 그 반환값에 대해 두 번째 `then()`을 호출할 수 있습니다. 이를 **프로미스 체이닝** 라고 하며, 연속적인 비동기 함수 호출이 필요할 때 들여쓰기 수준이 계속 증가하는 것을 방지할 수 있습니다.

다음 단계로 넘어가기 전에 추가해야 할 부분이 하나 더 있습니다. 요청을 읽기 전에 서버가 요청을 수락하고 처리할 수 있는지 확인해야 합니다. 이를 위해 응답의 상태 코드를 확인하고 "OK"가 아닌 경우 오류를 발생시키면 됩니다:

```js
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

fetchPromise
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => {
    console.log(data[0].name);
  });
```

## 오류 잡기

마지막으로 오류를 어떻게 처리할까요? `fetch()` API는 여러 가지 이유로 오류를 발생시킬 수 있으며(예: 네트워크 연결이 되지 않았거나 URL이 어떤 식으로든 잘못되었기 때문), 서버가 오류를 반환하면 저희도 오류를 발생시키고 있습니다.

지난 글에서 중첩 콜백을 사용하면 오류 처리가 매우 어려워져서 모든 중첩 수준에서 오류를 처리해야 한다는 것을 살펴보았습니다.

오류 처리를 지원하기 위해 `Promise` 객체는 {{jsxref("Promise/catch", "catch()")}} 메서드를 제공합니다. 이 메서드는 `then()`과 매우 유사합니다. 이 메서드를 호출하고 핸들러 함수를 전달합니다. 하지만 `then()`로 전달된 핸들러는 비동기 연산이 성공할 때 호출되는 반면, `catch()`로 전달된 핸들러는 비동기 연산이 실패할 때 호출됩니다.

`catch()`를 프로미스 체인의 끝에 추가하면 비동기 함수 호출 중 하나라도 실패하면 호출됩니다. 따라서 하나의 연산을 여러 개의 연속적인 비동기 함수 호출로 구현하고 모든 오류를 처리할 수 있는 단일 위치를 가질 수 있습니다.

이 버전의 `fetch()` 코드를 사용해 보세요. `catch()`를 사용하여 오류 처리기를 추가하고 요청이 실패하도록 URL도 수정했습니다.

```js
const fetchPromise = fetch('bad-scheme://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

fetchPromise
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => {
    console.log(data[0].name);
  })
  .catch((error) => {
    console.error(`Could not get products: ${error}`);
  });
```

이 버전을 실행해 보세요. `catch()` 핸들러에 오류가 기록되는 것을 볼 수 있을 것입니다.

## 프로미스 용어

프로미스에는 명확히 알아둘 필요가 있는 몇 가지 구체적인 용어가 있습니다.

첫째, 프로미스는 세 가지 상태 중 하나에 있을 수 있습니다:

- **pending**(보류 중): 프로미스가 생성되었지만 연결된 비동기 함수가 아직 성공하거나 실패하지 않은 상태입니다. 이 상태는 `fetch()` 호출에서 프로미스가 반환되고 요청이 계속 진행 중일 때 프로미스의 상태입니다.
- **fulfilled**(이행됨): 비동기 함수가 성공했습니다. 프라미스가 이행되면 `then()` 핸들러가 호출됩니다.
- **rejected**(거부됨): 비동기 함수가 실패했습니다. 프로미스가 거부되면 해당 `catch()` 핸들러가 호출됩니다.

여기서 "성공" 또는 "실패"의 의미는 해당 API에 따라 다릅니다. 예를 들어 `fetch()`는 서버가 [404 Not Found](/ko/docs/Web/HTTP/Status/404) 와 같은 오류를 반환하면 요청이 성공한 것으로 간주하지만 네트워크 오류로 인해 요청이 전송되지 않은 경우에는 요청이 성공하지 않은 것으로 간주합니다.

때로는 **fulfilled**(이행됨)와 **rejected**(거부됨) 모두를 포괄하기 위해 **settled**(해결)라는 용어를 사용하기도 합니다.

프로미스가 해결되었거나 다른 프로미스의 상태를 따르도록 "고정"된 경우 프로미스가 **resolved**(해결)된 것으로 간주됩니다.

[프로미스에 대해 이야기하는 방법에 대해 이야기해 봅시다](https://thenewtoys.dev/blog/2021/02/08/lets-talk-about-how-to-talk-about-promises/) 문서에서 이 용어에 대한 자세한 설명을 확인할 수 있습니다.

## 여러 개의 프로미스 결합하기

프로미스 체인은 작업이 여러 개의 비동기 함수로 구성되어 있고 다음 작업을 시작하기 전에 각 함수가 완료되어야 할 때 필요한 것입니다. 하지만 비동기 함수 호출을 결합해야 하는 다른 방법도 있으며, `Promise` API는 이를 위한 몇 가지 헬퍼를 제공합니다

때로는 모든 프로미스가 이행되어야 하지만 서로 의존하지 않는 경우가 있습니다. 이런 경우에는 모든 프로미스를 함께 시작한 다음 모든 프로미스가 이행되면 알림을 받는 것이 훨씬 더 효율적입니다. 여기에 필요한 것이 바로 {{jsxref("Promise/all", "Promise.all()")}} 메서드입니다. 이 메서드는 프로미스의 배열을 받아 하나의 프로미스를 반환합니다.

`Promise.all()`이 반환하는 프로미스는 다음과 같습니다:

- 배열의 모든 프로미스가 이행될 때 이행됩니다. 이 경우, `then()` 핸들러는 모든 응답의 배열과 함께 호출되며, 프로미스가 `all()`에 전달된 순서와 동일합니다.
- 배열의 프로미스 중 하나라도 거부되는 경우 거부됩니다. 이 경우 `catch()` 핸들러는 거부된 프로미스가 던진 에러와 함께 호출됩니다.

예를 들어

```js
const fetchPromise1 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
const fetchPromise2 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found');
const fetchPromise3 = fetch('https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');

Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
  .then((responses) => {
    for (const response of responses) {
      console.log(`${response.url}: ${response.status}`);
    }
  })
  .catch((error) => {
    console.error(`Failed to fetch: ${error}`)
  });
```

여기서는 세 개의 서로 다른 URL에 세 번의 `fetch()` 요청을 하고 있습니다. 모두 성공하면 각 요청의 응답 상태를 기록합니다. 하나라도 실패하면 실패를 기록합니다.

제공한 URL을 사용하면 모든 요청이 완료되어야 하지만, 두 번째 요청의 경우 요청된 파일이 존재하지 않기 때문에 서버가 `200`(OK) 대신 `404`(Not Found)를 반환합니다. 따라서 출력은 다음과 같아야 합니다:

```plain
https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json: 200
https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found: 404
https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json: 200
```

다음과 같이 잘못 형성된 URL로 동일한 코드를 시도해 보겠습니다:

```js
const fetchPromise1 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
const fetchPromise2 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found');
const fetchPromise3 = fetch('bad-scheme://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');

Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
  .then((responses) => {
    for (const response of responses) {
      console.log(`${response.url}: ${response.status}`);
    }
  })
  .catch((error) => {
    console.error(`Failed to fetch: ${error}`)
  });
```

그러면 `catch()` 핸들러가 실행될 것으로 예상할 수 있으며 다음과 같은 내용이 표시될 것입니다:

```plain
Failed to fetch: TypeError: Failed to fetch
```

때로는 일련의 프로미스 중 하나만 이행해야 하고 어떤 프로미스가 이행되든 상관없을 수도 있습니다. 이 경우 {{jsxref("Promise/any", "Promise.any()")}} 가 필요합니다. 이 함수는 `Promise.all()`과 비슷하지만, 프로미스 배열 중 하나라도 이행되면 즉시 이행되고, 모든 프로미스가 거부되면 거부된다는 점이 다릅니다:

```js
const fetchPromise1 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
const fetchPromise2 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found');
const fetchPromise3 = fetch('https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');

Promise.any([fetchPromise1, fetchPromise2, fetchPromise3])
  .then((response) => {
    console.log(`${response.url}: ${response.status}`);
  })
  .catch((error) => {
    console.error(`Failed to fetch: ${error}`)
  });
```

이 경우 어떤 가져오기 요청이 먼저 완료될지 예측할 수 없다는 점에 유의하세요.

이는 여러 프로미스를 결합하기 위한 추가 프로미스 함수 중 두 가지에 불과합니다. 나머지에 대해 알아보려면 {{jsxref("Promise")}} 참조 문서를 참조하세요.

## async 및 await

{{jsxref("Statements/async_function", "async")}} 키워드는 비동기 프로미스 기반 코드로 작업하는 더 간단한 방법을 제공합니다. 함수의 시작 부분에 `async`를 추가하면 비동기 함수가 됩니다:

```js
async function myFunction() {
  // This is an async function
}
```

비동기 함수 내에서 프로미스를 반환하는 함수를 호출하기 전에 `await` 키워드를 사용할 수 있습니다. 이렇게 하면 코드가 프로미스가 정산될 때까지 해당 지점에서 대기하게 되며, 이 시점에서 프로미스의 이행된 값이 반환 값으로 처리되거나 거부된 값이 던져집니다.

이를 통해 비동기 함수를 사용하지만 동기 코드처럼 보이는 코드를 작성할 수 있습니다. 예를 들어 이 기능을 사용하여 가져오기 예제를 다시 작성할 수 있습니다:

```js
async function fetchProducts() {
  try {
    // after this line, our function will wait for the `fetch()` call to be settled
    // the `fetch()` call will either return a Response or throw an error
    const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    // after this line, our function will wait for the `response.json()` call to be settled
    // the `response.json()` call will either return the parsed JSON object or throw an error
    const data = await response.json();
    console.log(data[0].name);
  }
  catch (error) {
    console.error(`Could not get products: ${error}`);
  }
}

fetchProducts();
```

여기서는 `await fetch()`를 호출하고 있는데, 호출자는 `Promise`를 가져오는 대신 `fetch()`가 동기식 함수인 것처럼 완전히 완전한 `Response` 객체를 반환받습니다!

코드가 동기식일 때와 똑같이 오류 처리를 위해 `try...catch` 블록을 사용할 수도 있습니다.

하지만 비동기 함수는 항상 프로미스를 반환하므로 다음과 같은 작업을 수행할 수 없습니다:

```js example-bad
async function fetchProducts() {
  try {
    const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    const data = await response.json();
    return data;
  }
  catch (error) {
    console.error(`Could not get products: ${error}`);
  }
}

const promise = fetchProducts();
console.log(promise[0].name);   // "promise" is a Promise object, so this will not work
```

대신 다음과 같은 작업을 수행해야 합니다:

```js
async function fetchProducts() {
  try {
    const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    const data = await response.json();
    return data;
  }
  catch (error) {
    console.error(`Could not get products: ${error}`);
  }
}

const promise = fetchProducts();
promise.then((data) => console.log(data[0].name));
```

또한 코드가 [JavaScript 모듈](/ko/docs/Web/JavaScript/Guide/Modules) 에 있지 않는 한 `async` 함수 내에서만 `await`을 사용할 수 있다는 점에 유의하세요. 즉, 일반 스크립트에서는 이 작업을 수행할 수 없습니다:

```js
try {
  // using await outside an async function is only allowed in a module
  const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }
  const data = await response.json();
  console.log(data[0].name);
}
catch(error) {
  console.error(`Could not get products: ${error}`);
}
```

프로미스 체인을 사용하는 경우 `async` 함수를 많이 사용하게 될 것이며, 비동기 함수를 사용하면 프로미스 작업을 훨씬 더 직관적으로 할 수 있습니다.

프로미스 체인과 마찬가지로, `await`이 비동기 연산을 연속적으로 완료하도록 강제한다는 점에 유의하세요. 이는 다음 작업의 결과가 마지막 작업의 결과에 의존하는 경우에 필요하지만, 그렇지 않은 경우에는 `Promise.all()`과 같은 것이 더 성능이 좋습니다.

## 결론

프로미스는 최신 자바스크립트에서 비동기 프로그래밍의 기초입니다. 프로미스는 깊게 중첩된 콜백 없이 비동기 연산 시퀀스를 쉽게 표현하고 추론할 수 있게 해주며, 동기식 `try...catch` 문과 유사한 오류 처리 스타일을 지원합니다.

`async` 및 `await` 키워드를 사용하면 일련의 연속적인 비동기 함수 호출에서 연산을 더 쉽게 구축할 수 있으므로 명시적인 프로미스 체인을 만들 필요가 없으며 동기 코드와 똑같이 보이는 코드를 작성할 수 있습니다.

프로미스는 모든 최신 브라우저의 최신 버전에서 작동하며, 프로미스 지원이 문제가 되는 유일한 곳은 Opera Mini와 IE11 및 이전 버전입니다.

이 글에서는 프로미스의 모든 기능을 다루지 않고 가장 흥미롭고 유용한 기능만 다루었습니다. 프로미스에 대해 더 많이 배우기 시작하면 더 많은 기능과 기술을 접하게 될 것입니다.

[WebRTC](/ko/docs/Web/API/WebRTC_API), [웹 오디오 API](/ko/docs/Web/API/Web_Audio_API), [미디어 캡처 및 스트림 API](/ko/docs/Web/API/Media_Capture_and_Streams_API) 등을 포함한 많은 최신 웹 API가 프로미스 기반입니다.

## 참조

- [`Promise()`](/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [프로미스 사용하기](/ko/docs/Web/JavaScript/Guide/Using_promises)
- 놀란 로슨의 [프로미스에 문제가 있습니다.](https://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html)
- [프로미스에 대해 이야기하는 방법에 대해 이야기해 봅시다](https://thenewtoys.dev/blog/2021/02/08/lets-talk-about-how-to-talk-about-promises/)

{{PreviousMenuNext("Learn/JavaScript/Asynchronous/Introducing", "Learn/JavaScript/Asynchronous/Implementing_a_promise-based_API", "Learn/JavaScript/Asynchronous")}}
