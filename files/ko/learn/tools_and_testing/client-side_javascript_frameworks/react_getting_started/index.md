---
title: Getting started with React
slug: >-
  Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Main_features","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_todo_list_beginning", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}

이 글에서는 React에 대해 소개하겠습니다. 배경과 사용 사례에 대해 조금 더 자세히 알아보고, 로컬 컴퓨터에 기본 React 툴체인을 설정하고, 간단한 스타터 앱을 만들어서 사용해 보면서 그 과정에서 React의 작동 방식에 대해 조금 배워보겠습니다.

<table>
  <tbody>
    <tr>
      <th scope="row">전제 조건:</th>
      <td>
        <p>
          핵심 <a href="/ko/docs/Learn/HTML">HTML</a>,
          <a href="/ko/docs/Learn/CSS">CSS</a>,
          <a href="/ko/docs/Learn/JavaScript">JavaScript</a> 언어에 익숙해야 하며,
          <a
            href="/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line"
            >터미널/커맨드 라인</a
          >에 대한 지식이 있어야 합니다.
        </p>
        <p>
          React는 JSX(JavaScript와 XML)라는 HTML-in-JavaScript 구문을 사용합니다. HTML과 자바스크립트에 모두 익숙하면 JSX를 학습하고 애플리케이션의 버그가 자바스크립트와 관련된 것인지 아니면 React의 더 구체적인 영역과 관련된 것인지 더 잘 식별하는 데 도움이 됩니다.
        </p>
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        <p>
          로컬 React 개발 환경을 설정하고, 시작 앱을 만들고, 작동 방식의 기본 사항을 이해합니다.
        </p>
      </td>
    </tr>
  </tbody>
</table>

## 안녕하세요 React

공식 태그 라인에서 알 수 있듯이 [React](https://reactjs.org/) 는 사용자 인터페이스를 구축하기 위한 라이브러리입니다. React는 프레임워크가 아니며 웹 전용도 아닙니다. 특정 환경에 렌더링하기 위해 다른 라이브러리와 함께 사용됩니다. 예를 들어 모바일 애플리케이션을 구축하는 데 [React Native](https://reactnative.dev/) 를 사용할 수 있습니다.

웹용으로 빌드하기 위해 개발자는 React를 [ReactDOM](https://reactjs.org/docs/react-dom.html) 과 함께 사용합니다. React와 ReactDOM은 종종 다른 진정한 웹 개발 프레임워크와 같은 공간에서 논의되고 동일한 문제를 해결하는 데 활용됩니다. React를 "프레임워크"라고 부를 때는 이러한 구어체적 이해를 바탕으로 작업하고 있습니다.

React의 주요 목표는 개발자가 UI를 빌드할 때 발생하는 버그를 최소화하는 것입니다. 이를 위해 사용자 인터페이스의 일부를 설명하는 독립적이고 논리적 코드 조각인 컴포넌트를 사용합니다. 이러한 컴포넌트를 함께 구성하여 전체 UI를 만들 수 있으며, React는 렌더링 작업의 대부분을 추상화하므로 개발자는 UI 디자인에 집중할 수 있습니다.

## 사용 사례

이 모듈에서 다루는 다른 프레임워크와 달리 React는 코드 규칙이나 파일 구성에 대해 엄격한 규칙을 적용하지 않습니다. 따라서 팀은 자신에게 가장 적합한 규칙을 설정하고 원하는 방식으로 React를 채택할 수 있습니다. React는 버튼 하나, 인터페이스의 일부 또는 앱의 전체 사용자 인터페이스를 처리할 수 있습니다.

React는 [인터페이스의 작은 부분](https://reactjs.org/docs/add-react-to-a-website.html) 에 사용할 수 있지만 jQuery와 같은 라이브러리나 Vue와 같은 프레임워크처럼 애플리케이션에 "드롭인"하기가 쉽지 않으며, 전체 앱을 React로 빌드할 때 더 쉽게 접근할 수 있습니다.

또한 JSX로 인터페이스를 작성하는 등 React 앱의 많은 개발자 경험 이점에는 컴파일 프로세스가 필요합니다. 웹사이트에 바벨과 같은 컴파일러를 추가하면 웹사이트의 코드가 느리게 실행되므로 개발자는 빌드 단계에서 이러한 툴을 설정하는 경우가 많습니다. React는 툴링 요구사항이 많지만 학습할 수 있습니다.

이 글에서는 페이스북의 자체 제작 도구인 [create-react-app](https://create-react-app.dev/) 에서 제공하는 툴을 사용해 애플리케이션의 전체 사용자 인터페이스를 렌더링하는 데 React를 사용하는 사용 사례에 초점을 맞추고자 합니다.

## React는 JavaScript를 어떻게 사용하나요?

React는 많은 패턴에 최신 자바스크립트의 기능을 활용합니다. 자바스크립트에서 가장 크게 벗어난 부분은 [JSX](https://reactjs.org/docs/introducing-jsx.html) 구문을 사용한다는 점입니다. JSX는 자바스크립트의 구문을 확장하여 HTML과 유사한 코드를 함께 사용할 수 있도록 합니다. 예를 들어

```jsx
const heading = <h1>Mozilla Developer Network</h1>;
```

이 제목 상수를 **JSX 표현식** 이라고 합니다. React는 이를 사용해 앱에서 해당 [`<h1>`](/ko/docs/Web/HTML/Element/Heading_Elements) 태그를 렌더링할 수 있습니다.

시맨틱한 이유로 제목을 [`<header>`](/ko/docs/Web/HTML/Element/header) 태그로 감싸고 싶다고 가정해 봅시다. JSX 접근 방식을 사용하면 HTML에서와 마찬가지로 엘리먼트를 서로 중첩할 수 있습니다:

```jsx
const header = (
  <header>
    <h1>Mozilla Developer Network</h1>
  </header>
);
```

> **참고:** 이전 스니펫의 괄호는 JSX에 고유하지 않으며 애플리케이션에 아무런 영향을 미치지 않습니다. 괄호는 내부에 있는 여러 줄의 코드가 동일한 표현식의 일부라는 것을 사용자(및 컴퓨터)에게 알려주는 신호입니다. 헤더 표현식을 다음과 같이 작성할 수도 있습니다:
>
> ```jsx
> const header = <header>
>     <h1>Mozilla Developer Network</h1>
> </header>
> ```
>
> 그러나 표현식을 시작하는 [`<header>`](/ko/docs/Web/HTML/Element/header) 태그가 해당 닫는 태그와 같은 위치에 들여쓰기가 되어 있지 않기 때문에 다소 어색해 보입니다.

물론 브라우저는 도움 없이는 JSX를 읽을 수 없습니다. ([Babel](https://babeljs.io/) 이나 [Parcel](https://parceljs.org/) 과 같은 도구를 사용하여) 컴파일하면 헤더 표현식은 다음과 같이 보일 것입니다:

```jsx
const header = React.createElement("header", null,
  React.createElement("h1", null, "Mozilla Developer Network")
);
```

컴파일 단계를 건너뛰고 [`React.createElement()`](https://reactjs.org/docs/react-api.html#createelement) 를 사용해 UI를 직접 작성할 수도 있습니다. 하지만 이렇게 하면 JSX의 선언적 이점을 잃게 되고 코드가 읽기 어려워집니다. 컴파일은 개발 프로세스의 추가 단계이지만, React 커뮤니티의 많은 개발자는 JSX의 가독성이 그만한 가치가 있다고 생각합니다. 또한 최신 프런트엔드 개발에는 거의 항상 빌드 프로세스가 포함되기 때문에 구형 브라우저와 호환되도록 최신 구문을 다운레벨링해야 하며, 로딩 성능을 최적화하기 위해 코드를 [minify](/ko/docs/Glossary/Minification) 해야 할 수도 있습니다. Babel과 같은 인기 있는 도구는 이미 JSX를 기본적으로 지원하므로 원하지 않는 한 컴파일을 직접 구성할 필요가 없습니다.

JSX는 HTML과 JavaScript가 혼합되어 있기 때문에 일부 개발자는 직관적이라고 생각합니다. 다른 사람들은 혼합된 특성 때문에 혼란스럽다고 말합니다. 하지만 익숙해지면 사용자 인터페이스를 더 빠르고 직관적으로 구축할 수 있고 다른 사람들이 코드베이스를 한 눈에 더 잘 이해할 수 있습니다.

JSX에 대해 자세히 알아보려면 React 팀의 [JSX 심층](https://reactjs.org/docs/jsx-in-depth.html) 문서를 확인하세요.

## 첫 번째 React 앱 설정하기

React를 사용하는 방법은 여러 가지가 있지만, 여기서는 앞서 설명한 것처럼 명령줄 인터페이스(CLI) 도구 create-react-app을 사용해 몇 가지 패키지를 설치하고 일부 파일을 생성하고 위에서 설명한 툴을 처리하여 React 애플리케이션을 개발하는 과정을 빠르게 진행할 것입니다.

[create-react-app 없이도](https://reactjs.org/docs/add-react-to-a-website.html) HTML 파일에 일부 [`<script>`](/ko/docs/Web/HTML/Element/script) 요소를 복사하여 웹사이트에 React를 추가할 수 있지만, create-react-app CLI는 React 애플리케이션의 일반적인 시작점입니다. 이를 사용하면 앱을 빌드하는 데 더 많은 시간을 할애할 수 있고 설정으로 인한 번거로움을 줄일 수 있습니다.

### 요구 사항

create-react-app를 사용하려면 [Node.js](https://nodejs.org/en/) 가 설치되어 있어야 합니다. 장기 지원(LTS) 버전을 사용하는 것이 좋습니다. 노드에는 npm(노드 패키지 관리자)과 npx(노드 패키지 런처)가 포함됩니다.

Yarn 패키지 관리자를 대안으로 사용할 수도 있지만 이 튜토리얼에서는 npm을 사용한다고 가정하겠습니다. npm과 Yarn에 대한 자세한 내용은 [패키지 관리 기본 사항](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management) 을 참조하세요.

Windows를 사용하는 경우 이 튜토리얼에서 언급된 터미널 명령을 사용하려면 Unix/macOS 터미널과 동등하게 사용할 수 있도록 몇 가지 소프트웨어를 설치해야 합니다. **Gitbash**([Windows용 git 도구 집합](https://gitforwindows.org/) 의 일부로 제공됨) 또는 **[Linux용 Windows 서브시스템](https://docs.microsoft.com/windows/wsl/about)**(**WSL**)이 모두 적합합니다. 이러한 명령어와 터미널 명령어 전반에 대한 자세한 내용은 [명령줄 크래시 코스](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line) 를 참조하세요.

또한 React와 ReactDOM은 일부 폴리필을 통해 상당히 최신 브라우저인 IE9+에서만 작동하는 앱을 생성한다는 점을 염두에 두세요. 이 튜토리얼을 진행할 때는 파이어폭스, 마이크로소프트 엣지, 사파리, 크롬과 같은 최신 브라우저를 사용하는 것이 좋습니다.

자세한 내용은 다음을 참조하세요:

- [npm 블로그의 "npm 소개"](https://docs.npmjs.com/about-npm/)
- [npm 블로그의 "npx 소개"](https://blog.npmjs.org/post/162869356040/introducing-npx-an-npm-package-runner)
- [create-react-app 문서](https://create-react-app.dev/)

### 앱 초기화하기

create-react-app는 앱에 붙일 이름을 하나의 인자로 받습니다. create-react-app는 이 이름을 사용하여 새 디렉터리를 만든 다음 그 안에 필요한 파일을 만듭니다. 하드 드라이브에서 앱을 저장할 위치로 `cd`한 다음 터미널에서 다음을 실행합니다:

```bash
npx create-react-app moz-todo-react
```

이렇게 하면 `moz-todo-react` 디렉토리가 생성되고 그 안에서 몇 가지 작업을 수행합니다:

- 앱의 기능에 필수적인 몇 가지 npm 패키지를 설치합니다.
- 애플리케이션을 시작하고 제공하기 위한 스크립트를 작성합니다.
- 기본 앱 아키텍처를 정의하는 파일과 디렉터리 구조를 생성합니다.
- 컴퓨터에 git이 설치되어 있는 경우 디렉터리를 git 리포지토리로 초기화합니다.

> **참고:** Yarn 패키지 매니저가 설치되어 있는 경우, create-react-app은 기본적으로 npm 대신 이 패키지 매니저를 사용합니다. 두 패키지 매니저가 모두 설치되어 있고 명시적으로 npm을 사용하려면 create-react-app을 실행할 때 `--use-npm` 플래그를 추가하면 됩니다:
>
> ```bash
> npx create-react-app moz-todo-react --use-npm
> ```

create-react-app이 작동하는 동안 터미널에 여러 메시지가 표시될 것이며 이는 정상입니다! 몇 분 정도 걸릴 수 있으니 지금이 차 한 잔 마시기에 좋은 시간일 수 있습니다.

프로세스가 완료되면 `moz-todo-react` 디렉터리에 `cd`를 넣고 `npm start` 명령을 실행합니다. create-react-app에 의해 설치된 스크립트가 localhost:3000의 로컬 서버에서 제공되기 시작하고 새 브라우저 탭에서 앱을 엽니다. 브라우저에 다음과 같은 화면이 표시됩니다:

![Screenshot of Firefox MacOS, open to localhost:3000, showing the default create-react-app application](default-create-react-app.png)

### 애플리케이션 구조

create-react-app은 React 애플리케이션을 개발하는 데 필요한 모든 것을 제공합니다. 초기 파일 구조는 다음과 같습니다:

```
moz-todo-react
├── README.md
├── node_modules
├── package.json
├── package-lock.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    ├── reportWebVitals.js
    └── setupTests.js
```

**`src`** 디렉터리는 애플리케이션의 소스 코드가 있는 곳이기 때문에 대부분의 시간을 보내게 될 곳입니다.

**`public`** 디렉토리에는 앱을 개발하는 동안 브라우저에서 읽게 될 파일들이 있는데, 그중 가장 중요한 파일은 `index.html`입니다. React는 브라우저가 코드를 실행할 수 있도록 이 파일에 코드를 삽입합니다. create-react-app 함수에 도움이 되는 몇 가지 다른 마크업이 있으므로, 여러분이 무엇을 하고 있는지 모른다면 편집하지 않도록 주의하세요. 이 파일의 [`<title>`](/ko/docs/Web/HTML/Element/title) 요소 안의 텍스트를 애플리케이션의 제목을 반영하도록 변경해야 합니다. 정확한 페이지 제목은 접근성을 위해 중요합니다!

`public` 디렉토리는 앱의 프로덕션 버전을 빌드하고 배포할 때에도 게시됩니다. 이 튜토리얼에서는 배포에 대해 다루지 않지만 [앱 배포](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Deployment) 튜토리얼에서 설명한 것과 유사한 솔루션을 사용할 수 있습니다.

`package.json` 파일에는 Node.js/npm이 프로젝트를 정리하는 데 사용하는 프로젝트에 대한 정보가 포함되어 있습니다. 이 파일은 React 애플리케이션에 고유한 것이 아니며, create-react-app은 단지 이 파일을 채울 뿐입니다. 이 튜토리얼을 완료하기 위해 이 파일을 전혀 이해할 필요는 없지만, 자세한 내용을 알고 싶다면 [npm 블로그에서 package.json](https://docs.npmjs.com/cli/v9/configuring-npm/package-json/) 을 읽어보거나 [패키지 관리 기본](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management) 튜토리얼에서도 이에 대해 설명합니다.

## 첫 번째 React 컴포넌트 - \<App/> 살펴보기

React에서 **컴포넌트** 는 앱의 일부를 렌더링하는 재사용 가능한 모듈입니다. 이러한 컴포넌트는 크거나 작을 수 있지만 일반적으로 명확하게 정의되어 있으며 하나의 분명한 목적을 수행합니다.

브라우저에서 편집하라는 메시지가 표시되므로 `src/App.js`를 열어 보겠습니다. 이 파일에는 첫 번째 컴포넌트인 `App`과 몇 줄의 다른 코드가 포함되어 있습니다:

```jsx
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
export default App;
```

`App.js` 파일은 크게 세 부분으로 구성됩니다. 상단에 몇 개의 [`import`](/ko/docs/Web/JavaScript/Reference/Statements/import) 문, 중간에 `App` 컴포넌트, 하단에 [`export`](/ko/docs/Web/JavaScript/Reference/Statements/export) 문이 있습니다. 대부분의 React 컴포넌트는 이 패턴을 따릅니다.

### import 문

파일 상단의 `import` 문을 사용하면 `App.js`에서 다른 곳에 정의된 코드를 사용할 수 있습니다. 이 문들을 좀 더 자세히 살펴보겠습니다.

```jsx
import logo from './logo.svg';
import './App.css';
```

첫 번째 문은 `'./logo.svg'`에서 로고를 가져옵니다. 경로의 시작 부분에 `./`가 있고 끝에 `.svg` 확장자가 있는 것을 주목하세요. 이는 파일이 로컬 파일이며 JavaScript 파일이 아님을 나타냅니다. 실제로 `logo.svg` 파일은 소스 디렉토리에 있습니다.

두 번째 문은 App 컴포넌트와 관련된 CSS를 가져옵니다. 변수 이름과 `from` 지시어가 없다는 점에 유의하세요. 이를 [_side-effect import_](/ko/docs/Web/JavaScript/Reference/Statements/import#import_a_module_for_its_side_effects_only) 라고 하는데, 자바스크립트 파일로 값을 가져오지는 않지만 번들러인 Webpack에게 참조된 CSS 파일을 최종 CSS 번들에 추가하도록 지시합니다.

2020년 React 17 릴리스 이전의 React 릴리스에서는 `import React from 'react'`하는 것처럼 React 라이브러리 자체도 임포트해야 했습니다. 이 단계를 건너뛰면 오류가 발생했습니다: React는 우리가 작성한 JSX를 `React.createElement()`로 변환했기 때문에 모든 React 컴포넌트는 `React` 모듈을 임포트해야 했습니다. React 17에서는 이 문장을 불필요하게 만드는 새롭게 재작성된 JSX 트랜스폼 버전이 도입되었으며, React 16.14.0, React 15.7.0 및 React 0.14.10에 백포트되었습니다([공식 React 문서](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html) 에서 자세한 내용을 읽어보세요).

### App 컴포넌트

임포트가 끝나면 `App`이라는 함수가 있습니다. 대부분의 자바스크립트 커뮤니티는 `helloWorld`와 같은 대소문자 이름을 선호하지만, React 컴포넌트는 `HelloWorld`와 같은 파스칼 대문자 변수 이름을 사용해 주어진 JSX 엘리먼트가 일반 HTML 태그가 아닌 React 컴포넌트라는 것을 명확히 합니다. `App` 함수의 이름을 `app`으로 바꾸면 브라우저에 오류가 표시됩니다.

`App`을 좀 더 자세히 살펴봅시다.

```jsx
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```

`App` 함수는 JSX 표현식을 반환합니다. 이 표현식은 브라우저가 최종적으로 DOM에 렌더링하는 내용을 정의합니다.

표현식의 일부 요소에는 HTML에서와 마찬가지로 `attribute="value"` 패턴에 따라 작성된 속성이 있습니다. 3줄의 첫 번째 [`<div>`](/ko/docs/Web/HTML/Element/div) 태그에는 `className` 속성이 있습니다. 이 어트리뷰트는 HTML의 [`class`](/ko/docs/Web/HTML/Global_attributes/class) 어트리뷰트와 동일하지만 JSX는 자바스크립트이기 때문에 `class`라는 단어를 사용할 수 없습니다. 클래스라는 단어는 예약어로, 자바스크립트에서 이미 특정 용도로 사용하고 있으며 여기 코드에서 문제를 일으킬 수 있습니다. 몇 가지 다른 HTML 어트리뷰트도 같은 이유로 JSX에서 HTML과 다르게 작성됩니다. 이 부분은 나중에 다루도록 하겠습니다.

잠시 시간을 내어 6번째 줄의 [`<p>`](/ko/docs/Web/HTML/Element/p) 태그를 "Hello, World!"라고 표시되도록 변경한 다음 파일을 저장합니다. 브라우저의 `http://localhost:3000` 에서 실행 중인 개발 서버에서 이 변경 사항이 즉시 렌더링되는 것을 확인할 수 있습니다. 이제 [`<a>`](/ko/docs/Web/HTML/Element/a) 태그를 삭제하고 저장하면 "Learn React" 링크가 사라집니다.

이제 `App` 컴포넌트가 다음과 같이 보일 것입니다:

```jsx
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Hello, World!
        </p>
      </header>
    </div>
  );
}
```

### Export 문

`App.js` 파일의 맨 아래에 있는 `export default App` 문은 다른 모듈에서 `App` 컴포넌트를 사용할 수 있도록 합니다.

## 인덱스 조회

`App` 컴포넌트가 사용되는 곳이므로 `src/index.js`를 열어 보겠습니다. 이 파일은 앱의 진입점이며 처음에는 다음과 같이 보입니다:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

`App.js`와 마찬가지로 파일은 실행에 필요한 모든 JS 모듈과 기타 에셋을 임포트하는 것으로 시작됩니다.

처음 두 문은 파일의 뒷부분에서 참조되기 때문에 `React` 및 `ReactDOM` 라이브러리를 임포트합니다. 이 라이브러리들은 로컬 파일이 아니기 때문에 가져올 때 경로나 확장자를 작성하지 않습니다. 실제로 `package.json` 파일에 종속성으로 나열됩니다. 이 레슨을 진행하면서 이 구분을 주의하세요!

`index.css`에는 전체 앱에 적용되는 글로벌 스타일이 있습니다. 또한 `App.js` 하단에 있는 `export` 문 덕분에 `App` 컴포넌트를 가져올 수 있습니다.

7행에서는 컴포넌트를 렌더링할 DOM 엘리먼트(이 경우 `root`라는 ID를 가진 엘리먼트)를 가지고 React의 `ReactDOM.createRoot()` 함수를 호출합니다. `public/index.html` 내부를 살펴보면 `<body>` 바로 안쪽에 `<div>` 엘리먼트가 있는 것을 볼 수 있습니다. React는 이 노드에 대한 루트를 생성하고 그 안에 있는 DOM을 관리합니다([공식 react 문서](https://beta.reactjs.org/apis/react-dom/client/createRoot) 에서 자세히 읽어보세요). 이 함수는 React 엘리먼트를 DOM에 `render`하는 데 사용할 수 있는 `root`를 반환합니다.

8행에서는 렌더링하려는 컴포넌트(이 경우 `<App />`)로 `root.render()`를 호출합니다.

이 모든 것은 `App` 컴포넌트를 루트 또는 첫 번째 컴포넌트로 사용하여 React 애플리케이션을 렌더링하고 싶다는 것을 React에 알려줍니다.

> **참고:** JSX에서 React 컴포넌트와 HTML 엘리먼트에는 닫는 슬래시가 있어야 합니다. `<App>`이나 `<img>`만 쓰면 오류가 발생합니다.

[`reportWebVitals`](https://create-react-app.dev/docs/measuring-performance/) 는 웹 페이지의 사용자 경험을 캡처하는 데 유용한 메트릭 집합이지만 이 문서에서는 다루지 않습니다. 해당 가져오기 줄과 `reportWebVitals();` 줄을 삭제할 수 있습니다.

최종 `index.js` 파일은 다음과 같아야 합니다:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(<App />);
```

## 변수와 props

다음으로 몇 가지 자바스크립트 기술을 사용해 React에서 컴포넌트를 편집하고 데이터로 작업하는 것을 좀 더 편하게 해보겠습니다. JSX 내에서 변수가 어떻게 사용되는지 살펴보고, 컴포넌트에 데이터를 전달하는 방법(변수를 사용해 접근할 수 있는)인 props를 소개하겠습니다.

### JSX의 변수

`App.js`로 돌아와서 8행에 집중해 보겠습니다:

```jsx
<img src={logo} className="App-logo" alt="logo" />
```

여기서 `<img />` 태그의 `src` 속성 값은 중괄호 안에 있습니다. 이것이 JSX가 변수를 인식하는 방식입니다. React는 `{logo}`를 보고 앱의 2번째 줄에서 로고 가져오기를 참조하고 있음을 인식한 다음 로고 파일을 검색하고 렌더링합니다.

직접 변수를 만들어 봅시다. `App`의 반환문 앞에 `const subject = 'React';` 를 추가합니다. 이제 `App` 컴포넌트는 다음과 같이 보일 것입니다:

```jsx
function App() {
  const subject = "React";
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Hello, World!
        </p>
      </header>
    </div>
  );
}
```

8번째 줄을 다음과 같이 "World"라는 단어 대신 `subject` 변수를 사용하도록 변경합니다:

```jsx
function App() {
  const subject = "React";
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Hello, {subject}!
        </p>
      </header>
    </div>
  );
}
```

저장하면 브라우저에 "Hello, World!" 대신 "Hello, React!"가 표시되어야 합니다.

변수는 편리하지만 방금 설정한 변수는 React의 기능을 잘 활용하지 못합니다. 이때 props가 필요합니다.

### 컴포넌트 props

**prop** 는 React 컴포넌트에 전달되는 모든 데이터입니다. React props는 HTML 어트리뷰트에 비유할 수 있습니다. HTML 엘리먼트에 어트리뷰트가 있다면, React 컴포넌트에는 props가 있습니다. props는 컴포넌트 호출 안에 작성되며, HTML 어트리뷰트와 동일한 구문(`prop="value"`)을 사용합니다. React에서 데이터 흐름은 단방향입니다. 부모 컴포넌트에서 자식 컴포넌트로만 props를 전달할 수 있으며, 프로퍼티는 읽기 전용입니다.

`index.js`를 열고 `<App/>` 호출에 첫 번째 prop을 지정해 봅시다.

`<App/>` 컴포넌트 호출에 `subject`의 prop을 추가하고 값은 `Clarice`로 지정합니다. 완료되면 코드가 다음과 같이 보일 것입니다:

```jsx
root.render(<App subject="Clarice" />);
```

`App.js`로 돌아가서 다음과 같이 표시되는 App 함수 자체를 다시 살펴봅시다(간결성을 위해 `return` 문을 줄임):

```jsx
function App() {
  const subject = "React";
  return (
    // return statement
  );
}
```

`App` 함수의 시그니처를 변경하여 매개변수로 props를 허용하도록 하고, `subject` const를 삭제합니다.
다른 함수 매개변수와 마찬가지로 `console.log()`에 `props`를 넣어 브라우저의 콘솔에 인쇄할 수 있습니다. 다음과 같이 반환 문 앞에 이 작업을 수행합니다:

```jsx
function App(props) {
  console.log(props);
  return (
    // return statement
  );
}
```

이 변경으로 {subject}가 정의되지 않게 되므로 지금은 `Hello, {subject}!` 줄을 주석 처리하세요.
파일을 저장하고 브라우저의 JavaScript 콘솔을 확인합니다. 다음과 같은 내용이 기록되어 있을 것입니다:

```
Object { subject: "Clarice" }
```

객체 속성 `subject`는 `<App />` 컴포넌트 호출에 추가한 `subject` 프로퍼티에 해당하며, 문자열 `Clarice`는 그 값에 해당합니다. React의 컴포넌트 props는 항상 이런 방식으로 객체로 수집됩니다.

이제 `subject`가 props 중 하나가 되었으니 `App.js`에서 이를 활용해 봅시다. `subject` 상수를 문자열 `React`로 정의하는 대신 `props.subject`의 값을 읽도록 변경합니다. 이제 `Hello, {subject}!` 줄의 주석 처리를 해제하고 원하는 경우 `console.log()`를 삭제할 수도 있습니다.

```jsx
function App(props) {
  const subject = props.subject;
  return (
    // return statement
  );
}
```

저장하면 이제 앱이 "Hello, Clarice!"라고 인사합니다. `index.js`로 돌아가서 `subject` 값을 편집하고 저장하면 텍스트가 변경됩니다. 이 변경 과정에서 `Hello` 줄을 그대로 유지하려면 JSX 변수를 `{props.subject}`로 업데이트할 수도 있습니다.

## 요약

로컬에 설치하는 방법, 스타터 앱을 만드는 방법, 기본 작동 방식 등 React에 대한 첫 번째 살펴보기가 끝났습니다. 다음 글에서는 첫 번째 제대로 된 애플리케이션인 할 일 목록을 만들어 보겠습니다. 하지만 그 전에 지금까지 배운 내용 중 몇 가지를 요약해 보겠습니다.

React에서:

- 컴포넌트는 필요한 모듈을 import 할 수 있으며 파일 하단에 반드시 export 해야 합니다.
- 컴포넌트 함수는 `PascalCase`로 명명됩니다.
- JSX 변수는 `{so}`와 같이 중괄호 사이에 넣으면 읽을 수 있습니다.
- 일부 JSX 속성은 HTML 속성과 다르므로 JavaScript 예약어와 충돌하지 않습니다. 예를 들어 HTML의 `class`는 JSX에서 `className`으로 변환됩니다. 다중 단어 어트리뷰트는 `camelCase` 입니다.
- Props는 컴포넌트 호출 내부의 어트리뷰트처럼 작성되며 컴포넌트에 전달됩니다.

{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Main_features","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_todo_list_beginning", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}
