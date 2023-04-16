---
title: JavaScript란 무엇인가요?
slug: Learn/JavaScript/First_steps/What_is_JavaScript
---

{{LearnSidebar}}{{NextMenu("Learn/JavaScript/First_steps/A_first_splash", "Learn/JavaScript/First_steps")}}

MDN 초급 자바스크립트 강좌에 오신 것을 환영합니다!
이 글에서는 "자바스크립트란 무엇인가요?", "자바스크립트로 무엇을 할 수 있나요?"와 같은 질문에 답하고 자바스크립트의 목적에 익숙해지도록 높은 수준에서 자바스크립트를 살펴볼 것입니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>기본적인 컴퓨터 활용 능력, HTML 및 CSS에 대한 기본적인 이해.</td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        JavaScript가 무엇인지, 무엇을 할 수 있는지, 웹 사이트에 어떻게 적용되는지 익히기 위한 과정입니다.
      </td>
    </tr>
  </tbody>
</table>

## 높은 수준의 정의

JavaScript는 웹 페이지에서 복잡한 기능을 구현할 수 있게 해주는 스크립팅 또는 프로그래밍 언어로, 웹 페이지가 단순히 정적인 정보를 표시하는 것 이상으로 시의적절한 콘텐츠 업데이트, 대화형 지도, 애니메이션 2D/3D 그래픽, 스크롤링 비디오 주크박스 등을 표시할 때마다 자바스크립트가 관련되어 있다고 확신할 수 있습니다.
자바스크립트는 표준 웹 기술의 레이어 케이크 중 세 번째 레이어이며, 이 중 두 가지([HTML](/ko/docs/Learn/HTML)과 [CSS](/ko/docs/Learn/CSS))는 학습 영역의 다른 부분에서 훨씬 더 자세히 다루었습니다.

![The three layers of standard web technologies; HTML, CSS and JavaScript](cake.png)

- {{glossary("HTML")}}은 단락, 제목, 데이터 테이블을 정의하거나 페이지에 이미지와 동영상을 삽입하는 등 웹 콘텐츠를 구성하고 의미를 부여하는 데 사용하는 마크업 언어입니다.
- {{glossary("CSS")}}는 배경색과 글꼴을 설정하고 콘텐츠를 여러 열에 배치하는 등 HTML 콘텐츠에 스타일을 적용하는 데 사용하는 스타일 규칙 언어입니다.
- {{glossary("JavaScript")}}는 동적으로 업데이트되는 콘텐츠를 만들고, 멀티미디어를 제어하고, 이미지에 애니메이션을 적용하는 등 거의 모든 작업을 수행할 수 있는 스크립팅 언어입니다. (물론 모든 것이 가능한 것은 아니지만, 자바스크립트 코드 몇 줄로 할 수 있는 일은 놀랍습니다.)

세 가지 레이어가 서로 잘 어울립니다. 간단한 텍스트 레이블을 예로 들어 보겠습니다. HTML을 사용하여 구조와 목적을 부여하기 위해 마크업할 수 있습니다:

```html
<p>Player 1: Chris</p>
```

![Paragraph of Player 1: Chris as plain text](just-html.png)

그런 다음 CSS를 추가하여 멋지게 보이도록 할 수 있습니다:

```css
p {
  font-family: "helvetica neue", helvetica, sans-serif;
  letter-spacing: 1px;
  text-transform: uppercase;
  text-align: center;
  border: 2px solid rgb(0 0 200 / 0.6);
  background: rgb(0 0 200 / 0.6);
  color: rgb(255 255 255 / 1);
  box-shadow: 1px 1px 2px rgb(0 0 200 / 0.4);
  border-radius: 10px;
  padding: 3px 10px;
  display: inline-block;
  cursor: pointer;
}
```

![Styled paragraph of Player 1: Chris](html-and-css.png)

마지막으로 자바스크립트를 추가하여 동적 동작을 구현할 수 있습니다:

```js
const para = document.querySelector("p");

para.addEventListener("click", updateName);

function updateName() {
  const name = prompt("Enter a new name");
  para.textContent = `Player 1: ${name}`;
}
```

{{ EmbedLiveSample('A_high-level_definition', '100%', 80) }}

이 마지막 버전의 텍스트 레이블을 클릭하여 어떤 일이 발생하는지 확인해 보세요(이 데모는 GitHub에서 찾을 수 있습니다. [소스 코드](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/what-is-js/javascript-label.html)를 보거나 [실시간으로 실행](https://mdn.github.io/learning-area/javascript/introduction-to-js-1/what-is-js/javascript-label.html)해 보세요)!

자바스크립트는 이보다 훨씬 더 많은 일을 할 수 있습니다. 자세한 내용을 살펴보겠습니다.

## 그렇다면 실제로 무엇을 할 수 있을까요?

핵심 클라이언트 측 자바스크립트 언어는 다음과 같은 작업을 수행할 수 있는 몇 가지 일반적인 프로그래밍 기능으로 구성되어 있습니다:

- 변수 안에 유용한 값을 저장합니다. 예를 들어 위의 예에서는 새 이름을 입력하도록 요청하고 해당 이름을 `name`이라는 변수에 저장합니다.
- 텍스트 조각에 대한 연산(프로그래밍에서는 "문자열"이라고 함). 위의 예에서는 문자열 "Player 1: "을 `name` 변수에 조인하여 전체 텍스트 레이블(예: "Player 1: Chris")을 만듭니다.
- 웹 페이지에서 발생하는 특정 이벤트에 대한 응답으로 코드를 실행합니다. 위 예제에서는 {{domxref("Element/click_event", "click")}} 이벤트를 사용하여 레이블이 클릭된 시점을 감지한 다음 텍스트 레이블을 업데이트하는 코드를 실행했습니다.
- 그리고 훨씬 더!

하지만 더욱 흥미로운 것은 클라이언트 측 자바스크립트 언어 위에 구축된 기능입니다. 이른바 **애플리케이션 프로그래밍 인터페이스**(**API**)는 자바스크립트 코드에서 사용할 수 있는 추가적인 강력한 기능을 제공합니다.

API는 개발자가 직접 구현하기 어렵거나 불가능한 프로그램을 구현할 수 있도록 해주는 기성 코드 빌딩 블록 세트입니다.
기성품 가구 키트가 집을 지을 때 하는 것과 같은 역할을 프로그래밍에서도 수행합니다. 직접 디자인을 구상하고, 올바른 목재를 찾고, 모든 패널을 올바른 크기와 모양으로 자르고, 올바른 크기의 나사를 찾아서 책장을 만드는 것보다 기성품 패널을 가져다가 함께 나사로 고정하여 책장을 만드는 것이 훨씬 더 쉽습니다.

일반적으로 두 가지 범주로 나뉩니다.

![Two categories of API; 3rd party APIs are shown to the side of the browser and browser APIs are in the browser](browser.png)

**브라우저 API**는 웹 브라우저에 내장되어 있으며 주변 컴퓨터 환경의 데이터를 노출하거나 유용한 복잡한 작업을 수행할 수 있습니다. 예를 들어

- {{domxref("Document_Object_Model","DOM (Document Object Model: 문서 객체 모델) API")}}를 사용하면 HTML과 CSS를 조작하여 HTML을 생성, 제거, 변경하고 페이지에 새 스타일을 동적으로 적용하는 등의 작업을 수행할 수 있습니다.
  예를 들어 페이지에 팝업 창이 나타나거나 새로운 콘텐츠가 표시될 때마다(위의 간단한 데모에서 보았듯이) DOM이 작동합니다.
- {{domxref("Geolocation","Geolocation API")}}는 지리적 정보를 검색합니다.
  이를 통해 [Google 지도](https://www.google.com/maps)가 사용자의 위치를 찾아 지도에 표시할 수 있습니다.
- {{domxref("Canvas_API","Canvas")}} 및 {{domxref("WebGL_API","WebGL")}} API를 사용하면 애니메이션 2D 및 3D 그래픽을 만들 수 있습니다. 사람들은 이러한 웹 기술을 사용하여 놀라운 작업을 하고 있습니다([Chrome 실험](https://experiments.withgoogle.com/collection/chrome) 및 [웹GL 샘플](https://webglsamples.org/)을 참조하세요).
- {{domxref("HTMLMediaElement")}} 및 {{domxref("WebRTC API", "WebRTC")}}와 같은 [오디오 및 비디오 API](/ko/docs/Web/Guide/Audio_and_video_delivery)를 사용하면 웹 페이지에서 바로 오디오 및 비디오를 재생하거나 웹 카메라에서 비디오를 가져와 다른 사람의 컴퓨터에 표시하는 등 멀티미디어로 정말 흥미로운 작업을 할 수 있습니다(간단한 [스냅샷 데모](https://chrisdavidmills.github.io/snapshot/)를 통해 아이디어를 얻을 수 있습니다).

> **참고:** 위의 데모 중 상당수는 구형 브라우저에서는 작동하지 않으므로 실험할 때는 Firefox, Chrome, Edge 또는 Opera와 같은 최신 브라우저에서 코드를 실행하는 것이 좋습니다.
> 프로덕션 코드(즉, 실제 고객이 사용할 실제 코드) 제공에 가까워지면 [크로스 브라우저 테스트](/ko/docs/Learn/Tools_and_testing/Cross_browser_testing)를 더 자세히 고려해야 합니다.

**타사 API**는 기본적으로 브라우저에 내장되어 있지 않으므로 일반적으로 웹 어딘가에서 해당 코드와 정보를 가져와야 합니다. 예를 들어

- [트위터 API](https://developer.twitter.com/en/docs)를 사용하면 웹사이트에 내 최신 트윗을 표시하는 등의 작업을 수행할 수 있습니다.
- [Google 지도 API](https://developers.google.com/maps/) 및 [오픈스트리트맵 API](https://wiki.openstreetmap.org/wiki/API)를 사용하면 웹사이트에 맞춤 지도를 임베드하는 등의 기능을 사용할 수 있습니다.

> **참고:** 이러한 API는 고급 API이므로 이 모듈에서는 다루지 않습니다. 이에 대한 자세한 내용은 [클라이언트 측 웹 API 모듈](/ko/docs/Learn/JavaScript/Client-side_web_APIs)에서 확인할 수 있습니다.

이 외에도 더 많은 것이 준비되어 있습니다! 하지만 아직 너무 흥분하지 마세요. 24시간 동안 자바스크립트를 공부했다고 해서 다음 페이스북, 구글 지도, 인스타그램을 만들 수 있는 것은 아니며, 먼저 다뤄야 할 기초가 많이 있습니다. 그렇기 때문에 여러분이 여기 있는 것이니 계속 진행합시다!

## 페이지에서 자바스크립트가 수행하는 작업은 무엇인가요?

여기서는 실제로 몇 가지 코드를 살펴보면서 페이지에서 자바스크립트를 실행하면 실제로 어떤 일이 일어나는지 살펴보겠습니다.

브라우저에서 웹 페이지를 로드할 때 어떤 일이 일어나는지 간단히 정리해 보겠습니다([CSS 작동 방식](/ko/docs/Learn/CSS/First_steps/How_CSS_works#how_does_css_actually_work) 문서에서 처음 설명했습니다). 브라우저에서 웹 페이지를 로드하면 실행 환경(브라우저 탭) 내에서 코드(HTML, CSS 및 JavaScript)를 실행하게 됩니다. 이는 원재료(코드)를 들여와 제품(웹 페이지)을 출력하는 공장과 같습니다.

![HTML, CSS and JavaScript code come together to create the content in the browser tab when the page is loaded](execution.png)

JavaScript의 가장 일반적인 용도는 위에서 설명한 대로 문서 객체 모델 API를 통해 HTML과 CSS를 동적으로 수정하여 사용자 인터페이스를 업데이트하는 것입니다.
웹 문서의 코드는 일반적으로 페이지에 표시되는 순서대로 로드되고 실행된다는 점에 유의하세요.
자바스크립트가 수정하려는 HTML 및 CSS보다 먼저 로드되고 실행되면 오류가 발생할 수 있습니다.
이 문서의 뒷부분에 있는 [스크립트 로딩 전략](#스크립트_로딩_전략) 섹션에서 이 문제를 해결하는 방법을 배우게 됩니다.

### 브라우저 보안

각 브라우저 탭에는 코드를 실행할 수 있는 별도의 버킷이 있습니다(이러한 버킷을 전문 용어로 "실행 환경"이라고 함). 즉, 대부분의 경우 각 탭의 코드는 완전히 개별적으로 실행되며 한 탭의 코드는 다른 탭의 코드나 다른 웹사이트에 직접적인 영향을 미칠 수 없습니다.
만약 그렇지 않다면 해적들이 다른 웹사이트의 정보를 훔치는 코드를 작성하는 등 나쁜 짓을 할 수 있기 때문에 이는 좋은 보안 조치입니다.

> **참고:** 서로 다른 웹사이트/탭 간에 코드와 데이터를 안전하게 전송하는 방법이 있지만, 이는 이 강좌에서 다루지 않는 고급 기술입니다.

### 자바스크립트 실행 순서

브라우저는 자바스크립트 블록을 발견하면 일반적으로 위에서 아래로 순서대로 실행합니다.
즉, 어떤 순서에 넣을지 주의해야 합니다.
예를 들어 첫 번째 예제에서 보았던 자바스크립트 블록으로 돌아가 보겠습니다:

```js
const para = document.querySelector("p");

para.addEventListener("click", updateName);

function updateName() {
  const name = prompt("Enter a new name");
  para.textContent = `Player 1: ${name}`;
}
```

여기서는 텍스트 단락(1줄)을 선택한 다음 이벤트 리스너를 첨부(3줄)하여 단락을 클릭하면 `updateName()` 코드 블록(5-8줄)이 실행되도록 하고 있습니다. `updateName()` 코드 블록(이러한 유형의 재사용 가능한 코드 블록을 "함수"라고 함)은 사용자에게 새 이름을 요청한 다음 해당 이름을 단락에 삽입하여 표시를 업데이트합니다.

코드의 처음 두 줄의 순서를 바꾸면 더 이상 작동하지 않고 대신 [브라우저 개발자 콘솔](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools)에 `TypeError: para is undefined`라는 오류가 반환됩니다. 이는 `para` 객체가 아직 존재하지 않으므로 이벤트 리스너를 추가할 수 없음을 의미합니다.

> **참고:** 이는 매우 일반적인 오류이므로 코드에서 참조하는 객체가 존재하는지 확인한 후에 작업을 수행해야 합니다.

### 해석된 코드와 컴파일된 코드 비교

프로그래밍의 맥락에서 **해석된(interpreted)** 그리고 **컴파일된(compiled)** 용어를 들어보셨을 것입니다.
해석된 언어에서는 코드가 위에서 아래로 실행되고 코드 실행 결과가 즉시 반환됩니다.
브라우저가 코드를 실행하기 전에 코드를 다른 형태로 변환할 필요가 없습니다.
코드는 프로그래머에게 친숙한 텍스트 형식으로 수신되어 바로 처리됩니다.

반면에 컴파일된 언어는 컴퓨터에서 실행되기 전에 다른 형태로 변환(컴파일)됩니다.
예를 들어 C/C++는 기계어 코드로 컴파일된 후 컴퓨터에서 실행됩니다.
프로그램은 원래 프로그램 소스 코드에서 생성된 바이너리 형식으로 실행됩니다.

자바스크립트는 가볍게 해석되는 프로그래밍 언어입니다.
웹 브라우저는 자바스크립트 코드를 원본 텍스트 형태로 받아 스크립트를 실행합니다.
기술적 관점에서 볼 때, 대부분의 최신 JavaScript 인터프리터는 실제로 성능을 향상시키기 위해 **적시 컴파일(just-in-time compiling)**이라는 기술을 사용하는데, 스크립트가 사용되는 동안 JavaScript 소스 코드를 더 빠른 바이너리 형식으로 컴파일하여 가능한 한 빨리 실행할 수 있도록 합니다.
그러나 컴파일이 미리 처리되는 것이 아니라 런타임에 처리되기 때문에 JavaScript는 여전히 해석 언어로 간주됩니다.

두 가지 유형의 언어 모두 장점이 있지만 지금 당장 논의하지는 않겠습니다.

### 서버 측 코드와 클라이언트 측 코드

특히 웹 개발과 관련하여 **서버 측(server-side)** 코드와 **클라이언트 측(client-side)** 코드라는 용어를 들어보셨을 것입니다.
클라이언트 측 코드는 사용자의 컴퓨터에서 실행되는 코드로, 웹 페이지를 볼 때 페이지의 클라이언트 측 코드가 다운로드된 다음 브라우저에서 실행되어 표시됩니다.
이 모듈에서는 **클라이언트 측 자바스크립트**에 대해 명시적으로 이야기합니다.

반면에 서버 측 코드는 서버에서 실행되고 그 결과가 다운로드되어 브라우저에 표시됩니다.
널리 사용되는 서버 측 웹 언어의 예로는 PHP, 파이썬, 루비, ASP.NET, 심지어 자바스크립트까지 있습니다!
JavaScript를 서버 측 언어로 사용할 수도 있습니다(예: 널리 사용되는 Node.js 환경). 서버 측 JavaScript에 대한 자세한 내용은 [동적 웹사이트 - 서버 측 프로그래밍](/ko/docs/Learn/Server-side) 주제에서 확인할 수 있습니다.

### 동적 코드와 정적 코드

**동적**이라는 단어는 클라이언트 측 JavaScript와 서버 측 언어를 모두 설명하는 데 사용되며, 웹 페이지/앱의 디스플레이를 업데이트하여 상황에 따라 다른 내용을 표시하고 필요에 따라 새 콘텐츠를 생성하는 기능을 의미합니다.
서버 측 코드는 데이터베이스에서 데이터를 가져오는 등 서버에서 새로운 콘텐츠를 동적으로 생성하는 반면, 클라이언트 측 자바스크립트는 새 HTML 테이블을 생성하고 서버에서 요청한 데이터로 채운 다음 사용자에게 표시되는 웹 페이지에 테이블을 표시하는 등 클라이언트 브라우저 내부에서 새로운 콘텐츠를 동적으로 생성합니다.
두 가지 맥락에서 의미는 약간 다르지만 서로 연관되어 있으며, 일반적으로 두 가지 접근 방식(서버 측 및 클라이언트 측)이 함께 작동합니다.

동적으로 업데이트되는 콘텐츠가 없는 웹 페이지를 **정적**이라고 하며, 항상 동일한 콘텐츠만 표시합니다.

## 페이지에 JavaScript를 어떻게 추가하나요?

자바스크립트는 CSS와 비슷한 방식으로 HTML 페이지에 적용됩니다.
CSS는 외부 스타일시트를 적용하는 데 {{htmlelement("link")}} 요소를 사용하고 내부 스타일시트를 HTML에 적용하는 데 {{htmlelement("style")}} 요소를 사용하는 반면, 자바스크립트는 HTML 세계에서 {{htmlelement("script")}} 요소라는 단 하나의 친구만 있으면 됩니다.이것이 어떻게 작동하는지 알아봅시다.

### 내부 자바스크립트

1. 먼저 예제 파일 [apply-javascript.html](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/what-is-js/apply-javascript.html)의 로컬 복사본을 만듭니다. 적당한 디렉터리에 저장합니다.
2. 웹 브라우저와 텍스트 편집기에서 파일을 엽니다. HTML이 클릭 가능한 버튼이 포함된 간단한 웹 페이지를 생성하는 것을 볼 수 있습니다.
3. 다음으로 텍스트 편집기로 이동하여 닫는 `</head>` 태그 바로 앞에 head 속에 다음을 추가합니다:

   ```html
   <script>
     // JavaScript goes here
   </script>
   ```

4. 이제 {{htmlelement("script")}} 요소 안에 JavaScript를 추가하여 페이지가 좀 더 흥미로운 작업을 수행하도록 만들겠습니다. "// JavaScript goes here" 줄 바로 아래에 다음 코드를 추가합니다:

   ```js
   document.addEventListener("DOMContentLoaded", () => {
     function createParagraph() {
       const para = document.createElement("p");
       para.textContent = "You clicked the button!";
       document.body.appendChild(para);
     }

     const buttons = document.querySelectorAll("button");

     for (const button of buttons) {
       button.addEventListener("click", createParagraph);
     }
   });
   ```

5. 파일을 저장하고 브라우저를 새로 고치면 이제 버튼을 클릭하면 새 단락이 생성되어 아래에 배치되는 것을 볼 수 있습니다.

> **참고:** 예제가 작동하지 않는 것 같으면 단계를 다시 진행하여 모든 작업을 올바르게 수행했는지 확인하세요.
> 시작 코드의 로컬 사본을 `.html` 파일로 저장했나요?
> `</head>` 태그 바로 앞에 {{htmlelement("script")}} 요소를 추가했나요?
> 표시된 대로 정확하게 JavaScript를 입력했나요? **자바스크립트는 대소문자를 구분하고 매우 까다롭기 때문에 구문을 표시된 대로 정확하게 입력해야 하며, 그렇지 않으면 작동하지 않을 수 있습니다.**

> **참고:** 이 버전은 GitHub에서 [apply-javascript-internal.html](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/what-is-js/apply-javascript-internal.html)로 확인할 수 있습니다([라이브 버전도 확인 가능](https://mdn.github.io/learning-area/javascript/introduction-to-js-1/what-is-js/apply-javascript-internal.html)).

### 외부 자바스크립트

이 방법은 훌륭하게 작동하지만 JavaScript를 외부 파일에 넣으려면 어떻게 해야 할까요? 지금부터 살펴봅시다.

1. 먼저 샘플 HTML 파일과 같은 디렉터리에 새 파일을 만듭니다. 파일 이름을 `script.js`로 지정하고 파일 확장자가 .js여야 JavaScript로 인식되므로 이 확장자를 사용하세요.
2. 현재 {{htmlelement("script")}} 요소를 다음으로 바꿉니다:

   ```html
   <script src="script.js" defer></script>
   ```

3. `script.js`에 다음 스크립트를 추가합니다:

   ```js
   function createParagraph() {
     const para = document.createElement("p");
     para.textContent = "You clicked the button!";
     document.body.appendChild(para);
   }

   const buttons = document.querySelectorAll("button");

   for (const button of buttons) {
     button.addEventListener("click", createParagraph);
   }
   ```

4. 브라우저를 저장하고 새로고침하면 동일한 내용이 표시됩니다!
   동일하게 작동하지만 이제 자바스크립트가 외부 파일에 있습니다.
   이는 일반적으로 코드를 정리하고 여러 HTML 파일에서 재사용할 수 있다는 측면에서 좋은 점입니다.
   또한 HTML에 스크립트 덩어리를 덤프하지 않아도 HTML을 더 쉽게 읽을 수 있습니다.

> **참고:** 이 버전은 GitHub에서 [apply-javascript-external.html](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/what-is-js/apply-javascript-external.html) 및 [script.js](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/what-is-js/script.js)로 확인할 수 있습니다([라이브로도 확인 가능](https://mdn.github.io/learning-area/javascript/introduction-to-js-1/what-is-js/apply-javascript-external.html)).

### 인라인 자바스크립트 핸들러

가끔 HTML 안에 실제 자바스크립트 코드가 있는 경우가 있습니다.
다음과 같이 보일 수 있습니다:

```js example-bad
function createParagraph() {
  const para = document.createElement("p");
  para.textContent = "You clicked the button!";
  document.body.appendChild(para);
}
```

```html example-bad
<button onclick="createParagraph()">Click me!</button>
```

아래에서 이 버전의 데모를 사용해 볼 수 있습니다.

{{ EmbedLiveSample('Inline_JavaScript_handlers', '100%', 150) }}

이 데모는 {{htmlelement("button")}} 요소에 버튼을 눌렀을 때 함수가 실행되도록 하는 인라인 `onclick` 핸들러가 포함되어 있다는 점을 제외하면 앞의 두 섹션과 완전히 동일한 기능을 가지고 있습니다.

**하지만 이렇게 하지 마세요.** 자바스크립트로 HTML을 오염시키는 것은 나쁜 습관이며, 비효율적이므로 자바스크립트를 적용하려는 모든 버튼에 `onclick="createParagraph()"` 속성을 포함해야 합니다.

### 대신 추가 이벤트 리스너 사용

HTML에 JavaScript를 포함시키는 대신 순수 자바스크립트 구문을 사용하세요.
`querySelectorAll()` 함수를 사용하면 페이지의 모든 버튼을 선택할 수 있습니다.
그런 다음 `addEventListener()`를 사용하여 각 버튼에 핸들러를 할당하여 버튼을 반복할 수 있습니다.
이를 위한 코드는 아래와 같습니다:

```js
const buttons = document.querySelectorAll("button");

for (const button of buttons) {
  button.addEventListener("click", createParagraph);
}
```

이 속성은 `onclick` 속성보다 약간 길 수 있지만 페이지에 있는 버튼 수나 추가 또는 제거되는 버튼 수에 관계없이 모든 버튼에 적용됩니다.
자바스크립트는 변경할 필요가 없습니다.

> **참고:** `apply-javascript.html` 버전을 편집하여 파일에 버튼을 몇 개 더 추가해 보세요.
> 다시 로드하면 모든 버튼을 클릭할 때 단락이 생성되는 것을 확인할 수 있습니다.
> 깔끔하지 않나요?

### 스크립트 로딩 전략

스크립트를 적시에 로드하는 데에는 여러 가지 문제가 있습니다. 보이는 것만큼 간단한 것은 없습니다!
일반적인 문제는 페이지의 모든 HTML이 표시되는 순서대로 로드된다는 것입니다.
JavaScript를 사용하여 페이지의 요소(또는 더 정확하게는 [문서 객체 모델](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents#the_document_object_model))를 조작하는 경우 JavaScript를 로드하고 구문 분석할 때 작업을 수행하려는 HTML보다 먼저 자바스크립트가 로드되면 코드가 작동하지 않습니다.

위의 코드 예시에서 내부 및 외부 예시에서는 HTML 본문이 구문 분석되기 전에 문서 헤드에서 자바스크립트가 로드되고 실행됩니다.
이로 인해 오류가 발생할 수 있으므로 이를 해결하기 위해 몇 가지 구문을 사용했습니다.

내부 예제에서 코드 주변에서 이 구조를 확인할 수 있습니다:

```js
document.addEventListener("DOMContentLoaded", () => {
  // …
});
```

이 이벤트 리스너는 HTML 본문이 완전히 로드되고 구문 분석되었음을 나타내는 브라우저의 `DOMContentLoaded` 이벤트를 수신하는 이벤트 리스너입니다.
이 블록 내부의 자바스크립트는 해당 이벤트가 실행될 때까지 실행되지 않으므로 오류를 방지할 수 있습니다(이 과정의 뒷부분에서 [이벤트에 대해 배우게](/ko/docs/Learn/JavaScript/Building_blocks/Events) 됩니다).

외부 예시에서는 보다 최신 자바스크립트 기능인 `defer` 속성을 사용하여 문제를 해결하는데, 이 속성은 `<script>` 태그 요소에 도달하면 브라우저에 HTML 콘텐츠를 계속 다운로드하도록 지시합니다.

```html
<script src="script.js" defer></script>
```

이 경우 스크립트와 HTML이 동시에 로드되고 코드가 작동합니다.

> **참고:** 외부 사례에서는 `defer` 속성으로 문제가 해결되었기 때문에 `DOMContentLoaded` 이벤트를 사용할 필요가 없었습니다.
> 내부 자바스크립트 예제에서는 `defer`가 외부 스크립트에서만 작동하기 때문에 `defer` 솔루션을 사용하지 않았습니다.

이 문제에 대한 구식 해결책은 스크립트 요소를 본문 바로 아래(예: `</body>` 태그 바로 앞)에 배치하여 모든 HTML이 파싱된 후에 로드되도록 하는 것이었습니다.
이 솔루션의 문제점은 HTML DOM이 로드될 때까지 스크립트의 로드/구문 분석이 완전히 차단된다는 것입니다.
자바스크립트가 많은 대규모 사이트에서는 이로 인해 사이트 속도가 느려지는 중대한 성능 문제가 발생할 수 있습니다.

#### 비동기 및 지연

실제로 차단 스크립트의 문제를 우회하는 데 사용할 수 있는 두 가지 최신 기능인 `async` 및 `defer`(위에서 살펴본)이 있습니다.
이 두 가지의 차이점을 살펴보겠습니다.

`async` 속성을 사용하여 로드된 스크립트는 스크립트를 가져오는 동안 페이지를 차단하지 않고 스크립트를 다운로드합니다.
그러나 다운로드가 완료되면 스크립트가 실행되어 페이지가 렌더링되지 않도록 차단합니다.
스크립트가 특정 순서로 실행된다는 보장은 없습니다.
페이지의 스크립트가 서로 독립적으로 실행되고 페이지의 다른 스크립트에 의존하지 않는 경우 `async`를 사용하는 것이 가장 좋습니다.

`defer` 속성으로 로드된 스크립트는 페이지에 표시되는 순서대로 로드됩니다.
페이지 콘텐츠가 모두 로드될 때까지 스크립트가 실행되지 않으므로 스크립트가 페이지의 하나 이상의 요소를 수정하는 등 DOM에 의존하는 경우에 유용합니다.

다음은 다양한 스크립트 로드 방법과 해당 방법이 페이지에 미치는 영향을 시각적으로 표현한 것입니다:

![How the three script loading method work: default has parsing blocked while JavaScript is fetched and executed. With async, the parsing pauses for execution only. With defer, parsing isn't paused, but execution on happens after everything is else is parsed.](async-defer.jpg)

_이 이미지는 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 라이선스 조건에 따라 축소된 버전으로 복사 및 잘라낸 [HTML 사양](https://html.spec.whatwg.org/images/asyncdefer.svg)의 이미지입니다._

예를 들어 다음과 같은 스크립트 요소가 있는 경우입니다:

```html
<script async src="js/vendor/jquery.js"></script>

<script async src="js/script2.js"></script>

<script async src="js/script3.js"></script>
```

스크립트가 로드되는 순서에 의존할 수 없습니다.
`jquery.js`가 `script2.js` 및 `script3.js`의 앞이나 뒤에 로드될 수 있으며, 이 경우 스크립트가 실행될 때 `jquery`가 정의되지 않기 때문에 `jquery`에 따라 해당 스크립트의 모든 함수가 오류를 발생시킬 수 있습니다.

`async`는 로드할 백그라운드 스크립트가 많고 가능한 한 빨리 제자리에 배치하고 싶을 때 사용해야 합니다.
예를 들어 실제로 게임이 시작될 때 필요한 게임 데이터 파일을 로드해야 하지만 지금은 스크립트 로딩에 방해받지 않고 게임 인트로, 제목, 로비만 표시하고 싶을 수 있습니다.

`defer` 속성(아래 참조)을 사용하여 로드된 스크립트는 페이지에 표시되는 순서대로 실행되며 스크립트와 콘텐츠가 다운로드되는 즉시 실행됩니다:

```html
<script defer src="js/vendor/jquery.js"></script>

<script defer src="js/script2.js"></script>

<script defer src="js/script3.js"></script>
```

두 번째 예제에서는 `script2.js`와 `script3.js`보다 먼저 `jquery.js`가 로드되고 `script2.js`가 `script3.js`보다 먼저 로드되는 것을 확인할 수 있습니다.
페이지 콘텐츠가 모두 로드될 때까지 스크립트가 실행되지 않으므로 스크립트가 DOM에 의존하는 경우(예: 페이지의 여러 요소 중 하나를 수정하는 경우) 유용합니다.

요약하자면:

- `async` 및 `defer`은 모두 브라우저에 스크립트를 별도의 스레드에서 다운로드하도록 지시하지만, 페이지의 나머지 부분(DOM 등)이 다운로드되는 동안에는 페이지 로딩이 차단되지 않도록 합니다.
- 속성이 `async`인 스크립트는 다운로드가 완료되는 즉시 실행됩니다.
  이렇게 하면 페이지가 차단되며 특정 실행 순서가 보장되지 않습니다.
- `defer` 속성이 있는 스크립트는 순서대로 로드되며 모든 로드가 완료된 후에만 실행됩니다.
- 스크립트가 즉시 실행되어야 하고 종속성이 없는 경우 `async`를 사용하세요.
- 스크립트가 구문 분석을 기다려야 하고 다른 스크립트 및/또는 DOM의 존재 여부에 의존해야 하는 경우, `defer`를 사용하여 스크립트를 로드하고 브라우저에서 실행할 순서대로 해당 `<script>` 요소를 배치하세요.

## 주석

HTML 및 CSS와 마찬가지로 자바스크립트 코드에 브라우저에서 무시되는 주석을 작성할 수 있으며, 코드 작동 방식에 대한 지침을 동료 개발자에게 제공하기 위해 존재합니다(6개월 후에 코드를 다시 살펴보고 무엇을 했는지 기억이 나지 않는 경우).
코멘트는 매우 유용하며, 특히 대규모 애플리케이션의 경우 자주 사용해야 합니다.
주석에는 두 가지 유형이 있습니다:

- 한 줄 댓글은 이중 슬래시(//) 뒤에 작성합니다. 예

  ```js
  // I am a comment
  ```

- 여러 줄 코멘트는 /\* 및 \*/ 문자열 사이에 작성됩니다. 예


  ```js
  /*
    I am also
    a comment
  */
  ```

예를 들어, 마지막 데모의 자바스크립트에 다음과 같은 주석을 달 수 있습니다:

```js
// 함수: 새 단락을 생성하여 HTML 본문 하단에 추가합니다.

function createParagraph() {
  const para = document.createElement("p");
  para.textContent = "You clicked the button!";
  document.body.appendChild(para);
}

/*
  1. 페이지의 모든 버튼에 대한 참조를 배열 형식으로 가져옵니다.
  2. 모든 버튼을 반복하고 각 버튼에 클릭 이벤트 리스너를 추가합니다.

  버튼을 누르면 createParagraph() 함수가 실행됩니다.
*/

const buttons = document.querySelectorAll("button");

for (const button of buttons) {
  button.addEventListener("click", createParagraph);
}
```

> **참고:** 일반적으로 코멘트가 많은 것이 적은 것보다 낫지만, 변수가 무엇인지 설명하기 위해(변수 이름이 더 직관적이어야 함) 또는 매우 간단한 연산을 설명하기 위해(코드가 지나치게 복잡할 수 있음) 많은 코멘트를 추가하는 경우 주의해야 합니다.

## 요약

이제 자바스크립트의 세계로 첫발을 내디뎠습니다.
왜 자바스크립트를 사용해야 하는지, 자바스크립트로 어떤 일을 할 수 있는지에 익숙해지기 위해 이론부터 시작하겠습니다.
그 과정에서 몇 가지 코드 예제를 보고 자바스크립트가 웹사이트의 다른 코드와 어떻게 조화를 이루는지 등을 배웠습니다.

지금은 자바스크립트가 다소 어렵게 느껴질 수 있지만, 걱정하지 마세요. 이 강좌에서는 앞으로 이해할 수 있는 간단한 단계로 안내해 드리겠습니다.
다음 글에서는 [바로 실무에 뛰어들어](/ko/docs/Learn/JavaScript/First_steps/A_first_splash) 자신만의 자바스크립트 예제를 구축할 수 있도록 도와드리겠습니다.

{{NextMenu("Learn/JavaScript/First_steps/A_first_splash", "Learn/JavaScript/First_steps")}}
