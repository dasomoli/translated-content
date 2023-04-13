---
title: Framework main features
slug: Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Main_features
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Introduction","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}

주요 자바스크립트 프레임워크는 각각 DOM 업데이트, 브라우저 이벤트 처리, 즐거운 개발자 경험 제공에 대해 서로 다른 접근 방식을 가지고 있습니다. 이 글에서는 "빅 4" 프레임워크의 주요 기능을 살펴보고, 프레임워크의 작동 방식과 프레임워크 간의 차이점을 높은 수준에서 살펴봅니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        핵심 <a href="/ko/docs/Learn/HTML">HTML</a>,
        <a href="/ko/docs/Learn/CSS">CSS</a> 및
        <a href="/ko/docs/Learn/JavaScript">JavaScript</a> 언어에 익숙해야 합니다.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>프레임워크의 주요 코드 기능을 이해합니다.</td>
    </tr>
  </tbody>
</table>

## 도메인별 언어

이 모듈에서 설명하는 모든 프레임워크는 자바스크립트로 구동되며, 모두 애플리케이션을 빌드하기 위해 도메인별 언어(DSL)를 사용할 수 있습니다. 특히 React는 컴포넌트 작성에 **JSX** 를 사용하는 것을 대중화했고, Ember는 **핸들바** 를 사용합니다. HTML과 달리 이러한 언어는 데이터 변수를 읽는 방법을 알고 있으며, 이 데이터를 사용하여 UI를 작성하는 과정을 간소화할 수 있습니다.

Angular 앱은 종종 **TypeScript** 를 많이 사용합니다. TypeScript는 사용자 인터페이스 작성과 관련이 없지만 도메인에 특화된 언어이며 바닐라 JavaScript와 상당한 차이가 있습니다.

DSL은 브라우저에서 직접 읽을 수 없으며 먼저 JavaScript 또는 HTML로 변환해야 합니다. [변환은 개발 프로세스에서 추가 단계](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Overview#transformation) 이지만 프레임워크 도구에는 일반적으로 이 단계를 처리하는 데 필요한 도구가 포함되어 있거나 이 단계를 포함하도록 조정할 수 있습니다. 이러한 도메인별 언어를 사용하지 않고도 프레임워크 앱을 빌드할 수 있지만, 프레임워크를 사용하면 개발 프로세스가 간소화되고 해당 프레임워크 관련 커뮤니티에서 도움을 더 쉽게 찾을 수 있습니다.

### JSX

JavaScript와 XML의 약자인 [JSX](https://reactjs.org/docs/introducing-jsx.html) 는 HTML과 유사한 구문을 JavaScript 환경에 제공하는 JavaScript의 확장입니다. React 팀에서 React 애플리케이션에 사용하기 위해 개발했지만, 예를 들어 Vue 앱과 같은 다른 애플리케이션을 개발하는 데에도 사용할 수 있습니다.

다음은 간단한 JSX 예제입니다:

```js
const subject = "World";
const header = (
  <header>
    <h1>Hello, {subject}!</h1>
  </header>
);
```

이 표현식은 내부에 [`<h1>`](/ko/docs/Web/HTML/Element/Heading_Elements) 요소가 있는 HTML [`<header>`](/ko/docs/Web/HTML/Element/header) 요소를 나타냅니다. 4줄의 `subject` 주위의 중괄호는 애플리케이션이 `subject` 상수의 값을 읽고 이를 `<h1>`에 삽입하도록 지시합니다.

React와 함께 사용하면 이전 스니펫의 JSX가 이것으로 컴파일됩니다:

```js
const subject = "World";
const header = React.createElement("header", null,
  React.createElement("h1", null, "Hello, ", subject, "!")
);
```

브라우저에서 최종적으로 렌더링될 때 위의 스니펫은 다음과 같은 HTML을 생성합니다:

```html
<header>
  <h1>Hello, World!</h1>
</header>
```

### Handlebars

[핸들바](https://handlebarsjs.com/) 템플릿 언어는 Ember 애플리케이션에만 국한된 것은 아니지만, Ember 앱에서 많이 활용되고 있습니다. 핸들바 코드는 HTML과 유사하지만 다른 곳에서 데이터를 가져올 수 있는 옵션이 있습니다. 이 데이터는 애플리케이션이 최종적으로 빌드하는 HTML에 영향을 미치는 데 사용될 수 있습니다.

JSX와 마찬가지로 핸들바는 중괄호를 사용하여 변수 값을 삽입합니다. 핸들바는 한 쌍이 아닌 두 쌍의 중괄호를 사용합니다.

이 핸들바 템플릿이 주어졌습니다:

```html
<header>
  <h1>Hello, \{{subject}}!</h1>
</header>
```

그리고 이 데이터:

```js
{
  subject: "World"
}
```

핸들바는 다음과 같이 HTML을 작성합니다:

```html
<header>
  <h1>Hello, World!</h1>
</header>
```

### TypeScript

[TypeScript](https://www.typescriptlang.org/) 는 자바스크립트의 상위 집합으로, 자바스크립트를 확장한다는 의미입니다. 모든 자바스크립트 코드는 유효한 타입스크립트이지만, 그 반대는 아닙니다. TypeScript는 개발자가 코드에 적용할 수 있는 엄격성 때문에 유용합니다. 예를 들어 정수 `a`와 `b`를 받아 그 합을 반환하는 `add()` 함수를 생각해 봅시다.

자바스크립트에서는 이 함수를 다음과 같이 작성할 수 있습니다:

```js
function add(a, b) {
  return a + b;
}
```

이 코드는 자바스크립트에 익숙한 사람에게는 사소할 수 있지만, 더 명확하게 이해할 수 있습니다. 자바스크립트에서는 `+` 연산자를 사용하여 문자열을 서로 연결할 수 있으므로 이 함수는 기술적으로는 `a`와 `b`가 문자열인 경우에도 여전히 작동하지만 예상한 결과를 얻지 못할 수 있습니다. 이 함수에 숫자만 전달할 수 있게 하려면 어떻게 해야 할까요? 타입스크립트를 사용하면 가능합니다:

```ts
function add(a: number, b: number) {
  return a + b;
}
```

여기서 각 매개변수 뒤에 붙은 `: number`는 TypeScript에 `a`와 `b`가 모두 숫자여야 한다는 것을 알려줍니다. 이 함수를 사용하면서 인자로 `'2'`를 전달하면 컴파일 중에 TypeScript가 오류를 발생시켜 실수를 수정해야 합니다. 이러한 오류를 발생시키는 자바스크립트를 직접 작성할 수도 있지만, 그렇게 하면 소스 코드가 훨씬 더 장황해집니다. TypeScript가 이러한 검사를 처리하도록 하는 것이 더 합리적일 수 있습니다.

## 컴포넌트 작성하기

이전 장에서 언급했듯이 대부분의 프레임워크에는 일종의 컴포넌트 모델이 있습니다. React 컴포넌트는 JSX로, Ember 컴포넌트는 핸들바를 사용하여 작성할 수 있으며, Angular 및 Vue 컴포넌트는 HTML을 가볍게 확장하는 템플릿 구문을 사용하여 작성할 수 있습니다.

컴포넌트를 작성하는 방법에 대한 의견에 관계없이 각 프레임워크의 컴포넌트는 필요한 외부 프로퍼티, 컴포넌트가 관리해야 하는 내부 상태, 사용자가 컴포넌트의 마크업에서 트리거할 수 있는 이벤트를 설명하는 방법을 제공합니다.

이 섹션의 나머지 코드 스니펫은 React를 예로 들어 JSX로 작성되었습니다

### 프로퍼티

프로퍼티 또는 **props** 은 컴포넌트가 렌더링하기 위해 필요한 외부 데이터입니다. 온라인 잡지를 위한 웹사이트를 구축하고 있는데, 기여한 각 작가가 자신의 작업에 대한 크레딧을 받을 수 있도록 해야 한다고 가정해 봅시다. 각 기사와 함께 `AuthorCredit` 컴포넌트를 만들 수 있습니다. 이 컴포넌트에는 작성자의 초상화와 간단한 바이라인이 표시되어야 합니다. 어떤 이미지를 렌더링할지, 어떤 바이라인을 인쇄할지 알기 위해 `AuthorCredit`은 몇 가지 소품을 받아들여야 합니다.

이 `AuthorCredit` 컴포넌트의 React 표현은 다음과 같이 보일 수 있습니다:

```js
function AuthorCredit(props) {
  return (
    <figure>
      <img src={props.src} alt={props.alt} />
      <figcaption>{props.byline}</figcaption>
    </figure>
  );
}
```

`{props.src}`, `{props.alt}`, `{props.byline}`은 컴포넌트에 props를 삽입할 위치를 나타냅니다. 이 컴포넌트를 렌더링하려면 렌더링할 위치(아마도 다른 컴포넌트 안에 있을 것임)에 이와 같은 코드를 작성합니다:

```js
<AuthorCredit
  src="./assets/zelda.png"
  alt="Portrait of Zelda Schiff"
  byline="Zelda Schiff is editor-in-chief of the Library Times."
/>
```

이렇게 하면 브라우저에 다음과 같은 [`<figure>`](/ko/docs/Web/HTML/Element/figure) 요소가 렌더링되며, 구조는 `AuthorCredit` 컴포넌트에 정의된 대로, 콘텐츠는 `AuthorCredit` 컴포넌트 호출에 포함된 props에 정의된 대로 렌더링됩니다:

```html
<figure>
  <img
    src="assets/zelda.png"
    alt="Portrait of Zelda Schiff"
  >
  <figcaption>
    Zelda Schiff is editor-in-chief of the Library Times.
  </figcaption>
</figure>
```

### 상태

이전 장에서 **상태** 의 개념에 대해 이야기했습니다. 강력한 상태 처리 메커니즘은 효과적인 프레임워크의 핵심이며, 각 컴포넌트에는 상태를 제어해야 하는 데이터가 있을 수 있습니다. 이 상태는 컴포넌트가 사용 중인 한 어떤 식으로든 유지됩니다. props와 마찬가지로 상태는 컴포넌트가 렌더링되는 방식에 영향을 주는 데 사용될 수 있습니다.

예를 들어 클릭 횟수를 세는 버튼이 있다고 가정해 보겠습니다. 이 컴포넌트는 자체 카운트 상태를 추적할 책임이 있으며 다음과 같이 작성할 수 있습니다:

```js
function CounterButton() {
  const [count] = useState(0);
  return (
    <button>Clicked {count} times</button>
  );
}
```

[`useState()`](https://reactjs.org/docs/hooks-reference.html#usestate) 는 초기 데이터 값이 주어지면 업데이트될 때 해당 값을 추적하는 **[React hook](https://reactjs.org/docs/hooks-intro.html)** 입니다. 코드는 처음에 브라우저에서 다음과 같이 렌더링됩니다:

```html
<button>Clicked 0 times</button>
```

`useState()` 호출은 사용자가 직접 코드를 작성할 필요 없이 앱 전체에서 강력한 방식으로 `count` 값을 추적합니다.

### 이벤트

인터랙티브한 기능을 제공하려면 컴포넌트가 브라우저 이벤트에 응답하여 애플리케이션이 사용자에게 응답할 수 있는 방법이 필요합니다. 프레임워크는 각각 브라우저 이벤트를 수신하기 위한 고유한 구문을 제공하며, 이 구문은 동등한 네이티브 브라우저 이벤트의 이름을 참조합니다.

React에서 [`click`](/ko/docs/Web/API/Element/click_event) 이벤트를 수신하려면 `onClick`이라는 특별한 프로퍼티가 필요합니다. 클릭 수를 계산할 수 있도록 위의 `CounterButton` 코드를 업데이트해 보겠습니다:

```js
function CounterButton() {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(count + 1)}>Clicked {count} times</button>
  );
}
```

이 버전에서는 추가적인 `useState()` 함수를 사용하여 특별한 `setCount()` 함수를 생성하고, 이 함수를 호출하여 `count` 값을 업데이트할 수 있습니다. 4줄에서 이 함수를 호출하고 `count`를 현재 값에 1을 더한 값으로 설정합니다.

## 컴포넌트 스타일 지정

각 프레임워크는 컴포넌트 또는 애플리케이션 전체에 대한 스타일을 정의하는 방법을 제공합니다. 컴포넌트의 스타일을 정의하는 각 프레임워크의 접근 방식은 조금씩 다르지만, 모든 프레임워크는 여러 가지 방법을 제공합니다. 몇 가지 도우미 모듈을 추가하면 프레임워크 앱의 스타일을 [Sass](https://sass-lang.com/) 또는 [Less](https://lesscss.org/) 에서 지정하거나 [PostCSS](https://postcss.org/) 로 CSS 스타일시트를 트랜스파일할 수 있습니다.

## 종속성 처리

모든 주요 프레임워크는 다른 컴포넌트 내부의 컴포넌트를 사용하여 종속성을 처리하는 메커니즘을 제공하며, 때로는 여러 계층 수준에서 종속성을 처리하기도 합니다. 다른 기능과 마찬가지로 정확한 메커니즘은 프레임워크마다 다르지만 최종 결과는 동일합니다. 컴포넌트는 표준 [자바스크립트 모듈 구문](/ko/docs/Web/JavaScript/Guide/Modules) 또는 최소한 이와 유사한 구문을 사용하여 다른 컴포넌트로 컴포넌트를 임포트하는 경향이 있습니다.

### 컴포넌트 안의 컴포넌트

컴포넌트 기반 UI 아키텍처의 주요 이점 중 하나는 컴포넌트를 함께 구성할 수 있다는 것입니다. 서로 내부에 HTML 태그를 작성하여 웹사이트를 구축할 수 있는 것처럼 다른 컴포넌트 내부에 컴포넌트를 사용하여 웹 애플리케이션을 구축할 수 있습니다. 각 프레임워크를 사용하면 다른 컴포넌트를 활용하는(따라서 의존하는) 컴포넌트를 작성할 수 있습니다.

예를 들어 `AuthorCredit` React 컴포넌트는 `Article` 컴포넌트 내에서 활용될 수 있습니다. 즉, `Article` 컴포넌트는 `AuthorCredit`을 임포트해야 합니다.

```js
import AuthorCredit from "./components/AuthorCredit";
```

이 작업이 완료되면 다음과 같이 `Article` 컴포넌트 내에서 `AuthorCredit`을 사용할 수 있습니다:

```js
// …

<AuthorCredit />

// …
```

### 종속성 주입

실제 애플리케이션에는 여러 수준의 중첩이 있는 컴포넌트 구조가 포함되는 경우가 많습니다. 여러 레벨 깊숙이 중첩된 `AuthorCredit` 컴포넌트는 어떤 이유로 애플리케이션의 최상위 레벨에서 데이터가 필요할 수 있습니다.

우리가 구축 중인 잡지 사이트가 다음과 같은 구조라고 가정해 보겠습니다:

```js
<App>
  <Home>
    <Article>
      <AuthorCredit {/* props */} />
    </Article>
  </Home>
</App>
```

`App` 컴포넌트에는 `AuthorCredit` 컴포넌트가 필요로 하는 데이터가 있습니다. `Home`과 `Article`를 다시 작성하여 props을 전달하도록 할 수도 있지만, 데이터의 출처와 목적지 사이에 많은 레벨이 있는 경우 지루할 수 있습니다. 또한 `Home`과 `Article`는 실제로 저자의 초상화나 바이라인을 사용하지 않지만, 해당 정보를 `AuthorCredit`에 포함하려면 `Home`과 `Article`를 변경하여 이를 수용해야 합니다.

여러 계층의 컴포넌트를 통해 데이터를 전달하는 문제를 prop 드릴링이라고 하며, 대규모 애플리케이션에는 적합하지 않습니다.

prop 드릴링을 피하기 위해 프레임워크는 특정 데이터를 중간 단계를 거치지 않고 필요한 컴포넌트로 직접 가져오는 방법인 종속성 주입이라는 기능을 제공합니다. 각 프레임워크는 다른 이름과 다른 방식으로 종속성 주입을 구현하지만 궁극적으로 그 효과는 동일합니다.

Angular는 이 프로세스를 [종속성 주입](https://angular.io/guide/dependency-injection) 이라고 부르고, Vue에는 [`provide()` 및 `inject()` 컴포넌트 메서드](https://v2.vuejs.org/v2/api/#provide-inject) 가 있으며, React에는 [컨텍스트 API](https://reactjs.org/docs/context.html) 가 있고, Ember는 [서비스](https://guides.emberjs.com/release/services/) 를 통해 상태를 공유합니다.

### 라이프사이클

프레임워크의 맥락에서 컴포넌트의 **라이프사이클** 는 컴포넌트가 DOM에 추가되고 브라우저에서 렌더링되는 시점(흔히 마운팅이라고 함)부터 DOM에서 제거되는 시점(흔히 언마운팅이라고 함)까지 컴포넌트가 거치는 단계의 집합을 말합니다. 프레임워크마다 이러한 라이프사이클 단계의 이름은 다르며, 모든 프레임워크에서 개발자에게 동일한 단계에 대한 액세스 권한을 부여하는 것은 아닙니다. 모든 프레임워크는 동일한 일반 모델을 따르며, 개발자는 컴포넌트가 마운트될 때, 렌더링될 때, 마운트 해제될 때, 그리고 그 사이에 있는 여러 단계에서 특정 작업을 수행할 수 있습니다.

렌더링 단계는 사용자가 애플리케이션과 상호 작용할 때 가장 많이 반복되기 때문에 이해해야 할 가장 중요한 단계입니다. 이 단계는 브라우저에 새로운 정보를 추가하거나 삭제하거나 기존 정보를 편집하는 등 브라우저에서 새로운 정보를 렌더링해야 할 때마다 실행됩니다.

이 [다이어그램은 React 컴포넌트의 라이프사이클](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/) 에 대한 일반적인 개요를 제공합니다.

## 렌더링 요소

라이프사이클과 마찬가지로 프레임워크는 애플리케이션을 렌더링하는 방식에 대해 서로 다르지만 비슷한 접근 방식을 취합니다. 모든 프레임워크는 브라우저의 현재 렌더링된 DOM 버전을 추적하며, 애플리케이션의 컴포넌트가 다시 렌더링될 때 DOM이 어떻게 변경되어야 하는지에 대해 각각 조금씩 다른 결정을 내립니다. 프레임워크가 이러한 결정을 대신 내리기 때문에 일반적으로 사용자는 DOM과 직접 상호 작용하지 않습니다. DOM에서 벗어난 추상화는 DOM을 직접 업데이트하는 것보다 더 복잡하고 메모리를 많이 사용하지만, 프레임워크가 없으면 선언적인 방식으로 프로그래밍할 수 없습니다.

**가상 DOM** 은 브라우저의 DOM에 대한 정보를 자바스크립트 메모리에 저장하는 접근 방식입니다. 애플리케이션은 이 DOM 복사본을 업데이트한 다음 "실제" DOM(사용자에게 실제로 렌더링되는 DOM)과 비교하여 무엇을 렌더링할지 결정합니다. 애플리케이션은 업데이트된 가상 DOM과 현재 렌더링된 DOM의 차이점을 비교하기 위해 "차이점"을 빌드하고, 그 차이점을 사용하여 실제 DOM에 업데이트를 적용합니다. React와 Vue는 모두 가상 DOM 모델을 활용하지만 차이점이나 렌더링할 때 정확히 동일한 로직을 적용하지는 않습니다.

[가상 DOM에 대한 자세한 내용은 React 문서에서 확인](https://reactjs.org/docs/faq-internals.html#what-is-the-virtual-dom) 할 수 있습니다.

**증분 DOM** 은 렌더링할 내용을 결정하기 위해 DOM diff를 빌드한다는 점에서 가상 DOM과 유사하지만, 자바스크립트 메모리에 DOM의 완전한 복사본을 생성하지 않는다는 점에서 다릅니다. 변경할 필요가 없는 DOM 부분은 무시합니다. 이 모듈에서 지금까지 설명한 프레임워크 중 증분 DOM을 사용하는 프레임워크는 Angular가 유일합니다.

[증분 DOM에 대한 자세한 내용은 Auth0 블로그에서 확인](https://auth0.com/blog/incremental-dom/) 할 수 있습니다.

**글리머 VM** 은 Ember만의 고유한 기능입니다. 가상 DOM이나 증분 DOM이 아니라 Ember의 템플릿을 JavaScript보다 더 쉽고 빠르게 읽을 수 있는 일종의 "바이트 코드"로 변환하는 별도의 프로세스입니다.

## 라우팅

[이전 장에서 언급했듯이 라우팅](/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Introduction#routing) 은 웹 경험의 중요한 부분입니다. 이 모듈에서 다루는 각 프레임워크는 개발자가 애플리케이션에서 클라이언트 측 라우팅을 구현하는 데 도움이 되는 라이브러리(또는 하나 이상의 라이브러리)를 제공하여 뷰가 많은 매우 복잡한 앱에서 경험이 손상되는 것을 방지합니다.

## 테스트

모든 애플리케이션은 소프트웨어가 예상한 대로 계속 작동하도록 보장하는 테스트 범위의 이점을 누릴 수 있으며, 웹 애플리케이션도 마찬가지입니다. 각 프레임워크의 에코시스템은 테스트 작성을 용이하게 하는 도구를 제공합니다. 테스트 도구는 프레임워크 자체에 내장되어 있지는 않지만 프레임워크 앱을 생성하는 데 사용되는 명령줄 인터페이스 도구를 통해 적절한 테스트 도구에 액세스할 수 있습니다.

각 프레임워크는 에코시스템에 단위 테스트 및 통합 테스트를 위한 기능을 모두 갖춘 광범위한 도구를 제공합니다.

[테스팅 라이브러리](https://testing-library.com/) 는 React, Vue, Angular 등 다양한 JavaScript 환경을 위한 도구가 포함된 테스트 유틸리티 모음입니다. Ember 문서는 [Ember 앱 테스트](https://guides.emberjs.com/release/testing/) 에 대해 다룹니다.

다음은 React 테스팅 라이브러리의 도움으로 작성한 `CounterButton`에 대한 간단한 테스트입니다. 버튼의 존재 여부, 버튼이 0번, 1번, 2번 클릭된 후 올바른 텍스트를 표시하는지 여부 등 여러 가지를 테스트합니다:

```js
import React from "react";
import { render, fireEvent } from "@testing-library/react";
import "@testing-library/jest-dom/extend-expect";

import CounterButton from "./CounterButton";

it("Renders a semantic button with an initial state of 0", () => {
  const { getByRole } = render(<CounterButton />);
  const btn = getByRole("button");

  expect(btn).toBeInTheDocument();
  expect(btn).toHaveTextContent("Clicked 0 times");
});

it("Increments the count when clicked", () => {
  const { getByRole } = render(<CounterButton />);
  const btn = getByRole("button");

  fireEvent.click(btn);
  expect(btn).toHaveTextContent("Clicked 1 times");

  fireEvent.click(btn);
  expect(btn).toHaveTextContent("Clicked 2 times");
});
```

## 요약

이쯤 되면 프레임워크로 애플리케이션을 만들 때 사용하게 될 실제 언어, 기능 및 도구에 대해 어느 정도 파악하고 있을 것입니다. 이제 실제로 코딩을 해보고 싶다는 열정이 생겼을 테니 이제부터 시작하세요! 이 시점에서 어떤 프레임워크를 먼저 배우고 싶은지 선택할 수 있습니다:

- [React](/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started)
- [Ember](/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Ember_getting_started)
- [Vue](/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_getting_started)
- [Svelte](/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_getting_started)
- [Angular](/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Angular_getting_started)

{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Introduction","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}
