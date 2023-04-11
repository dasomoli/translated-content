---
title: Manipulating documents
slug: Learn/JavaScript/Client-side_web_APIs/Manipulating_documents
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Client-side_web_APIs/Introduction", "Learn/JavaScript/Client-side_web_APIs/Fetching_data", "Learn/JavaScript/Client-side_web_APIs")}}

웹 페이지와 앱을 작성할 때 가장 흔히 하는 일 중 하나는 어떤 식으로든 문서 구조를 조작하는 것입니다. 이 작업은 일반적으로 {{domxref("Document")}} 객체를 많이 사용하는 HTML 및 스타일링 정보를 제어하기 위한 API 집합인 문서 객체 모델(DOM)을 사용하여 수행합니다. 이 글에서는 DOM을 사용하는 방법과 환경을 흥미로운 방식으로 변경할 수 있는 몇 가지 흥미로운 API를 자세히 살펴봅니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        기본적인 컴퓨터 활용 능력, HTML, CSS 및 JavaScript(JavaScript 객체 포함)에 대한 기본적인 이해가 필요합니다.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        핵심 DOM API와 DOM 및 문서 조작과 일반적으로 관련된 기타 API에 익숙해집니다.
      </td>
    </tr>
  </tbody>
</table>

## 웹 브라우저의 중요한 부분

웹 브라우저는 움직이는 부분이 많은 매우 복잡한 소프트웨어로, 웹 개발자가 JavaScript를 사용하여 제어하거나 조작할 수 없는 부분이 많습니다. 이러한 제한이 나쁜 것이라고 생각할 수도 있지만, 브라우저는 대부분 보안을 중심으로 한 좋은 이유로 잠겨 있습니다. 웹사이트가 사용자의 저장된 비밀번호나 기타 민감한 정보에 액세스하여 마치 사용자인 것처럼 웹사이트에 로그인할 수 있다고 상상해 보세요.

이러한 제한에도 불구하고 웹 API는 웹 페이지로 다양한 작업을 수행할 수 있는 많은 기능에 대한 액세스를 제공합니다. 웹 페이지 보기에 직접적으로 관련된 브라우저의 주요 부분을 나타내는 다음 다이어그램을 참조해 보세요:

![Important parts of web browser; the document is the web page. The window includes the entire document and also the tab. The navigator is the browser, which includes the window (which includes the document) and all other windows.](document-window-navigator.png)

- 창은 웹 페이지가 로드되는 브라우저 탭으로, 자바스크립트에서는 {{domxref("Window")}} 객체로 표현됩니다. 이 객체에서 사용할 수 있는 메서드를 사용하면 창 크기 반환({{domxref("Window.innerWidth")}} 및 {{domxref("Window.innerHeight")}} 참조), 해당 창에 로드된 문서 조작, 해당 문서와 관련된 데이터를 클라이언트 측에 저장(예: 로컬 데이터베이스 또는 기타 저장 메커니즘 사용), [이벤트 핸들러](/ko/docs/Learn/JavaScript/Building_blocks/Events#a_series_of_fortunate_events) 를 현재 창에 첨부하는 등의 작업을 수행할 수 있습니다.
- 내비게이터는 웹에 존재하는 브라우저(즉, 사용자 에이전트)의 상태와 신원을 나타냅니다. 자바스크립트에서는 {{domxref("Navigator")}} 객체로 표현됩니다. 이 객체를 사용하여 사용자가 선호하는 언어, 사용자 웹캠의 미디어 스트림 등을 검색할 수 있습니다
- 문서(브라우저에서 DOM으로 표시됨)는 창에 로드된 실제 페이지이며 JavaScript에서는 {{domxref("Document")}} 객체로 표시됩니다. 이 객체를 사용하여 문서를 구성하는 HTML 및 CSS에 대한 정보를 반환하고 조작할 수 있습니다(예: DOM에서 요소에 대한 참조를 가져오고, 텍스트 콘텐츠를 변경하고, 새 스타일을 적용하고, 새 요소를 만들어 현재 요소에 자식으로 추가하거나, 완전히 삭제할 수도 있습니다).

이 글에서는 주로 문서 조작에 초점을 맞추겠지만 그 외에도 몇 가지 유용한 기능을 보여드리겠습니다.

## 문서 객체 모델

현재 각 브라우저 탭에 로드된 문서는 문서 객체 모델로 표시됩니다. 이는 브라우저에서 생성한 "트리 구조"로, 프로그래밍 언어에서 HTML 구조에 쉽게 액세스할 수 있도록 해줍니다. 예를 들어 브라우저 자체에서 페이지를 렌더링할 때 올바른 요소에 스타일 및 기타 정보를 적용하는 데 사용하고, 페이지가 렌더링된 후 사용자와 같은 개발자가 JavaScript를 사용하여 DOM을 조작할 수 있습니다.

[dom-example.html](https://github.com/mdn/learning-area/blob/main/javascript/apis/document-manipulation/dom-example.html) 에 간단한 예제 페이지를 만들었습니다([라이브 페이지도 참조하세요](https://mdn.github.io/learning-area/javascript/apis/document-manipulation/dom-example.html)). 브라우저에서 이 페이지를 열어 보세요. 이 페이지는 이미지를 찾을 수 있는 {{htmlelement("section")}} 요소와 내부에 링크가 있는 단락이 포함된 매우 간단한 페이지입니다. HTML 소스 코드는 다음과 같습니다:

```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title>Simple DOM example</title>
  </head>
  <body>
    <section>
      <img
        src="dinosaur.png"
        alt="A red Tyrannosaurus Rex: A two legged dinosaur standing upright like a human, with small arms, and a large head with lots of sharp teeth." />
      <p>
        Here we will add a link to the
        <a href="https://www.mozilla.org/">Mozilla homepage</a>
      </p>
    </section>
  </body>
</html>
```

반면에 DOM은 다음과 같이 보입니다:

![Tree structure representation of Document Object Model: The top node is the doctype and HTML element. Child nodes of the HTML include head and body. Each child element is a branch. All text, even white space, is shown as well.](dom-screenshot.png)

> **참고:** 이 DOM 트리 다이어그램은 Ian Hickson의 [라이브 DOM 뷰어](https://software.hixie.ch/utilities/js/live-dom-viewer/) 를 사용하여 작성되었습니다.

트리의 각 항목을 **노드** 라고 합니다. 위 다이어그램에서 일부 노드는 요소(`HTML`, `HEAD`, `META` 등으로 식별됨)를 나타내고 다른 노드는 텍스트(`#text`로 식별됨)를 나타내는 것을 볼 수 있습니다. [다른 유형의 노드](/ko/docs/Web/API/Node/nodeType) 도 있지만, 이 두 가지가 여러분이 주로 접하게 될 노드입니다.

노드는 다른 노드에 대한 트리 내 위치로 참조되기도 합니다:

- **루트 노드**: 트리의 최상위 노드로, HTML의 경우 항상 `HTML` 노드입니다(SVG 및 사용자 정의 XML과 같은 다른 마크업 어휘는 다른 루트 요소를 갖습니다).
- **자식 노드**: 다른 노드 바로 안에 있는 노드입니다. 예를 들어 위 예제에서 `IMG`는 `SECTION`의 자식 노드입니다.
- **하위 노드**: 다른 노드 내부에 있는 노드입니다. 예를 들어, 위 예제에서 `IMG`는 `SECTION`의 자식이며 하위 노드이기도 합니다. `IMG`는 트리에서 두 레벨 아래에 있기 때문에 `BODY`의 자식은 아니지만 `BODY`의 하위 노드입니다.
- **부모 노드**: 내부에 다른 노드가 있는 노드입니다. 예를 들어, 위 예제에서 `BODY`는 `SECTION`의 부모 노드입니다.
- **형제 노드**: DOM 트리에서 같은 레벨에 있는 노드입니다. 예를 들어, 위 예제에서 `IMG`와 `P`는 형제 노드입니다.

앞으로 접하게 될 많은 코드 용어가 이 용어를 사용하므로 DOM으로 작업하기 전에 이 용어를 숙지하는 것이 유용합니다. CSS(예: 하위 선택자, 자식 선택자)를 공부했다면 이러한 용어를 접했을 수도 있습니다.

## 능동적 학습: 기본 DOM 조작

DOM 조작에 대한 학습을 시작하려면 실제 예제부터 시작하겠습니다.

1. [dom-example.html page](https://github.com/mdn/learning-area/blob/main/javascript/apis/document-manipulation/dom-example.html) 페이지와 그에 포함된 [이미지](https://github.com/mdn/learning-area/blob/main/javascript/apis/document-manipulation/dinosaur.png)  의 로컬 복사본을 가져옵니다.
2. 닫는 `</body>` 태그 바로 위에 `<script></script>` 요소를 추가합니다.
3. DOM 내부의 요소를 조작하려면 먼저 해당 요소를 선택하고 변수 안에 해당 요소에 대한 참조를 저장해야 합니다. 스크립트 요소 안에 다음 줄을 추가합니다:

   ```js
   const link = document.querySelector('a');
   ```

4. 이제 요소 참조가 변수에 저장되었으므로 요소에 사용할 수 있는 프로퍼티와 메서드를 사용하여 요소를 조작할 수 있습니다(이러한 프로퍼티와 메서드는 {{htmlelement("a")}} 요소의 경우 {{domxref("HTMLAnchorElement")}}, 보다 일반적인 상위 인터페이스인 {{domxref("HTMLElement")}}, DOM의 모든 노드를 나타내는 {{domxref("Node")}} 와 같은 인터페이스에 정의되어 있음). 먼저 {{domxref("Node.textContent")}} 속성의 값을 업데이트하여 링크 내부의 텍스트를 변경해 보겠습니다.

   ```js
   link.textContent = 'Mozilla Developer Network';
   ```

5. 또한 링크를 클릭했을 때 잘못된 위치로 이동하지 않도록 링크가 가리키는 URL을 변경해야 합니다. 하단에 다시 다음 줄을 추가합니다:

   ```js
   link.href = 'https://developer.mozilla.org';
   ```

자바스크립트에서 요소를 선택하고 변수에 해당 요소에 대한 참조를 저장하는 방법은 여러 가지가 있다는 점에 유의하세요. {{domxref("Document.querySelector()")}} 가 권장되는 최신 접근 방식입니다. CSS 선택기를 사용하여 요소를 선택할 수 있기 때문에 편리합니다. 위의 `querySelector()` 호출은 문서에 나타나는 첫 번째 {{htmlelement("a")}} 요소와 일치합니다. 여러 요소에 일치시키고 작업을 수행하려면 선택기와 일치하는 문서의 모든 요소를 일치시키고 이에 대한 참조를 {{domxref("NodeList")}} 라는 [배열](/ko/docs/Learn/JavaScript/First_steps/Arrays) 과 유사한 객체에 저장하는 {{domxref("Document.querySelectorAll()")}} 을 사용할 수 있습니다.

다음과 같이 요소 참조를 가져오는 데 사용할 수 있는 이전 메서드도 있습니다:

- {{domxref("Document.getElementById()")}} 는 지정된 `id` 속성 값을 가진 요소를 선택합니다(예: `<p id="myId">My paragraph</p>`). ID는 매개변수로 함수에 전달됩니다(예: `const elementRef = document.getElementById('myId')`).
- {{domxref("Document.getElementsByTagName()")}} 은 주어진 유형의 페이지에 있는 모든 요소(예: `<p>`들, `<a>`들 등)를 포함하는 배열과 같은 객체를 반환합니다. 요소 유형은 매개변수로 함수에 전달됩니다(예: `const elementRefArray = document.getElementsByTagName('p')`).

이 두 가지 방법은 `querySelector()`와 같은 최신 메서드보다 구형 브라우저에서 더 잘 작동하지만 편리하지는 않습니다. 다른 방법이 있는지 찾아보세요!

### 새 노드 생성 및 배치

위의 내용을 통해 무엇을 할 수 있는지 조금은 알 수 있었지만 더 나아가 새로운 요소를 만드는 방법을 살펴 보겠습니다.

1. 현재 예제로 돌아가서 {{htmlelement("section")}} 요소에 대한 참조를 가져오는 것부터 시작하겠습니다. 기존 스크립트 하단에 다음 코드를 추가합니다(다른 줄도 동일하게 수행):

   ```js
   const sect = document.querySelector('section');
   ```

2. 이제 {{domxref("Document.createElement()")}} 를 사용하여 새 단락을 만들고 이전과 같은 방식으로 텍스트 콘텐츠를 추가해 보겠습니다:

   ```js
   const para = document.createElement('p');
   para.textContent = 'We hope you enjoyed the ride.';
   ```

3. 이제 {{domxref("Node.appendChild()")}} 를 사용하여 섹션 끝에 새 단락을 추가할 수 있습니다:

   ```js
   sect.appendChild(para);
   ```

4. 마지막으로 이 부분에서는 링크가 있는 단락에 텍스트 노드를 추가하여 문장을 멋지게 마무리해 보겠습니다. 먼저 {{domxref("Document.createTextNode()")}} 를 사용해 텍스트 노드를 생성합니다:

   ```js
   const text = document.createTextNode(' — the premier source for web development knowledge.');
   ```

5. 이제 링크가 있는 단락에 대한 참조를 가져와서 텍스트 노드를 추가하겠습니다:

   ```js
   const linkPara = document.querySelector('p');
   linkPara.appendChild(text);
   ```

이것이 DOM에 노드를 추가하는 데 필요한 대부분의 메서드이며, 동적 인터페이스를 구축할 때 이러한 메서드를 많이 사용하게 될 것입니다(나중에 몇 가지 예를 살펴보겠습니다).

### 요소 이동 및 제거

노드를 이동하거나 DOM에서 노드를 완전히 삭제하고 싶을 때가 있을 수 있습니다. 이는 완벽하게 가능합니다.

링크가 있는 단락을 섹션 하단으로 이동하고 싶다면 이렇게 하면 됩니다:

```js
sect.appendChild(linkPara);
```

이렇게 하면 단락이 섹션의 맨 아래로 이동합니다. 두 번째 복사본을 만들 것이라고 생각했을 수도 있지만 그렇지 않습니다. `linkPara`는 해당 단락의 유일한 복사본에 대한 참조일 뿐입니다. 복사본을 만들어 추가하고 싶다면 대신 {{domxref("Node.cloneNode()")}} 를 사용해야 합니다.

노드를 제거하는 것도 매우 간단합니다. 적어도 제거할 노드와 그 부모 노드에 대한 참조가 있는 경우에는 말입니다. 현재 사례에서는 다음과 같이 {{domxref("Node.removeChild()")}} 를 사용하면 됩니다:

```js
sect.removeChild(linkPara);
```

노드 자체에 대한 참조만을 기반으로 노드를 제거하려는 경우(매우 일반적인 경우)에는 {{domxref("Element.remove()")}} 를 사용할 수 있습니다:

```js
linkPara.remove();
```

이 메서드는 구형 브라우저에서는 지원되지 않습니다. 구형 브라우저에는 노드 자체를 제거하도록 지시하는 메서드가 없으므로 다음을 수행해야 합니다.

```js
linkPara.parentNode.removeChild(linkPara);
```

위의 코드를 코드에 추가해 보세요.

### 스타일 조작하기

JavaScript를 통해 다양한 방법으로 CSS 스타일을 조작할 수 있습니다.

우선, 문서에 첨부된 모든 스타일시트 목록을 가져오는 {{domxref("Document.stylesheets")}} 를 사용하면 {{domxref("CSSStyleSheet")}} 객체가 포함된 배열과 같은 객체를 반환합니다. 그런 다음 원하는 대로 스타일을 추가/제거할 수 있습니다. 그러나 이러한 기능은 다소 구식이고 스타일을 조작하기 어려운 방법이기 때문에 더 이상 설명하지 않겠습니다. 훨씬 더 쉬운 방법이 있습니다.

첫 번째 방법은 동적으로 스타일을 지정하려는 요소에 직접 인라인 스타일을 추가하는 것입니다. 이 작업은 문서의 각 요소에 대한 인라인 스타일링 정보가 포함된 {{domxref("HTMLElement.style")}} 속성을 사용하여 수행됩니다. 이 객체의 속성을 설정하여 요소 스타일을 직접 업데이트할 수 있습니다.

1. 예를 들어 진행 중인 예제에 다음 줄을 추가해 보겠습니다:

   ```js
   para.style.color = 'white';
   para.style.backgroundColor = 'black';
   para.style.padding = '10px';
   para.style.width = '250px';
   para.style.textAlign = 'center';
   ```

2. 페이지를 새로고침하면 단락에 스타일이 적용된 것을 확인할 수 있습니다. 브라우저의 [페이지 검사기/DOM 검사기](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/index.html) 에서 해당 단락을 보면 이 줄이 실제로 문서에 인라인 스타일을 추가하고 있음을 알 수 있습니다:

   ```html
   <p
     style="color: white; background-color: black; padding: 10px; width: 250px; text-align: center;">
     We hope you enjoyed the ride.
   </p>
   ```

> **참고:** CSS 스타일의 JavaScript 속성 버전은 소문자로 작성되는 반면 CSS 버전은 하이픈으로 구분되어 있습니다(예: `backgroundColor` 대 `background-color`). 혼동하지 않도록 주의하세요. 그렇지 않으면 작동하지 않습니다.

문서에서 스타일을 동적으로 조작하는 또 다른 일반적인 방법이 있는데, 지금부터 살펴보겠습니다.

1. 자바스크립트에 추가한 이전 5줄을 삭제합니다.
2. HTML {{htmlelement("head")}} 안에 다음을 추가합니다:

   ```html
   <style>
     .highlight {
       color: white;
       background-color: black;
       padding: 10px;
       width: 250px;
       text-align: center;
     }
   </style>
   ```

3. 이제 일반적인 HTML 조작에 매우 유용한 메서드인 {{domxref("Element.setAttribute()")}} 를 살펴보겠습니다. 이 메서드에는 요소에 설정하려는 속성과 설정할 값이라는 두 개의 인수가 필요합니다. 이 경우 단락에 하이라이트의 클래스 이름을 설정하겠습니다:

   ```js
   para.setAttribute('class', 'highlight');
   ```

4. 페이지를 새로고침해도 변경 사항이 표시되지 않습니다. CSS는 여전히 단락에 적용되지만 이번에는 인라인 CSS 스타일이 아닌 CSS 규칙에 의해 선택된 클래스를 지정하여 적용합니다.

두 가지 방법 모두 장단점이 있으므로 어떤 방법을 선택하든 여러분의 선택에 달려 있습니다. 첫 번째 방법은 설정이 덜 필요하고 간단한 용도에 적합하지만, 두 번째 방법은 보다 순수합니다(CSS와 자바스크립트를 혼합하지 않고 인라인 스타일을 사용하지 않는 것은 나쁜 관행으로 간주됩니다). 더 크고 복잡한 앱을 구축하기 시작하면 두 번째 방법을 더 많이 사용하게 되겠지만, 이는 여러분의 선택에 달려 있습니다.

이 시점에서 우리는 실제로 유용한 작업을 수행하지 않았습니다! 정적 콘텐츠를 만드는 데 자바스크립트를 사용할 필요는 없으며, 그냥 HTML에 작성하고 자바스크립트를 사용하지 않는 것이 좋습니다. HTML보다 복잡하고 자바스크립트로 콘텐츠를 만들면 검색 엔진에서 읽을 수 없는 등 다른 문제도 발생할 수 있습니다.

다음 섹션에서는 DOM API를 보다 실용적으로 사용하는 방법을 살펴보겠습니다.

> **참고:** [완성된 버전의 dom-example.html](https://github.com/mdn/learning-area/blob/main/javascript/apis/document-manipulation/dom-example-manipulated.html) 데모는 GitHub에서 찾을 수 있습니다([라이브 버전도 참조하세요](https://mdn.github.io/learning-area/javascript/apis/document-manipulation/dom-example-manipulated.html))

## 능동적 학습: 동적 쇼핑 목록

이 챌린지에서는 양식 입력과 버튼을 사용하여 목록에 항목을 동적으로 추가할 수 있는 간단한 쇼핑 목록 예제를 만들어 보겠습니다. 입력란에 항목을 추가하고 버튼을 누릅니다:

- 해당 항목이 목록에 표시되어야 합니다.
- 각 항목에는 버튼을 눌러 목록에서 해당 항목을 삭제할 수 있는 버튼이 제공되어야 합니다.
- 입력이 비워지고 다른 항목을 입력할 수 있도록 초점이 맞춰져야 합니다.

완성된 데모는 다음과 같은 모습입니다:

![Demo layout of a shopping list. A 'my shopping list' header followed by 'Enter a new item' with an input field and 'add item' button. The list of already added items is below, each with a corresponding delete button. ](shopping-list.png)

연습을 완료하려면 아래 단계를 따르고 목록이 위에서 설명한 대로 작동하는지 확인하세요.

1. 우선 [shopping-list.html](https://github.com/mdn/learning-area/blob/main/javascript/apis/document-manipulation/shopping-list.html) 시작 파일의 사본을 다운로드하여 어딘가에 복사해 두세요. 최소한의 CSS, 레이블, 입력 및 버튼이 있는 div, 빈 목록 및 {{htmlelement("script")}} 요소가 있는 것을 볼 수 있습니다. 스크립트 내에서 모든 추가 사항을 만들 것입니다.
2. 목록({{htmlelement("ul")}}), {{htmlelement("input")}}, {{htmlelement("button")}} 요소에 대한 참조를 저장하는 세 개의 변수를 만듭니다.
3. 버튼 클릭에 대한 응답으로 실행되는 [함수](/ko/docs/Learn/JavaScript/Building_blocks/Functions) 를 만듭니다.
4. 함수 본문에서 입력 요소의 현재 [값](/ko/docs/Web/API/HTMLInputElement#properties) 을 변수에 저장하는 것으로 시작합니다.
5. 그런 다음 입력 요소의 값을 빈 문자열인 `''`로 설정하여 입력 요소를 비웁니다.
6. 목록 항목(({{htmlelement('li')}})), {{htmlelement('span')}}, {{htmlelement('button')}} 등 세 가지 요소를 새로 생성하고 변수에 저장합니다.
7. 스팬과 버튼을 목록 항목의 하위 요소로 추가합니다.
8. 스팬의 텍스트 내용을 앞서 저장한 입력 요소 값으로 설정하고 버튼의 텍스트 내용을 'Delete'로 설정합니다.
9. 목록 항목을 목록의 하위 항목으로 추가합니다.
10. 삭제 버튼에 이벤트 핸들러를 첨부하여 클릭하면 전체 목록 항목이 삭제되도록 합니다(`<li>...</li>`).
11. 마지막으로 [`focus()`](/ko/docs/Web/API/HTMLElement/focus) 메서드를 사용하여 다음 쇼핑 목록 항목을 입력할 준비가 된 입력 요소에 초점을 맞춥니다.

> **참고:** 정말 막막하다면 [완성된 쇼핑 목록](https://github.com/mdn/learning-area/blob/main/javascript/apis/document-manipulation/shopping-list-finished.html) 을 살펴보세요([실시간으로 실행되는 모습도 참조하세요](https://mdn.github.io/learning-area/javascript/apis/document-manipulation/shopping-list-finished.html)).

## 요약

문서와 DOM 조작에 대한 공부의 마지막에 도달했습니다. 이 시점에서 문서 제어 및 사용자 웹 경험의 다른 측면과 관련하여 웹 브라우저의 중요한 부분이 무엇인지 이해해야 합니다. 가장 중요한 것은 문서 객체 모델이 무엇인지, 그리고 이를 조작하여 유용한 기능을 만드는 방법을 이해해야 한다는 것입니다.

## 참조 항목

문서를 조작하는 데 사용할 수 있는 기능은 훨씬 더 많습니다. 몇 가지 레퍼런스를 확인하여 어떤 기능을 사용할 수 있는지 알아보세요:

- {{domxref("Document")}}
- {{domxref("Window")}}
- {{domxref("Node")}}
- {{domxref("HTMLElement")}}, {{domxref("HTMLInputElement")}}, {{domxref("HTMLImageElement")}}, 등.

(MDN에 문서화된 웹 API의 전체 목록은 [웹 API 색인](/ko/docs/Web/API) 을 참조하세요!)

{{PreviousMenuNext("Learn/JavaScript/Client-side_web_APIs/Introduction", "Learn/JavaScript/Client-side_web_APIs/Fetching_data", "Learn/JavaScript/Client-side_web_APIs")}}
