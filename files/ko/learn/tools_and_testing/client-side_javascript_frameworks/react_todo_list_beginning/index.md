---
title: Beginning our React todo list
slug: >-
  Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_todo_list_beginning
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_components", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}

사용자가 작업하려는 작업을 추가, 편집, 삭제할 수 있고 작업을 삭제하지 않고 완료로 표시할 수 있는 앱인 React 개념 증명을 만드는 과제를 받았다고 가정해 봅시다. 이 글에서는 나중에 추가할 개별 컴포넌트 정의와 상호작용을 준비하기 위해 기본적인 `App` 컴포넌트 구조와 스타일을 설정하는 과정을 안내합니다.

> **참고:** 코드를 버전과 비교하여 확인해야 하는 경우, 완성된 버전의 샘플 React 앱 코드를 [todo-react 리포지토리](https://github.com/mdn/todo-react) 에서 찾을 수 있습니다. 실행 중인 라이브 버전은 <https://mdn.github.io/todo-react/> 을 참조하세요.

<table>
  <tbody>
    <tr>
      <th scope="row">전제 조건:</th>
      <td>
        <p>
          핵심 <a href="/ko/docs/Learn/HTML">HTML</a>,
          <a href="/ko/docs/Learn/CSS">CSS</a>,
          <a href="/ko/docs/Learn/JavaScript">JavaScript</a> 언어에 익숙하고
          <a
            href="/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line"
            >터미널/커맨드 라인</a
          >에 대한 지식이 있어야 합니다.
        </p>
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        할 일 목록 사례 연구를 소개하고 기본적인 <code>App</code> 구조와 스타일을 익히는 것입니다.
      </td>
    </tr>
  </tbody>
</table>

## 앱의 사용자 스토리

소프트웨어 개발에서 사용자 스토리는 사용자 관점에서 실행 가능한 목표입니다. 작업을 시작하기 전에 사용자 스토리를 정의하면 작업에 집중하는 데 도움이 됩니다. 앱은 다음과 같은 스토리를 충족해야 합니다:

사용자는 다음을 수행할 수 있습니다.

- 작업 목록을 읽습니다.
- 마우스나 키보드를 사용하여 작업을 추가할 수 있습니다.
- 마우스 또는 키보드를 사용하여 작업을 완료된 것으로 표시합니다.
- 마우스 또는 키보드를 사용하여 작업을 삭제합니다.
- 마우스 또는 키보드를 사용하여 작업을 편집합니다.
- 작업의 특정 하위 집합을 봅니다: 모든 작업, 활성 작업만, 또는 완료된 작업만 보기.

이러한 이야기를 하나씩 살펴보겠습니다.

## 프로젝트 전 관리

create-react-app은 프로젝트에 전혀 사용하지 않을 파일 몇 개를 만들었습니다.

- 컴포넌트별로 스타일시트를 작성하지 않을 것이므로 먼저 `App.js`의 상단에서 `App.css` 임포트를 삭제합니다.
- `logo.svg` 파일도 사용하지 않을 것이므로 해당 가져오기 파일도 제거합니다.

그런 다음 다음 명령을 복사하여 터미널에 붙여넣어 불필요한 파일을 삭제합니다. 앱의 루트 디렉토리에서 시작해야 합니다!

```bash
# Move into the src directory of your project
cd src
# Delete a few files
rm -- App.test.js App.css logo.svg reportWebVitals.js setupTests.js
# Move back up to the root of the project
cd ..
```

참고:

- 삭제하는 파일 중 두 개는 애플리케이션 테스트용입니다. 여기서는 테스트에 대해서는 다루지 않겠습니다.
- 위에서 언급한 터미널 작업을 수행하기 위해 서버를 중지한 경우 `npm start`를 사용하여 서버를 다시 시작해야 합니다.

## 프로젝트 시작 코드

이 프로젝트의 시작점으로 지금 가지고 있는 함수를 대체할 `App()` 함수와 앱의 스타일을 지정할 CSS 두 가지를 제공하겠습니다.

### JSX

다음 스니펫을 클립보드에 복사한 다음 `기존 App()` 함수를 대체하도록 `App.js`에 붙여넣습니다:

```jsx
function App(props) {
  return (
    <div className="todoapp stack-large">
      <h1>TodoMatic</h1>
      <form>
        <h2 className="label-wrapper">
          <label htmlFor="new-todo-input" className="label__lg">
            What needs to be done?
          </label>
        </h2>
        <input
          type="text"
          id="new-todo-input"
          className="input input__lg"
          name="text"
          autoComplete="off"
        />
        <button type="submit" className="btn btn__primary btn__lg">
          Add
        </button>
      </form>
      <div className="filters btn-group stack-exception">
        <button type="button" className="btn toggle-btn" aria-pressed="true">
          <span className="visually-hidden">Show </span>
          <span>all</span>
          <span className="visually-hidden"> tasks</span>
        </button>
        <button type="button" className="btn toggle-btn" aria-pressed="false">
          <span className="visually-hidden">Show </span>
          <span>Active</span>
          <span className="visually-hidden"> tasks</span>
        </button>
        <button type="button" className="btn toggle-btn" aria-pressed="false">
          <span className="visually-hidden">Show </span>
          <span>Completed</span>
          <span className="visually-hidden"> tasks</span>
        </button>
      </div>
      <h2 id="list-heading">3 tasks remaining</h2>
      <ul
        role="list"
        className="todo-list stack-large stack-exception"
        aria-labelledby="list-heading">
        <li className="todo stack-small">
          <div className="c-cb">
            <input id="todo-0" type="checkbox" defaultChecked={true} />
            <label className="todo-label" htmlFor="todo-0">
              Eat
            </label>
          </div>
          <div className="btn-group">
            <button type="button" className="btn">
              Edit <span className="visually-hidden">Eat</span>
            </button>
            <button type="button" className="btn btn__danger">
              Delete <span className="visually-hidden">Eat</span>
            </button>
          </div>
        </li>
        <li className="todo stack-small">
          <div className="c-cb">
            <input id="todo-1" type="checkbox" />
            <label className="todo-label" htmlFor="todo-1">
              Sleep
            </label>
          </div>
          <div className="btn-group">
            <button type="button" className="btn">
              Edit <span className="visually-hidden">Sleep</span>
            </button>
            <button type="button" className="btn btn__danger">
              Delete <span className="visually-hidden">Sleep</span>
            </button>
          </div>
        </li>
        <li className="todo stack-small">
          <div className="c-cb">
            <input id="todo-2" type="checkbox" />
            <label className="todo-label" htmlFor="todo-2">
              Repeat
            </label>
          </div>
          <div className="btn-group">
            <button type="button" className="btn">
              Edit <span className="visually-hidden">Repeat</span>
            </button>
            <button type="button" className="btn btn__danger">
              Delete <span className="visually-hidden">Repeat</span>
            </button>
          </div>
        </li>
      </ul>
    </div>
  );
}
```

이제 `public/index.html`을 열고 [`<title>`](/ko/docs/Web/HTML/Element/title) 요소의 텍스트를 `TodoMatic`으로 변경합니다. 이렇게 하면 앱 상단의 [`<h1>`](/ko/docs/Web/HTML/Element/Heading_Elements) 과 일치하게 됩니다.

```html
<title>TodoMatic</title>
```

브라우저가 새로고침되면 다음과 같은 내용이 표시됩니다:

![todo-matic app, unstyled, showing a jumbled mess of labels, inputs, and buttons](unstyled-app.png)

아직 보기 흉하고 제대로 작동하지 않지만 괜찮습니다. 잠시 후에 스타일을 지정하겠습니다. 먼저 우리가 가지고 있는 JSX와 이것이 사용자 스토리에 어떻게 대응하는지 생각해 보겠습니다:

- 새 작업을 작성하기 위한 [`<input type="text">`](/ko/docs/Web/HTML/Element/input/text) 와 양식을 제출하는 버튼이 있는 [`<form>`](/ko/docs/Web/HTML/Element/form) 요소가 있습니다.
- 작업을 필터링하는 데 사용되는 버튼 배열이 있습니다.
- 남은 작업 수를 알려주는 제목이 있습니다.
- 3개의 작업이 순서 없이 목록으로 정렬되어 있습니다. 각 작업은 목록 항목([`<li>`](/ko/docs/Web/HTML/Element/li))이며, 편집 및 삭제 버튼과 완료로 체크박스를 선택할 수 있는 버튼이 있습니다.

양식을 사용하면 작업을 만들 수 있고, 버튼을 사용하면 필터링할 수 있으며, 제목과 목록은 작업을 읽을 수 있는 방법입니다. 지금은 작업을 편집할 수 있는 UI가 눈에 띄게 없습니다. 괜찮습니다. 나중에 추가할 예정입니다.

### 접근성 기능

여기서 몇 가지 특이한 속성을 발견할 수 있습니다. 예를 들어

```html
<button type="button" className="btn toggle-btn" aria-pressed="true">
  <span className="visually-hidden">Show </span>
  <span>all</span>
  <span className="visually-hidden"> tasks</span>
</button>
```

여기서 `aria-pressed`는 화면 리더와 같은 보조 기술에 버튼이 `pressed`나 `unpressed` 두 가지 상태 중 하나일 수 있음을 알려줍니다. `on`과 `off`에 대한 아날로그로 생각하면 됩니다. 값을 `true`로 설정하면 기본적으로 버튼이 눌려집니다.

`visually-hidden` 클래스는 아직 CSS를 포함하지 않았기 때문에 아무런 효과가 없습니다. 하지만 스타일을 적용하면 이 클래스가 있는 요소는 시각 장애인 사용자에게는 숨겨지지만 화면 리더 사용자에게는 계속 사용할 수 있습니다. 이는 시각 장애인 사용자에게는 이러한 단어가 필요하지 않고 추가적인 시각적 컨텍스트가 없는 화면 리더 사용자에게 버튼의 기능에 대한 자세한 정보를 제공하기 위한 것이기 때문입니다.

더 아래로 내려가면 [`<ul>`](/ko/docs/Web/HTML/Element/ul) 요소를 찾을 수 있습니다:

```html
<ul
  role="list"
  className="todo-list stack-large stack-exception"
  aria-labelledby="list-heading">
  …
</ul>
```

`role` 속성은 보조 기술이 태그가 어떤 종류의 요소를 나타내는지 설명하는 데 도움이 됩니다. `<ul>`은 기본적으로 목록처럼 취급되지만 곧 추가할 스타일은 그 기능을 깨뜨릴 것입니다. 이 역할은 `<ul>` 요소에 "list" 의미를 복원합니다. 이것이 필요한 이유에 대해 자세히 알아보려면 [Scott O'Hara의 글 "목록 수정하기"](https://www.scottohara.me/blog/2019/01/12/lists-and-safari.html) 를 참조하세요.

`aria-labelledby` 속성은 보조 기술이 목록 제목을 그 아래에 있는 목록의 목적을 설명하는 레이블로 취급하고 있음을 알려줍니다. 이렇게 연결하면 목록에 더 많은 정보를 제공하는 컨텍스트가 제공되므로 화면 리더 사용자가 목록의 목적을 더 잘 이해하는 데 도움이 될 수 있습니다.

마지막으로, 목록 항목의 레이블과 입력에는 JSX 고유의 몇 가지 속성이 있습니다:

```jsx
<input id="todo-0" type="checkbox" defaultChecked={true} />
<label className="todo-label" htmlFor="todo-0">
  Eat
</label>
```

`<input/ >` 태그의 `defaultChecked` 속성은 React가 처음에 이 체크박스를 체크하도록 지시합니다. 일반 HTML에서와 같이 `checked`를 사용한다면, React는 브라우저 콘솔에 체크박스의 이벤트 처리와 관련된 몇 가지 경고를 기록할 텐데, 이는 피하고 싶습니다. 지금은 너무 걱정하지 마세요. 나중에 이벤트를 사용할 때 이 문제를 다룰 것입니다.

`htmlFor` 속성은 HTML에서 사용되는 `for` 속성에 해당합니다. `for`는 예약어이기 때문에 JSX에서 어트리뷰트로 사용할 수 없으므로 React는 대신 `htmlFor`를 사용합니다.

참고:

- JSX 어트리뷰트에서 부울 값(`true`과 `false`)을 사용하려면 중괄호로 묶어야 합니다. `defaultChecked="true"`를 작성하면 `defaultChecked`의 값은 문자열 리터럴인 `"true"`가 됩니다. 기억하세요 - 이것은 실제로 HTML이 아니라 JavaScript입니다!
- 이전 코드 스니펫에서 사용된 `aria-pressed` 속성의 값이 `"true"`인 이유는 `aria-pressed`가 `checked`인 방식으로 진정한 부울 속성이 아니기 때문입니다.

### 스타일 구현하기

다음 CSS 코드를 `src/index.css`에 붙여넣어 현재 있는 내용을 대체합니다:

```css
/* RESETS */
*,
*::before,
*::after {
  box-sizing: border-box;
}
*:focus {
  outline: 3px dashed #228bec;
  outline-offset: 0;
}
html {
  font: 62.5% / 1.15 sans-serif;
}
h1,
h2 {
  margin-bottom: 0;
}
ul {
  list-style: none;
  padding: 0;
}
button {
  border: none;
  margin: 0;
  padding: 0;
  width: auto;
  overflow: visible;
  background: transparent;
  color: inherit;
  font: inherit;
  line-height: normal;
  -webkit-font-smoothing: inherit;
  -moz-osx-font-smoothing: inherit;
  appearance: none;
}
button::-moz-focus-inner {
  border: 0;
}
button,
input,
optgroup,
select,
textarea {
  font-family: inherit;
  font-size: 100%;
  line-height: 1.15;
  margin: 0;
}
button,
input {
  overflow: visible;
}
input[type="text"] {
  border-radius: 0;
}
body {
  width: 100%;
  max-width: 68rem;
  margin: 0 auto;
  font: 1.6rem/1.25 Arial, sans-serif;
  background-color: #f5f5f5;
  color: #4d4d4d;
}
@media screen and (min-width: 620px) {
  body {
    font-size: 1.9rem;
    line-height: 1.31579;
  }
}
/*END RESETS*/
/* GLOBAL STYLES */
.form-group > input[type="text"] {
  display: inline-block;
  margin-top: 0.4rem;
}
.btn {
  padding: 0.8rem 1rem 0.7rem;
  border: 0.2rem solid #4d4d4d;
  cursor: pointer;
  text-transform: capitalize;
}
.btn.toggle-btn {
  border-width: 1px;
  border-color: #d3d3d3;
}
.btn.toggle-btn[aria-pressed="true"] {
  text-decoration: underline;
  border-color: #4d4d4d;
}
.btn__danger {
  color: #fff;
  background-color: #ca3c3c;
  border-color: #bd2130;
}
.btn__filter {
  border-color: lightgrey;
}
.btn__primary {
  color: #fff;
  background-color: #000;
}
.btn-group {
  display: flex;
  justify-content: space-between;
}
.btn-group > * {
  flex: 1 1 49%;
}
.btn-group > * + * {
  margin-left: 0.8rem;
}
.label-wrapper {
  margin: 0;
  flex: 0 0 100%;
  text-align: center;
}
.visually-hidden {
  position: absolute !important;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap;
}
[class*="stack"] > * {
  margin-top: 0;
  margin-bottom: 0;
}
.stack-small > * + * {
  margin-top: 1.25rem;
}
.stack-large > * + * {
  margin-top: 2.5rem;
}
@media screen and (min-width: 550px) {
  .stack-small > * + * {
    margin-top: 1.4rem;
  }
  .stack-large > * + * {
    margin-top: 2.8rem;
  }
}
.stack-exception {
  margin-top: 1.2rem;
}
/* END GLOBAL STYLES */
.todoapp {
  background: #fff;
  margin: 2rem 0 4rem 0;
  padding: 1rem;
  position: relative;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
}
@media screen and (min-width: 550px) {
  .todoapp {
    padding: 4rem;
  }
}
.todoapp > * {
  max-width: 50rem;
  margin-left: auto;
  margin-right: auto;
}
.todoapp > form {
  max-width: 100%;
}
.todoapp > h1 {
  display: block;
  max-width: 100%;
  text-align: center;
  margin: 0;
  margin-bottom: 1rem;
}
.label__lg {
  line-height: 1.01567;
  font-weight: 300;
  padding: 0.8rem;
  margin-bottom: 1rem;
  text-align: center;
}
.input__lg {
  padding: 2rem;
  border: 2px solid #000;
}
.input__lg:focus {
  border-color: #4d4d4d;
  box-shadow: inset 0 0 0 2px;
}
[class*="__lg"] {
  display: inline-block;
  width: 100%;
  font-size: 1.9rem;
}
[class*="__lg"]:not(:last-child) {
  margin-bottom: 1rem;
}
@media screen and (min-width: 620px) {
  [class*="__lg"] {
    font-size: 2.4rem;
  }
}
/* Todo item styles */
.todo {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.todo > * {
  flex: 0 0 100%;
}
.todo-text {
  width: 100%;
  min-height: 4.4rem;
  padding: 0.4rem 0.8rem;
  border: 2px solid #565656;
}
.todo-text:focus {
  box-shadow: inset 0 0 0 2px;
}
/* CHECKBOX STYLES */
.c-cb {
  box-sizing: border-box;
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  font-weight: 400;
  font-size: 1.6rem;
  line-height: 1.25;
  display: block;
  position: relative;
  min-height: 44px;
  padding-left: 40px;
  clear: left;
}
.c-cb > label::before,
.c-cb > input[type="checkbox"] {
  box-sizing: border-box;
  top: -2px;
  left: -2px;
  width: 44px;
  height: 44px;
}
.c-cb > input[type="checkbox"] {
  -webkit-font-smoothing: antialiased;
  cursor: pointer;
  position: absolute;
  z-index: 1;
  margin: 0;
  opacity: 0;
}
.c-cb > label {
  font-size: inherit;
  font-family: inherit;
  line-height: inherit;
  display: inline-block;
  margin-bottom: 0;
  padding: 8px 15px 5px;
  cursor: pointer;
  touch-action: manipulation;
}
.c-cb > label::before {
  content: "";
  position: absolute;
  border: 2px solid currentcolor;
  background: transparent;
}
.c-cb > input[type="checkbox"]:focus + label::before {
  border-width: 4px;
  outline: 3px dashed #228bec;
}
.c-cb > label::after {
  box-sizing: content-box;
  content: "";
  position: absolute;
  top: 11px;
  left: 9px;
  width: 18px;
  height: 7px;
  transform: rotate(-45deg);
  border: solid;
  border-width: 0 0 5px 5px;
  border-top-color: transparent;
  opacity: 0;
  background: transparent;
}
.c-cb > input[type="checkbox"]:checked + label::after {
  opacity: 1;
}
```

저장하고 브라우저에서 다시 확인하면 이제 앱에 적절한 스타일링이 적용됩니다.

## 요약

이제 할 일 목록 앱이 실제 앱과 조금 더 비슷해졌습니다! 문제는 실제로는 아무것도 하지 않는다는 것입니다. 다음 장에서 이 문제를 해결해 보겠습니다!

{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_components", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}
