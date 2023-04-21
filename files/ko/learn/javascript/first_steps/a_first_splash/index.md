---
title: A first splash into JavaScript
slug: Learn/JavaScript/First_steps/A_first_splash
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/First_steps/What_is_JavaScript", "Learn/JavaScript/First_steps/What_went_wrong", "Learn/JavaScript/First_steps")}}

이제 자바스크립트의 이론과 자바스크립트로 무엇을 할 수 있는지에 대해 배웠으니 이제 간단한 자바스크립트 프로그램을 만드는 과정을 실습 튜토리얼을 통해 안내해 드리겠습니다. 여기서는 간단한 "숫자 맞추기" 게임을 단계별로 만들 것입니다.

<table>
  <tbody>
    <tr>
      <th scope="row">전제 조건:</th>
      <td>
        기본적인 컴퓨터 활용 능력, HTML과 CSS에 대한 기본적인 이해, 자바스크립트가 무엇인지에 대한 이해가 필요합니다.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        약간의 자바스크립트 작성 경험을 쌓고, 자바스크립트 프로그램 작성에 대해 최소한 기본적인 이해가 필요합니다.
      </td>
    </tr>
  </tbody>
</table>

여기서 정말 명확한 기대치를 설정하고 싶습니다: 이 글이 끝날 때까지 JavaScript를 배우거나 작성하라는 코드를 모두 이해해야 하는 것은 아닙니다. 대신 자바스크립트의 기능들이 어떻게 함께 작동하는지, 자바스크립트를 작성하는 것이 어떤 느낌인지에 대한 아이디어를 제공하고자 합니다. 다음 글에서는 여기에 소개된 모든 기능을 훨씬 더 자세히 살펴볼 예정이니 당장 이해가 되지 않더라도 걱정하지 마세요!

> **참고:** JavaScript에서 볼 수 있는 코드 기능의 대부분은 함수, 루프 등 다른 프로그래밍 언어와 동일합니다. 코드 구문은 달라 보이지만 개념은 거의 동일합니다.

## 프로그래머처럼 생각하기

프로그래밍에서 가장 배우기 어려운 것 중 하나는 구문을 배우는 것이 아니라 실제 문제를 해결하기 위해 구문을 적용하는 방법입니다. 프로그래머처럼 생각하기 시작해야 합니다. 여기에는 일반적으로 프로그램이 수행해야 하는 작업에 대한 설명을 살펴보고, 이를 달성하기 위해 필요한 코드 기능과 이를 함께 작동시키는 방법을 알아내는 작업이 포함됩니다.

이를 위해서는 노력, 프로그래밍 구문에 대한 경험, 연습과 함께 약간의 창의력이 필요합니다. 코딩을 많이 할수록 더 잘할 수 있습니다. 5분 만에 '프로그래머의 두뇌'를 개발할 수 있다고 약속할 수는 없지만, 교육 과정 내내 프로그래머처럼 생각하는 연습을 할 수 있는 기회를 충분히 제공할 것입니다.

이를 염두에 두고 이 글에서 구축할 예제를 살펴보고 이를 실제 작업으로 분해하는 일반적인 프로세스를 검토해 보겠습니다.

## 예시 — 숫자 게임 맞추기

이 문서에서는 아래에서 볼 수 있는 간단한 게임을 구축하는 방법을 보여드리겠습니다:

{{EmbedGHLiveSample("learning-area/javascript/introduction-to-js-1/first-splash/number-guessing-game", 900, 300)}}

게임을 플레이해 보세요. 게임을 시작하기 전에 게임에 익숙해지세요.

상사가 이 게임을 만들기 위해 다음과 같은 간단한 지시를 내렸다고 가정해 보겠습니다:

> 간단한 숫자 맞추기 게임을 만들어 달라는 것입니다. 이 게임은 1에서 100 사이의 난수를 선택한 다음 플레이어가 10턴 동안 숫자를 맞히도록 도전해야 합니다. 각 턴이 끝날 때마다 플레이어에게 맞았는지 틀렸는지, 틀렸다면 추측이 너무 낮았는지 너무 높았는지 알려줘야 합니다. 또한 플레이어가 이전에 어떤 숫자를 추측했는지도 알려줘야 합니다. 플레이어가 정답을 맞히거나 턴이 다 떨어지면 게임이 종료됩니다. 게임이 종료되면 플레이어에게 다시 게임을 시작할 수 있는 옵션이 제공되어야 합니다.

이 개요를 살펴본 후 가장 먼저 할 수 있는 일은 가능한 한 프로그래머의 사고방식으로 간단한 실행 가능한 작업으로 세분화하는 것입니다:

1. 1에서 100 사이의 난수를 생성합니다.
2. 플레이어가 켜져 있는 턴 번호를 기록합니다. 1에서 시작합니다.
3. 플레이어에게 숫자가 무엇인지 추측할 수 있는 방법을 제공합니다.
4. 추측이 제출되면 먼저 사용자가 이전 추측을 볼 수 있도록 어딘가에 기록합니다.
5. 그런 다음 올바른 번호인지 확인합니다.
6. 정답이면:

   1. 축하 메시지를 표시합니다.
   2. 플레이어가 더 이상 추측을 입력할 수 없도록 차단합니다(게임이 엉망이 될 수 있음).
   3. 플레이어가 게임을 다시 시작할 수 있도록 디스플레이 컨트롤을 표시합니다.

7. 틀렸고 플레이어가 왼쪽으로 돌아간 경우::

   1. 플레이어에게 틀린 점과 추측이 너무 높거나 낮은 이유를 알려줍니다.
   2. 다른 추측을 입력할 수 있도록 합니다.
   3. 턴 수를 1씩 늘립니다.

8. 틀렸고 플레이어에게 남은 턴이 없는 경우:

   1. 플레이어에게 게임 오버라고 말합니다.
   2. 플레이어가 더 이상 추측을 입력할 수 없도록 합니다(게임이 엉망이 될 수 있습니다).
   3. 플레이어가 게임을 다시 시작할 수 있도록 컨트롤을 표시합니다.

9. 게임이 다시 시작되면 게임 로직과 UI가 완전히 리셋되었는지 확인한 다음 1단계로 돌아갑니다.

이제 이 단계를 코드로 전환하는 방법을 살펴보고 예제를 구축하며 자바스크립트 기능을 살펴보면서 앞으로 나아가겠습니다.

### 초기 설정

이 튜토리얼을 시작하려면 [number-guessing-game-start.html](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/first-splash/number-guessing-game-start.html) 파일의 로컬 복사본을 만드세요([여기에서 라이브 보기](https://mdn.github.io/learning-area/javascript/introduction-to-js-1/first-splash/number-guessing-game-start.html)). 텍스트 편집기와 웹 브라우저 모두에서 파일을 엽니다. 지금은 간단한 제목과 지침 단락, 추측을 입력하는 양식이 표시되지만, 현재 이 양식은 아무 기능도 수행하지 않습니다.

모든 코드를 추가할 위치는 HTML 하단의 {{htmlelement("script")}} 요소 안에 있습니다:

```html
<script>
  // 자바스크립트는 여기에 둡니다.
</script>
```

### 데이터를 저장할 변수 추가하기

이제 시작하겠습니다. 먼저 {{htmlelement("script")}} 요소 안에 다음 줄을 추가합니다:

```js
let randomNumber = Math.floor(Math.random() * 100) + 1;

const guesses = document.querySelector('.guesses');
const lastResult = document.querySelector('.lastResult');
const lowOrHi = document.querySelector('.lowOrHi');

const guessSubmit = document.querySelector('.guessSubmit');
const guessField = document.querySelector('.guessField');

let guessCount = 1;
let resetButton;
```

이 코드 섹션에서는 프로그램에서 사용할 데이터를 저장하는 데 필요한 변수와 상수를 설정합니다.

변수는 기본적으로 숫자나 텍스트 문자열과 같은 값의 이름입니다. `let` 키워드로 변수를 만들고 그 뒤에 변수 이름을 지정합니다.

상수도 값의 이름을 지정하는 데 사용되지만 변수와 달리 한 번 설정한 값은 변경할 수 없습니다. 이 경우 상수를 사용하여 사용자 인터페이스의 일부에 대한 참조를 저장하고 있습니다. 이러한 요소 중 일부의 텍스트는 변경될 수 있지만 각 상수는 항상 초기화된 것과 동일한 HTML 요소를 참조합니다. 상수를 생성하려면 키워드 `const` 뒤에 상수의 이름을 지정합니다.

변수나 상수에 등호 기호(=) 뒤에 원하는 값을 지정하여 값을 할당할 수 있습니다.

이 예제에서는

- 첫 번째 변수인 `randomNumber`에는 수학적 알고리즘을 사용하여 계산된 1에서 100 사이의 난수가 할당됩니다.
- 처음 세 개의 상수는 각각 HTML의 결과 단락에 대한 참조를 저장하기 위해 만들어졌으며, 코드의 뒷부분에서 단락에 값을 삽입하는 데 사용됩니다(`<div>` 요소 안에 있는 것을 주목하세요. 나중에 게임을 다시 시작할 때 재설정을 위해 세 개 모두를 선택하는 데 사용됨):

  ```html
  <div class="resultParas">
    <p class="guesses"></p>
    <p class="lastResult"></p>
    <p class="lowOrHi"></p>
  </div>
  ```

- 다음 두 상수는 양식 텍스트 입력 및 제출 버튼에 대한 참조를 저장하고 나중에 추측을 제출하는 것을 제어하는 데 사용됩니다.

  ```html
  <label for="guessField">Enter a guess: </label>
  <input type="number" id="guessField" class="guessField" />
  <input type="submit" value="Submit guess" class="guessSubmit" />
  ```

- 마지막 두 변수는 플레이어가 얼마나 많은 추측을 했는지 추적하는 데 사용되는 추측 횟수 1과 아직 존재하지 않지만 나중에 생성될 재설정 버튼에 대한 참조를 저장합니다.

> **참고:** 변수와 상수에 대해서는 [다음 글](/ko/docs/Learn/JavaScript/First_steps/Variables)부터 강좌의 뒷부분에서 더 자세히 배우게 될 것입니다.

### 함수

다음으로 이전 자바스크립트 아래에 다음을 추가합니다:

```js
function checkGuess() {
  alert('I am a placeholder');
}
```

함수는 한 번 작성하고 반복해서 실행할 수 있는 재사용 가능한 코드 블록으로, 코드를 계속 반복할 필요가 없습니다. 정말 유용한 기능입니다. 함수를 정의하는 방법에는 여러 가지가 있지만 여기서는 간단한 유형 하나에 집중하겠습니다. 여기서는 `function`라는 키워드를 사용하여 함수를 정의하고 그 뒤에 괄호로 묶은 이름을 붙였습니다. 그 뒤에 중괄호(`{ }`) 두 개를 넣습니다. 중괄호 안에는 함수를 호출할 때마다 실행하려는 모든 코드가 들어갑니다.

코드를 실행하려면 함수 이름과 괄호를 입력합니다.

이제 실행해 봅시다. 코드를 저장하고 브라우저에서 페이지를 새로고침합니다. 그런 다음 [개발자 도구 JavaScript 콘솔](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools)로 이동하여 다음 줄을 입력합니다:

```js
checkGuess();
```

<kbd>Return</kbd>/<kbd>Enter</kbd>를 누르면 `I am a placeholder`라는 경고가 표시될 것입니다. 코드에서 함수를 호출할 때마다 경고를 생성하는 함수를 정의했습니다.

> **참고:** [강좌 뒷부분](/ko/docs/Learn/JavaScript/Building_blocks/Functions)에서 함수에 대해 자세히 알아볼 것입니다.

### 연산자

자바스크립트 연산자를 사용하면 테스트를 수행하고, 연산을 수행하고, 문자열을 결합하는 등의 작업을 수행할 수 있습니다.

아직 코드를 저장하지 않았다면 코드를 저장하고 브라우저에서 페이지를 새로고침한 다음 [개발자 도구 JavaScript 콘솔](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools)을 엽니다. 그런 다음 아래에 표시된 예제를 입력해 볼 수 있습니다. "예제" 열에 표시된 대로 각 예제를 정확히 입력하고 각 예제 뒤에 <kbd>Return</kbd>/<kbd>Enter</kbd>를 누른 다음 어떤 결과가 반환되는지 확인합니다.

먼저 산술 연산자를 예로 들어 보겠습니다:

| Operator | Name           | Example   |
| -------- | -------------- | --------- |
| `+`      | Addition       | `6 + 9`   |
| `-`      | Subtraction    | `20 - 15` |
| `*`      | Multiplication | `3 * 7`   |
| `/`      | Division       | `10 / 5`  |

`+` 연산자를 사용하여 텍스트 문자열을 서로 연결할 수도 있습니다(프로그래밍에서는 이를 연결이라고 합니다). 다음 줄을 한 번에 하나씩 입력해 보세요:

```js
const name = 'Bingo';
name;
const hello = ' says hello!';
hello;
const greeting = name + hello;
greeting;
```

[assignment operators](/ko/docs/Web/JavaScript/Reference/Operators#assignment_operators)라고 하는 바로가기 연산자도 사용할 수 있습니다. 예를 들어 기존 문자열에 새 텍스트 문자열을 추가하고 결과를 반환하려는 경우 이렇게 할 수 있습니다:

```js
let name1 = 'Bingo';
name1 += ' says hello!';
```

이것은 다음과 같습니다.

```js
let name2 = 'Bingo';
name2 = name2 + ' says hello!';
```

참/거짓 테스트를 실행할 때(예: 조건부 내부 - [아래](#conditionals) 참조) [비교 연산자](/ko/docs/Web/JavaScript/Reference/Operators)를 사용합니다. 예를 들어

<table class="standard-table">
  <thead>
    <tr>
      <th scope="col">Operator</th>
      <th scope="col">Name</th>
      <th scope="col">Example</th>
    </tr>
    <tr>
      <td><code>===</code></td>
      <td>Strict equality (is it exactly the same?)</td>
      <td>
        <pre class="brush: js">
5 === 2 + 4 // false
'Chris' === 'Bob' // false
5 === 2 + 3 // true
2 === '2' // false; number versus string
</pre
        >
      </td>
    </tr>
    <tr>
      <td><code>!==</code></td>
      <td>Non-equality (is it not the same?)</td>
      <td>
        <pre class="brush: js">
5 !== 2 + 4 // true
'Chris' !== 'Bob' // true
5 !== 2 + 3 // false
2 !== '2' // true; number versus string
</pre
        >
      </td>
    </tr>
    <tr>
      <td><code>&#x3C;</code></td>
      <td>Less than</td>
      <td>
        <pre class="brush: js">
6 &#x3C; 10 // true
20 &#x3C; 10 // false</pre
        >
      </td>
    </tr>
    <tr>
      <td><code>></code></td>
      <td>Greater than</td>
      <td>
        <pre class="brush: js">
6 > 10 // false
20 > 10 // true</pre
        >
      </td>
    </tr>
  </thead>
</table>

### 조건부

`checkGuess()` 함수로 돌아가서, 플레이스홀더 메시지를 그냥 뱉어내는 함수는 원하지 않는다고 해도 무방할 것 같습니다. 플레이어의 추측이 맞는지 아닌지 확인하고 적절하게 응답하기를 원합니다.

이 시점에서 현재 `checkGuess()` 함수를 이 버전으로 대체하세요:

```js
function checkGuess() {
  const userGuess = Number(guessField.value);
  if (guessCount === 1) {
    guesses.textContent = 'Previous guesses: ';
  }
  guesses.textContent += `${userGuess} `;

  if (userGuess === randomNumber) {
    lastResult.textContent = 'Congratulations! You got it right!';
    lastResult.style.backgroundColor = 'green';
    lowOrHi.textContent = '';
    setGameOver();
  } else if (guessCount === 10) {
    lastResult.textContent = '!!!GAME OVER!!!';
    lowOrHi.textContent = '';
    setGameOver();
  } else {
    lastResult.textContent = 'Wrong!';
    lastResult.style.backgroundColor = 'red';
    if (userGuess < randomNumber) {
      lowOrHi.textContent = 'Last guess was too low!';
    } else if (userGuess > randomNumber) {
      lowOrHi.textContent = 'Last guess was too high!';
    }
  }

  guessCount++;
  guessField.value = '';
  guessField.focus();
}
```

코드가 많네요 - 휴! 각 섹션을 살펴보고 각 섹션이 무엇을 하는지 설명해 보겠습니다.

- 첫 번째 줄은 `userGuess`이라는 변수를 선언하고 그 값을 텍스트 필드에 입력한 현재 값으로 설정합니다. 또한 값이 확실히 숫자인지 확인하기 위해 내장된 `Number()` 생성자를 통해 이 값을 실행합니다. 이 변수는 변경하지 않으므로 `const`를 사용해 선언하겠습니다.
- 다음으로 첫 번째 조건부 코드 블록을 만나게 됩니다. 조건부 코드 블록을 사용하면 특정 조건이 참인지 아닌지에 따라 코드를 선택적으로 실행할 수 있습니다. 함수처럼 보이지만 함수는 아닙니다. 가장 간단한 형태의 조건부 블록은 `if`라는 키워드로 시작하여 괄호, 중괄호, 중괄호로 구성됩니다. 괄호 안에는 테스트가 포함됩니다. 테스트가 `true`을 반환하면 중괄호 안에 있는 코드를 실행합니다. 그렇지 않으면 실행하지 않고 다음 코드로 넘어갑니다. 이 경우 테스트는 `guessCount` 변수가 `1`과 같은지(즉, 플레이어의 첫 번째 게임인지 아닌지) 테스트합니다:

  ```js
  guessCount === 1
  ```

  일치하면 추측 단락의 텍스트 콘텐츠를 `Previous guesses:`과 동일하게 만듭니다. 그렇지 않으면 그러지 않습니다.

- 6행은 `guesses` 단락의 끝에 현재 `userGuess` 값을 추가하고 빈 공간을 추가하여 표시되는 각 추측 사이에 공백이 생기도록 합니다.
- 다음 블록은 몇 가지 검사를 수행합니다:

  - 첫 번째 `if (){ }`는 사용자의 추측이 자바스크립트 상단에 설정된 `randomNumber`와 같은지 여부를 확인합니다. 일치하면 플레이어가 올바르게 추측했고 게임에 승리한 것이므로 플레이어에게 멋진 녹색으로 축하 메시지를 표시하고 낮음/높음 추측 정보 상자의 내용을 지운 다음 나중에 설명할 `setGameOver()`라는 함수를 실행합니다.
  - 이제 `else if (){ }` 구조를 사용하여 마지막 테스트의 끝에 다른 테스트를 연결했습니다. 이 테스트는 이번 턴이 사용자의 마지막 턴인지 여부를 확인합니다. 만약 그렇다면 프로그램은 이전 블록에서와 동일한 작업을 수행하지만 축하 메시지 대신 게임 오버 메시지를 표시합니다.
  - 이 코드 끝에 연결된 마지막 블록`else { }`)에는 다른 두 테스트 중 어느 것도 참을 반환하지 않는 경우에만 실행되는 코드가 포함되어 있습니다(즉, 플레이어가 맞히지 못했지만 남은 추측이 더 있는 경우). 이 경우 플레이어에게 틀렸다고 말한 다음 다른 조건부 테스트를 수행하여 추측이 정답보다 높았는지 낮았는지 확인하고, 더 높거나 낮은 경우 적절한 추가 메시지를 표시합니다.

- 함수의 마지막 세 줄(위의 26~28줄)은 다음 추측을 제출할 수 있도록 준비합니다. `guessCount` 변수에 1을 추가하여 플레이어가 자신의 차례를 다 사용하도록 하고(`++`는 증분 연산으로 1씩 증가), 양식 텍스트 필드에서 값을 비우고 다시 초점을 맞춰 다음 추측을 입력할 수 있도록 준비합니다.

### Events

이 시점에서는 멋지게 구현된 `checkGuess()` 함수가 있지만 아직 호출하지 않았기 때문에 아무 일도 하지 않습니다. 이상적으로는 "Submit guess" 버튼을 눌렀을 때 함수를 호출하고 싶지만, 이를 위해서는 **이벤트**를 사용해야 합니다. 이벤트는 버튼 클릭, 페이지 로딩, 동영상 재생 등 브라우저에서 일어나는 일로, 이에 대한 응답으로 코드 블록을 실행할 수 있습니다. **이벤트 리스너**는 특정 이벤트를 관찰하고 이벤트 발생에 대한 응답으로 실행되는 코드 블록인 **이벤트 핸들러**를 호출합니다.

`checkGuess()` 함수 아래에 다음 줄을 추가합니다:

```js
guessSubmit.addEventListener('click', checkGuess);
```

여기서는 `guessSubmit` 버튼에 이벤트 리스너를 추가하고 있습니다. 이 메서드는 두 개의 입력 값(인자라고 함)을 받는데, 이 값은 문자열로 수신 중인 이벤트 유형(이 경우 클릭)과 이벤트가 발생할 때 실행할 코드(이 경우 `checkGuess()` 함수)를 받습니다. {{domxref("EventTarget.addEventListener", "addEventListener()")}} 안에 작성할 때 괄호를 지정할 필요가 없다는 점에 유의하세요.

이제 코드를 저장하고 새로고침하면 예제가 어느 정도 작동할 것입니다. 이제 유일한 문제는 정답을 추측하거나 추측이 부족할 경우 게임이 종료된 후 실행되어야 하는 `setGameOver()` 함수를 아직 정의하지 않았기 때문에 게임이 중단된다는 것입니다. 이제 누락된 코드를 추가하여 예제 기능을 완성해 보겠습니다.

### 게임 기능 완성하기

코드 하단에 `setGameOver()` 함수를 추가한 다음 살펴봅시다. 이제 나머지 자바스크립트 아래에 추가하세요:

```js
function setGameOver() {
  guessField.disabled = true;
  guessSubmit.disabled = true;
  resetButton = document.createElement('button');
  resetButton.textContent = 'Start new game';
  document.body.append(resetButton);
  resetButton.addEventListener('click', resetGame);
}
```

- 처음 두 줄은 비활성화 속성을 `true`로 설정하여 폼 텍스트 입력과 버튼을 비활성화합니다. 그렇지 않으면 게임이 끝난 후 사용자가 더 많은 추측을 제출할 수 있고, 그러면 상황이 엉망이 될 수 있기 때문에 이 작업이 필요합니다.
- 다음 세 줄은 새 {{htmlelement("button")}} 요소를 생성하고 텍스트 레이블을 "Start new game" 으로 설정한 다음 기존 HTML의 맨 아래에 추가합니다.
- 마지막 줄은 새 버튼에 이벤트 리스너를 설정하여 버튼이 클릭될 때 `resetGame()`이라는 함수가 실행되도록 합니다.

이제 이 함수도 정의해야 합니다! 자바스크립트 하단에 다음 코드를 다시 추가합니다:

```js
function resetGame() {
  guessCount = 1;

  const resetParas = document.querySelectorAll('.resultParas p');
  for (const resetPara of resetParas) {
    resetPara.textContent = '';
  }

  resetButton.parentNode.removeChild(resetButton);

  guessField.disabled = false;
  guessSubmit.disabled = false;
  guessField.value = '';
  guessField.focus();

  lastResult.style.backgroundColor = 'white';

  randomNumber = Math.floor(Math.random() * 100) + 1;
}
```

이 다소 긴 코드 블록은 모든 것을 게임 시작 시점으로 완전히 초기화하여 플레이어가 다시 시도할 수 있도록 합니다. 이는:

- `guessCount`를 1로 되돌립니다.
- 정보 단락에서 모든 텍스트를 비웁니다.  `<div class="resultParas"></div>` 내의 모든 단락을 선택한 다음 각 단락을 반복하여 `textContent`를 `''`(빈 문자열)로 설정합니다.
- 코드에서 reset 버튼을 제거합니다
- 양식 요소를 활성화하고 텍스트 필드를 비우고 초점을 맞춰 새로운 추측을 입력할 수 있도록 준비합니다.
- `lastResult` 단락에서 배경색을 제거합니다.
- 같은 숫자를 다시 추측하지 않도록 새로운 난수를 생성합니다!

**이 시점에서 완전히 작동하는 (간단한) 게임이 생겼습니다 - 축하합니다!**

이제 이 글에서 남은 것은 여러분이 미처 깨닫지 못했을 수도 있지만 이미 보셨던 몇 가지 중요한 코드 기능에 대해 이야기하는 것뿐입니다.

### 루프

위 코드에서 좀 더 자세히 살펴봐야 할 부분은 [for...of](/ko/docs/Web/JavaScript/Reference/Statements/for...of) 루프입니다. 루프는 프로그래밍에서 매우 중요한 개념으로, 특정 조건이 충족될 때까지 코드를 계속 반복해서 실행할 수 있게 해줍니다.

먼저 [브라우저 개발자 도구 JavaScript 콘솔](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools)로 다시 이동하여 다음을 입력합니다:

```js
const fruits = ['apples', 'bananas', 'cherries'];
for (const fruit of fruits) {
  console.log(fruit);
}
```

무슨 일이 일어났을까요? 콘솔에 `'apples', 'bananas', 'cherries'` 문자열이 출력되었습니다.

이는 루프 때문입니다. `const fruits = ['apples', 'bananas', 'cherries'];` 줄은 배열을 만듭니다. 이 모듈의 뒷부분에서 [배열에 대한 전체 가이드](/ko/docs/Learn/JavaScript/First_steps/Arrays)를 살펴보겠지만, 지금은 배열은 항목(이 경우 문자열)의 모음입니다.

`for...of` 루프는 배열의 각 항목을 가져와서 자바스크립트를 실행할 수 있는 방법을 제공합니다.`for (const fruit of fruits)` 줄은 다음과 같습니다:

1. `fruits`의 첫 번째 항목을 가져옵니다.
2. `fruit` 변수를 해당 항목으로 설정한 다음 `{}` 괄호 사이의 코드를 실행합니다.
3. `fruits`의 다음 항목을 가져오고 `fruits`의 끝에 도달할 때까지 2번을 반복합니다.

이 경우 괄호 안의 코드가 콘솔에 `fruit`을 출력합니다.

이제 숫자 맞추기 게임의 루프를 살펴보겠습니다. 다음은 `resetGame()` 함수 내부에서 찾을 수 있습니다:

```js
const resetParas = document.querySelectorAll('.resultParas p');
for (const resetPara of resetParas) {
  resetPara.textContent = '';
}
```

이 코드는 {{domxref("Document.querySelectorAll", "querySelectorAll()")}} 메서드를 사용하여 `<div class="resultParas">` 내의 모든 단락 목록이 포함된 변수를 생성한 다음 각 단락을 반복하여 각 단락의 텍스트 콘텐츠를 제거합니다.

`resetPara`가 상수이긴 하지만 `textContent`와 같은 내부 속성을 변경할 수 있다는 점에 유의하세요.

### 객체에 대한 간단한 논의

이 논의에 들어가기 전에 마지막으로 개선 사항을 하나 더 추가하겠습니다. 자바스크립트 상단의 `let resetButton;` 줄 바로 아래에 다음 줄을 추가한 다음 파일을 저장합니다:

```js
guessField.focus();
```

이 줄은 {{domxref("HTMLElement/focus", "focus()")}} 메서드를 사용하여 페이지가 로드되는 즉시 텍스트 커서를 {{htmlelement("input")}} 텍스트 필드에 자동으로 배치하므로 사용자가 양식 필드를 먼저 클릭할 필요 없이 바로 첫 번째 추측을 입력할 수 있습니다. 사소한 추가 기능이지만 사용성을 개선하여 사용자에게 게임을 플레이하기 위해 무엇을 해야 하는지 시각적으로 알려줍니다.

여기서 무슨 일이 일어나고 있는지 좀 더 자세히 분석해 보겠습니다. 자바스크립트에서 코드에서 조작하는 대부분의 항목은 객체입니다. 객체는 단일 그룹에 저장된 관련 기능의 모음입니다. 객체를 직접 생성할 수도 있지만 이는 상당히 고급이므로 강좌의 후반부에서 다루지 않을 것입니다. 지금은 브라우저에 포함된 기본 제공 객체를 통해 여러 가지 유용한 작업을 수행할 수 있는 방법에 대해서만 간략하게 설명하겠습니다.

이 특별한 경우, 먼저 HTML에 텍스트 입력 양식 필드에 대한 참조를 저장하는 `guessField` 상수를 만들었습니다. 코드 상단 근처의 선언에서 다음 줄을 찾을 수 있습니다:

```js
const guessField = document.querySelector('.guessField');
```

이 참조를 얻기 위해 {{domxref("document")}} 객체의 {{domxref("document.querySelector", "querySelector()")}} 메서드를 사용했습니다. `querySelector()`는 참조를 원하는 요소를 선택하는 [CSS 선택자](/ko/docs/Learn/CSS/Building_blocks/Selectors)라는 한 가지 정보를 받습니다.

이제 `guessField`에 {{htmlelement("input")}} 요소에 대한 참조가 포함되어 있으므로 여러 속성(기본적으로 객체 내부에 저장된 변수, 일부는 값을 변경할 수 없음)과 메서드(기본적으로 객체 내부에 저장된 함수)에 액세스할 수 있습니다. 입력 요소에 사용할 수 있는 메서드 중 하나는 `focus()`이므로 이제 이 줄을 사용하여 텍스트 입력에 초점을 맞출 수 있습니다:

```js
guessField.focus();
```

양식 요소에 대한 참조가 포함되지 않은 변수는 `focus()`를 사용할 수 없습니다. 예를 들어 `guesses` 상수에는 {{htmlelement("p")}} 요소에 대한 참조가 포함되어 있고 `guessCount` 변수에는 숫자가 포함되어 있습니다.

### 브라우저 객체 가지고 놀기

몇 가지 브라우저 객체를 가지고 놀아 보겠습니다.

1. 먼저 브라우저에서 프로그램을 엽니다
2. 그런 다음 [브라우저 개발자 도구](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools)를 열고 자바스크립트 콘솔 탭이 열려 있는지 확인합니다.
3. 콘솔에 `guessField`를 입력하면 변수에 {{htmlelement("input")}} 요소가 포함되어 있음을 콘솔에 표시합니다. 또한 변수를 포함하여 실행 환경 내에 존재하는 객체의 이름이 콘솔에 자동 완성되는 것을 확인할 수 있습니다!
4. 이제 다음을 입력합니다:

   ```js
   guessField.value = 2;
   ```

   `value` 속성은 텍스트 필드에 입력된 현재 값을 나타냅니다. 이 명령을 입력하면 텍스트 필드의 텍스트가 변경된 것을 볼 수 있습니다!

5. 이제 콘솔에 `guesses`을 입력하고 Return 키를 눌러 보세요. 콘솔에 변수에 {{htmlelement("p")}} 요소가 포함되어 있음을 알 수 있습니다.
6. 이제 다음 줄을 입력해 보세요:

   ```js
   guesses.value
   ```

   단락에 `value` 속성이 없기 때문에 브라우저가 `undefined`를 반환됩니다.

7. 단락 내부의 텍스트를 변경하려면 대신 {{domxref("Node.textContent", "textContent")}} 속성이 필요합니다. 이렇게 해 보세요:

   ```js
   guesses.textContent = 'Where is my paragraph?';
   ```

8. 이제 재미있는 게임을 해보겠습니다. 아래 줄을 하나씩 입력해 보세요:

   ```js
   guesses.style.backgroundColor = 'yellow';
   guesses.style.fontSize = '200%';
   guesses.style.padding = '10px';
   guesses.style.boxShadow = '3px 3px 6px black';
   ```

   페이지의 모든 요소에는 `style` 프로퍼티가 있으며, 이 프로퍼티에는 해당 요소에 적용된 모든 인라인 CSS 스타일이 포함된 객체가 포함되어 있습니다. 이를 통해 JavaScript를 사용하여 요소에 새로운 CSS 스타일을 동적으로 설정할 수 있습니다.

## 여기까지...

예제 빌드는 여기까지입니다. 끝까지 해내셨습니다! 최종 코드를 사용해 보거나 [여기에서 완성된 버전을 사용](https://mdn.github.io/learning-area/javascript/introduction-to-js-1/first-splash/number-guessing-game.html)해 보세요. 예제가 작동하지 않는다면 [소스 코드](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/first-splash/number-guessing-game.html)와 비교해 보세요.

{{PreviousMenuNext("Learn/JavaScript/First_steps/What_is_JavaScript", "Learn/JavaScript/First_steps/What_went_wrong", "Learn/JavaScript/First_steps")}}
