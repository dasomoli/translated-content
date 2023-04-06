---
title: Working with JSON
slug: Learn/JavaScript/Objects/JSON
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Objects/Classes_in_JavaScript", "Learn/JavaScript/Objects/Object_building_practice", "Learn/JavaScript/Objects")}}

JSON(JavaScript Object Notation)은 JavaScript 객체 구문을 기반으로 구조화된 데이터를 표현하기 위한 표준 텍스트 기반 형식입니다. 일반적으로 웹 애플리케이션에서 데이터를 전송하는 데 사용됩니다(예: 일부 데이터를 서버에서 클라이언트로 전송하여 웹 페이지에 표시하거나 그 반대로 표시할 수 있도록 하는 경우). 자주 접하게 될 것이므로 이 글에서는 JSON을 파싱하여 그 안의 데이터에 액세스하고 JSON을 생성하는 등 JavaScript를 사용하여 JSON으로 작업하는 데 필요한 모든 것을 알려드립니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        기본적인 컴퓨터 활용 능력, HTML 및 CSS에 대한 기본적인 이해, JavaScript 기본 사항(<a href="/ko/docs/Learn/JavaScript/First_steps">첫걸음</a> 및 <a href="/ko/docs/Learn/JavaScript/Building_blocks">Building blocks</a>빌딩 블록</a> 참조) 및 OOJS 기본 사항(<a href="/ko/docs/Learn/JavaScript/Objects/Basics">객체 소개</a> 참조)에 익숙해야 합니다.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        JSON으로 저장된 데이터로 작업하는 방법을 이해하고 자신만의 JSON 문자열을 생성할 수 있습니다.
      </td>
    </tr>
  </tbody>
</table>

## JSON이란 무엇인가요?

{{glossary("JSON")}}은 [더글러스 크록포드](https://en.wikipedia.org/wiki/Douglas_Crockford) 가 대중화시킨 JavaScript 객체 구문을 따르는 텍스트 기반 데이터 형식입니다.
JavaScript 객체 리터럴 구문과 매우 유사하지만 JavaScript와 독립적으로 사용할 수 있으며, 많은 프로그래밍 환경에서 JSON을 읽고(파싱) 생성할 수 있는 기능을 제공합니다.

JSON은 문자열로 존재하므로 네트워크를 통해 데이터를 전송할 때 유용합니다.
데이터에 액세스하려면 네이티브 JavaScript 객체로 변환해야 합니다.
이는 큰 문제가 되지 않습니다. JavaScript는 둘 사이를 변환하는 데 사용할 수 있는 메서드가 있는 전역 [JSON](/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON) 객체를 제공합니다.

> **참고:** 문자열을 네이티브 객체로 변환하는 것을 역직렬화라고 하고, 네이티브 객체를 문자열로 변환하여 네트워크를 통해 전송할 수 있도록 하는 것을 직렬화라고 합니다.

JSON 문자열은 자체 파일에 저장할 수 있으며, 기본적으로 확장자가 `.json`인 텍스트 파일과 {{glossary("MIME type")}} 형식의 `application/json`입니다.

### JSON 구조

위에서 설명한 것처럼 JSON은 JavaScript 객체 리터럴 형식과 매우 유사한 형식을 가진 문자열입니다.
표준 JavaScript 객체와 동일한 기본 데이터 유형(문자열, 숫자, 배열, 부울 및 기타 객체 리터럴)을 JSON에 포함할 수 있습니다.
이를 통해 다음과 같이 데이터 계층 구조를 구성할 수 있습니다:

```json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

예를 들어 이 문자열을 자바스크립트 프로그램에 로드하여 superHeroes라는 변수로 구문 분석하면 자바스크립트 객체 기본 문서에서 살펴본 것과 동일한 점/대괄호 표기법을 사용하여 그 안에 있는 데이터에 액세스할 수 있습니다.
예를 들어

```js
superHeroes.homeTown
superHeroes['active']
```

계층 구조 아래쪽의 데이터에 액세스하려면 필요한 속성 이름과 배열 인덱스를 함께 연결해야 합니다. 예를 들어, 멤버 목록에 나열된 두 번째 영웅의 세 번째 초능력에 액세스하려면 이렇게 하면 됩니다:

```js
superHeroes['members'][1]['powers'][2]
```

1. 먼저 변수 이름이 `superHeroes`입니다.
2. 그 안에 `members` 속성에 액세스하고 싶으므로 `["members"]`를 사용합니다.
3. `members`에는 객체로 채워진 배열이 들어 있습니다. 배열 내부의 두 번째 객체에 액세스하고 싶으므로 `[1]`을 사용합니다.
4. 이 객체 내부에서 `powers` 프로퍼티에 액세스하고 싶으므로 `["powers"]`를 사용합니다.
5. `powers` 속성 안에는 선택한 영웅의 초능력이 포함된 배열이 있습니다. 세 번째가 필요하므로 `[2]`를 사용합니다.

> **참고:** 위에 표시된 JSON을 [JSONTest.html](https://mdn.github.io/learning-area/javascript/oojs/json/JSONTest.html) 예제의 변수 내부에서 사용할 수 있도록 만들었습니다([소스 코드](https://github.com/mdn/learning-area/blob/main/javascript/oojs/json/JSONTest.html) 참조).
> 이를 로드한 다음 브라우저의 JavaScript 콘솔을 통해 변수 내부의 데이터에 액세스해 보세요.

### JSON으로 배열

위에서 JSON 텍스트는 기본적으로 문자열 내부의 JavaScript 객체처럼 보인다고 언급했습니다.
배열을 JSON으로 변환할 수도 있습니다. 예를 들어 아래는 유효한 JSON입니다:

```json
[
  {
    "name": "Molecule Man",
    "age": 29,
    "secretIdentity": "Dan Jukes",
    "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
  },
  {
    "name": "Madame Uppercut",
    "age": 39,
    "secretIdentity": "Jane Wilson",
    "powers": [
      "Million tonne punch",
      "Damage resistance",
      "Superhuman reflexes"
    ]
  }
]
```

위는 완벽하게 유효한 JSON입니다. 배열 인덱스로 시작하여 배열 항목(구문 분석된 버전)에 액세스하기만 하면 됩니다(예: `[0]["powers"][0])`.

### 기타 참고 사항

- JSON은 지정된 데이터 형식을 가진 문자열일 뿐이며 메서드 없이 속성만 포함합니다.
- JSON에서는 문자열과 속성 이름 주위에 큰따옴표를 사용해야 합니다.
  작은따옴표는 전체 JSON 문자열을 둘러싸는 것 외에는 유효하지 않습니다.
- 쉼표나 콜론이 하나만 잘못 배치되어도 JSON 파일이 잘못되어 작동하지 않을 수 있습니다.
  사용하려는 데이터의 유효성을 검사하는 데 주의를 기울여야 합니다(컴퓨터로 생성된 JSON은 생성기 프로그램이 올바르게 작동하는 한 오류를 포함할 가능성이 적지만).
  [JSONLint](https://jsonlint.com/) 와 같은 애플리케이션을 사용하여 JSON의 유효성을 검사할 수 있습니다.
- JSON은 실제로 배열이나 객체뿐만 아니라 JSON에 포함할 수 있는 모든 데이터 유형의 형태를 취할 수 있습니다.
  예를 들어, 단일 문자열이나 숫자도 유효한 JSON이 될 수 있습니다.
- 객체 속성을 따옴표로 묶지 않을 수 있는 JavaScript 코드와 달리 JSON에서는 따옴표로 묶인 문자열만 속성으로 사용할 수 있습니다.

## 능동적 학습: JSON 예제를 통해 작업하기

이제 예제를 통해 웹 사이트에서 JSON 형식의 데이터를 어떻게 활용할 수 있는지 살펴보겠습니다.

### 시작하기

먼저 [heroes.html](https://github.com/mdn/learning-area/blob/main/javascript/oojs/json/heroes.html) 및 [style.css](https://github.com/mdn/learning-area/blob/main/javascript/oojs/json/style.css) 파일의 로컬 복사본을 만듭니다.
후자에는 페이지 스타일을 지정하는 간단한 CSS가 포함되어 있고, 전자는 매우 간단한 본문 HTML과 이 연습에서 작성할 JavaScript 코드를 포함하는 {{HTMLElement("script")}} 요소가 포함되어 있습니다:

```html
<header>

</header>

<section>

</section>

<script>

</script>
```

저희는 GitHub(<https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json>)에서 JSON 데이터를 사용할 수 있도록 공개했습니다.

JSON을 스크립트에 로드하고 다음과 같이 몇 가지 멋진 DOM 조작을 사용하여 표시하겠습니다:

![Image of a document titled "Super hero squad" (in a fancy font) and subtitled "Hometown: Metro City // Formed: 2016". Three columns below the heading are titled "Molecule Man", "Madame Uppercut", and "Eternal Flame", respectively. Each column lists the hero's secret identity name, age, and superpowers.](json-superheroes.png)

### 최상위 함수

최상위 함수는 다음과 같습니다:

```js
async function populate() {

  const requestURL = 'https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json';
  const request = new Request(requestURL);

  const response = await fetch(request);
  const superHeroes = await response.json();

  populateHeader(superHeroes);
  populateHeroes(superHeroes);

}
```

JSON을 가져오기 위해 [Fetch](/ko/docs/Web/API/Fetch_API) 라는 API를 사용합니다.
이 API를 사용하면 JavaScript를 통해 서버에서 리소스(예: 이미지, 텍스트, JSON, HTML 스니펫)를 검색하도록 네트워크 요청을 할 수 있으므로 전체 페이지를 다시 로드할 필요 없이 콘텐츠의 작은 섹션을 업데이트할 수 있습니다.

이 함수에서 처음 네 줄은 Fetch API를 사용하여 서버에서 JSON을 가져옵니다:

- `requestURL` 변수를 선언하여 GitHub URL을 저장합니다.
- URL을 사용하여 새 {{domxref("Request")}} 객체를 초기화합니다.
- {{domxref("fetch", "fetch()")}} 함수를 사용하여 네트워크 요청을 하면 {{domxref("Response")}} 객체가 반환됩니다.
- `Response` 객체의 {{domxref("Response/json", "json()")}} 함수를 사용하여 응답을 JSON으로 검색합니다.

> **참고:** `fetch()` API는 **비동기식** 입니다. [다음 모듈](/ko/docs/Learn/JavaScript/Asynchronous) 에서 비동기 함수에 대해 자세히 알아보겠지만, 지금은 fetch API를 사용하는 함수 이름 앞에 {{jsxref("Statements/async_function", "async")}} 키워드를 추가하고 비동기 함수를 호출하기 전에 {{jsxref("Operators/await", "await")}} 키워드를 추가해야 한다는 점만 말씀드리겠습니다.

그 후, `superHeroes` 변수에는 JSON에 기반한 JavaScript 객체가 포함됩니다. 그런 다음 이 객체를 두 개의 함수 호출에 전달합니다. 첫 번째 호출은 `<header>`를 올바른 데이터로 채우고, 두 번째 호출은 팀의 각 영웅에 대한 정보 카드를 생성하여 `<section>`에 삽입합니다.

### 헤더 채우기

이제 JSON 데이터를 검색하고 자바스크립트 객체로 변환했으므로 위에서 참조한 두 함수를 작성하여 이를 활용해 보겠습니다. 먼저 이전 코드 아래에 다음 함수 정의를 추가합니다:

```js
function populateHeader(obj) {
  const header = document.querySelector('header');
  const myH1 = document.createElement('h1');
  myH1.textContent = obj.squadName;
  header.appendChild(myH1);

  const myPara = document.createElement('p');
  myPara.textContent = `Hometown: ${obj.homeTown} // Formed: ${obj.formed}`;
  header.appendChild(myPara);
}
```

여기서는 먼저 [`createElement()`](/ko/docs/Web/API/Document/createElement) 를 사용하여 {{HTMLElement("Heading_Elements", "h1")}} 요소를 생성하고, [`textContent`](/ko/docs/Web/API/Node/textContent)을 객체의 `squadName` 속성과 같도록 설정한 다음 [`appendChild()`](/ko/docs/Web/API/Node/appendChild) 를 사용하여 헤더에 추가합니다. 그런 다음 단락을 생성하고 텍스트 내용을 설정한 다음 헤더에 추가하는 매우 유사한 작업을 수행합니다. 유일한 차이점은 텍스트가 개체의 `homeTown`과 `formed` 속성을 모두 포함하는 [template literal](/ko/docs/Web/JavaScript/Reference/Template_literals) 로 설정된다는 점입니다.

### 영웅 정보 카드 만들기

다음으로 코드 하단에 슈퍼히어로 카드를 생성하고 표시하는 다음 함수를 추가합니다:

```js
function populateHeroes(obj) {
  const section = document.querySelector('section');
  const heroes = obj.members;

  for (const hero of heroes) {
    const myArticle = document.createElement('article');
    const myH2 = document.createElement('h2');
    const myPara1 = document.createElement('p');
    const myPara2 = document.createElement('p');
    const myPara3 = document.createElement('p');
    const myList = document.createElement('ul');

    myH2.textContent = hero.name;
    myPara1.textContent = `Secret identity: ${hero.secretIdentity}`;
    myPara2.textContent = `Age: ${hero.age}`;
    myPara3.textContent = 'Superpowers:';

    const superPowers = hero.powers;
    for (const power of superPowers) {
      const listItem = document.createElement('li');
      listItem.textContent = power;
      myList.appendChild(listItem);
    }

    myArticle.appendChild(myH2);
    myArticle.appendChild(myPara1);
    myArticle.appendChild(myPara2);
    myArticle.appendChild(myPara3);
    myArticle.appendChild(myList);

    section.appendChild(myArticle);
  }
}
```

우선 자바스크립트 객체의 `members` 프로퍼티를 새 변수에 저장합니다. 이 배열에는 각 영웅에 대한 정보가 포함된 여러 개의 오브젝트가 포함됩니다.

다음으로 [for...of 루프](/ko/docs/Learn/JavaScript/Building_blocks/Looping_code#the_for...of_loop) 를 사용하여 배열의 각 객체를 반복합니다. 각각의 객체에 대해

1. `<article>`, `<h2>`, `<p>` 세 개, `<ul>` 등 여러 개의 새 요소를 생성합니다.
2. `<h2>`에 현재 영웅의 `name`을 포함하도록 설정합니다.
3. 세 단락에 `secretIdentity`, `age`, "Superpowers:"라는 한 줄을 채워 목록에 있는 정보를 소개합니다.
4. 현재 영웅의 초능력을 나열하는 배열을 포함하는 `superPowers`라는 또 다른 새 상수에 `powers` 속성을 저장합니다.
5. 또 다른 `for...of` 루프를 사용하여 현재 영웅의 초능력을 반복합니다. 각 초능력에 대해 `<li>` 엘리먼트를 생성하고 그 안에 초능력을 넣은 다음 `appendChild()`를 사용하여 `listItem`을 `<ul>` 엘리먼트(`myList`) 안에 넣습니다.
6. 마지막으로 `<h2>`, `<p>`, `<ul>`을 `<article>`(`myArticle`) 안에 추가한 다음 `<section>` 안에 `<article>`를 추가하는 것입니다. 추가하는 순서는 HTML 내부에 표시되는 순서이므로 중요합니다.

> **참고:** 예제가 작동하는 데 문제가 있는 경우, [heroes-finished.html](https://github.com/mdn/learning-area/blob/main/javascript/oojs/json/heroes-finished.html) 소스 코드를 참조해 보세요([실시간으로 실행되는 모습](https://mdn.github.io/learning-area/javascript/oojs/json/heroes-finished.html) 도 확인하세요).

> **참고:** 자바스크립트 객체에 액세스하기 위해 사용하는 점/괄호 표기법을 따르는 데 문제가 있는 경우, 다른 탭이나 텍스트 편집기에서 [superheroes.json](https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json) 파일을 열고 자바스크립트를 볼 때 참조하면 도움이 될 수 있습니다.
> 점 및 대괄호 표기법에 대한 자세한 내용은 [JavaScript 객체 기초](/ko/docs/Learn/JavaScript/Objects/Basics) 문서를 참조하세요.

### 최상위 함수 호출하기

마지막으로 최상위 `populate()` 함수를 호출해야 합니다:

```js
populate();
```

## 객체와 텍스트 간 변환

위의 예제는 `response.json()`을 사용하여 네트워크 응답을 JavaScript 객체로 직접 변환했기 때문에 JavaScript 객체에 액세스하는 방식이 간단했습니다.

하지만 때로는 원시 JSON 문자열을 받아 직접 객체로 변환해야 하는 경우도 있습니다. 그리고 네트워크를 통해 자바스크립트 객체를 전송하려면 전송하기 전에 JSON(문자열)으로 변환해야 합니다. 다행히도 이 두 가지 문제는 웹 개발에서 매우 흔한 문제이기 때문에 브라우저에 내장된 [JSON](/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON) 객체를 사용할 수 있으며, 여기에는 다음 두 가지 방법이 포함되어 있습니다:

- [`parse()`](/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse):JSON 문자열을 매개변수로 받아 해당 JavaScript 객체를 반환합니다.
- [`stringify()`](/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify): 객체를 매개변수로 받아 그에 상응하는 JSON 문자열을 반환합니다.

첫 번째 함수는 [heroes-finished-json-parse.html](https://mdn.github.io/learning-area/javascript/oojs/json/heroes-finished-json-parse.html) 예제([소스 코드](https://github.com/mdn/learning-area/blob/main/javascript/oojs/json/heroes-finished-json-parse.html) 참조)에서 작동하는 것을 볼 수 있습니다. 이 예제는 앞서 구축한 예제와 정확히 동일한 작업을 수행합니다:

- 응답의 {{domxref("Response/text", "text()")}} 메서드를 호출하여 JSON이 아닌 텍스트로 응답을 검색합니다.
- 다음 `parse()`를 사용하여 텍스트를 JavaScript 객체로 변환합니다.

핵심 코드 스니펫은 여기에 있습니다:

```js
async function populate() {

  const requestURL = 'https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json';
  const request = new Request(requestURL);

  const response = await fetch(request);
  const superHeroesText = await response.text();

  const superHeroes = JSON.parse(superHeroesText);
  populateHeader(superHeroes);
  populateHeroes(superHeroes);

}
```

짐작할 수 있듯이 `stringify()`는 반대 방식으로 작동합니다. 브라우저의 자바스크립트 콘솔에 다음 줄을 하나씩 입력하여 실제로 작동하는지 확인해 보세요:

```js
let myObj = { name: "Chris", age: 38 };
myObj
let myString = JSON.stringify(myObj);
myString
```

여기서는 JavaScript 객체를 생성한 다음, 객체에 포함된 내용을 확인한 다음, `stringify()`를 사용하여 JSON 문자열로 변환하고 반환값을 새 변수에 저장한 다음 다시 확인합니다.

## 실력을 테스트해 보세요!

이 글의 마지막에 도달했지만 가장 중요한 정보를 기억할 수 있나요? 계속 진행하기 전에 이 정보를 기억하고 있는지 확인할 수 있는 몇 가지 추가 테스트를 찾아보세요: [실력을 테스트해 보세요: JSON](/ko/docs/Learn/JavaScript/Objects/Test_your_skills:_JSON) 을 참조하세요.

## 요약

이번 글에서는 JSON을 생성하고 구문 분석하는 방법과 그 안에 잠긴 데이터에 액세스하는 방법 등 프로그램에서 JSON을 사용하는 방법에 대한 간단한 가이드를 제공했습니다. 다음 글에서는 객체 지향 자바스크립트에 대해 살펴보겠습니다.

## 참고 항목

- [JSON 참조](/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [Fetch API 개요](/ko/docs/Web/API/Fetch_API)
- [Fetch 사용](/ko/docs/Web/API/Fetch_API/Using_Fetch)
- [HTTP 요청 방법](/ko/docs/Web/HTTP/Methods)
- [ECMA 표준 링크가 포함된 공식 JSON 웹 사이트](https://json.org)

{{PreviousMenuNext("Learn/JavaScript/Objects/Classes_in_JavaScript", "Learn/JavaScript/Objects/Object_building_practice", "Learn/JavaScript/Objects")}}
