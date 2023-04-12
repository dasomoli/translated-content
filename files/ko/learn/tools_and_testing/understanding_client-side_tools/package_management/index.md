---
title: Package management basics
slug: Learn/Tools_and_testing/Understanding_client-side_tools/Package_management
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Tools_and_testing/Understanding_client-side_tools/Command_line","Learn/Tools_and_testing/Understanding_client-side_tools/Introducing_complete_toolchain", "Learn/Tools_and_testing/Understanding_client-side_tools")}}

이 글에서는 패키지 관리자를 자세히 살펴보고 프로젝트 도구 종속성을 설치하고 최신 상태로 유지하는 등 프로젝트에서 패키지 관리자를 어떻게 사용할 수 있는지 알아보세요.

<table>
  <tbody>
    <tr>
      <th scope="row">전제 조건:</th>
      <td>
        핵심 <a href="/ko/docs/Learn/HTML">HTML</a>,
        <a href="/ko/docs/Learn/CSS">CSS</a>,
        <a href="/ko/docs/Learn/JavaScript">JavaScript</a> 언어에 익숙해야 합니다.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        패키지 관리자와 패키지 저장소가 무엇인지, 왜 필요한지, 어떻게 사용하는지 기본 사항을 이해합니다.
      </td>
    </tr>
  </tbody>
</table>

## 프로젝트의 종속성

**종속성** 이란 다른 사람이 작성한 타사 소프트웨어로, 하나의 문제를 해결하는 것이 이상적입니다. 웹 프로젝트에는 종속성이 없는 것부터 많은 것까지 다양한 종속성이 있을 수 있으며, 종속성에는 명시적으로 설치하지 않은 하위 종속성이 포함될 수 있으며, 종속성에는 자체 종속성이 있을 수 있습니다.

프로젝트에 필요할 수 있는 유용한 종속성의 간단한 예로는 상대 날짜를 사람이 읽을 수 있는 텍스트로 계산하는 코드가 있습니다. 물론 직접 코딩할 수도 있지만, 다른 사람이 이미 이 문제를 해결했을 가능성이 높으므로 같은 일을 반복하는 데 시간을 낭비할 이유가 없습니다. 게다가 신뢰할 수 있는 타사 종속성은 다양한 상황에서 테스트를 거쳤을 가능성이 높으므로 자체 솔루션보다 더 강력하고 브라우저 간 호환성이 뛰어납니다.

프로젝트 종속 요소는 React나 Vue와 같은 전체 JavaScript 라이브러리 또는 프레임워크일 수도 있고, 사람이 읽을 수 있는 날짜 라이브러리와 같은 아주 작은 유틸리티일 수도 있으며, 이전 글에서 소개한 Prettier나 ESLint와 같은 명령줄 도구일 수도 있습니다.

최신 빌드 도구가 없다면 이와 같은 종속성을 간단한 [`<script>`](/ko/docs/Web/HTML/Element/script) 요소를 사용하여 프로젝트에 포함할 수 있지만, 이 방법은 즉시 작동하지 않을 수 있으며 웹에 배포할 때 코드와 종속성을 함께 번들로 묶으려면 최신 도구가 필요할 수 있습니다. 번들은 일반적으로 소프트웨어의 모든 JavaScript를 포함하는 웹 서버의 단일 파일을 지칭하는 용어로, 일반적으로 소프트웨어를 다운로드하고 방문자의 브라우저에 표시하는 데 걸리는 시간을 줄이기 위해 최대한 압축하여 사용합니다.

또한 현재 도구 대신 사용하고 싶은 더 나은 도구를 찾거나 업데이트하고 싶은 종속 요소의 새 버전이 출시되면 어떻게 될까요? 몇 개의 종속 요소만 있으면 큰 문제가 되지 않지만, 종속 요소가 많은 대규모 프로젝트에서는 이런 일이 발생하면 추적하기가 정말 어려워질 수 있습니다. npm과 같은 **패키지 관리자** 를 사용하면 코드를 깔끔하게 추가 및 제거할 수 있을 뿐만 아니라 다른 여러 가지 이점도 얻을 수 있으므로 더 좋습니다.

## 패키지 관리자란 정확히 무엇인가요?

이미 [npm](https://www.npmjs.com/) 에 대해 알아봤지만, npm 자체에서 한 발짝 물러나서 패키지 관리자는 프로젝트 종속성을 관리하는 시스템입니다.

패키지 관리자는 새로운 종속성("패키지"라고도 함)을 설치하고, 파일 시스템에서 패키지가 저장되는 위치를 관리하며, 사용자가 직접 패키지를 게시할 수 있는 기능을 제공합니다.

이론적으로는 패키지 관리자가 필요하지 않을 수도 있고 프로젝트 종속 요소를 수동으로 다운로드하여 저장할 수도 있지만, 패키지 관리자는 패키지 설치 및 제거를 원활하게 처리합니다. 패키지 관리자를 사용하지 않는다면 수동으로 처리해야 합니다:

- 올바른 패키지 JavaScript 파일을 모두 찾습니다.
- 알려진 취약점이 없는지 확인합니다.
- 파일을 다운로드하여 프로젝트의 올바른 위치에 배치합니다.
- 애플리케이션에 패키지를 포함하도록 코드를 작성합니다(이 작업은 [자바스크립트 모듈](/ko/docs/Web/JavaScript/Guide/Modules) 을 사용하여 수행하는 경향이 있는데, 이 주제에 대해 자세히 알아보고 이해할 필요가 있습니다).
- 수십 개 또는 수백 개에 달하는 패키지의 모든 하위 종속성에 대해 동일한 작업을 수행합니다.
- 패키지를 제거하려면 모든 파일을 다시 제거합니다.

또한 패키지 관리자는 중복 종속성(프론트엔드 개발에서 중요하고 일반적인 문제)을 처리합니다.

npm(및 자바스크립트 및 노드 기반 패키지 관리자)의 경우 종속성을 설치하는 위치에 두 가지 옵션이 있습니다. 이전 글에서 살펴본 것처럼 종속 요소는 프로젝트에 전역적으로 또는 로컬로 설치할 수 있습니다. 글로벌 설치의 장점이 더 많은 경향이 있지만 로컬 설치의 장점은 코드 이식성 및 버전 잠금과 같은 더 중요한 것입니다.

예를 들어 프로젝트가 특정 구성의 Webpack에 의존하는 경우 다른 컴퓨터에 해당 프로젝트를 설치하거나 나중에 다시 돌아와도 해당 구성이 계속 작동하는지 확인하고 싶을 것입니다. 다른 버전의 Webpack을 설치한 경우 호환되지 않을 수 있습니다. 이 문제를 완화하기 위해 종속성은 프로젝트에 로컬로 설치됩니다.

로컬 종속성이 실제로 빛을 발하는지 확인하려면 기존 프로젝트를 다운로드하여 실행해 보기만 하면 됩니다. 프로젝트가 작동하고 모든 종속성이 즉시 작동한다면 코드가 이식 가능하다는 사실에 감사할 로컬 종속성이 있는 것입니다.

> **참고:** npm만이 유일한 패키지 관리자는 아닙니다. 성공적이고 인기 있는 대체 패키지 관리자로는 [Yarn](https://yarnpkg.com/) 이 있습니다. Yarn은 다른 알고리즘을 사용하여 종속성을 해결하므로 사용자 경험이 더 빨라질 수 있습니다. 이 외에도 [pnpm](https://pnpm.js.org/) 과 같은 여러 가지 새로운 클라이언트도 있습니다.

## 패키지 레지스트리

패키지 관리자가 작동하려면 패키지를 설치할 위치를 알아야 하며, 이는 패키지 레지스트리의 형태로 제공됩니다. 레지스트리는 패키지가 게시되어 설치될 수 있는 중앙 위치입니다. npm은 패키지 관리자이기도 하지만 JavaScript 패키지에 가장 일반적으로 사용되는 패키지 레지스트리의 이름이기도 합니다. npm 레지스트리는 [npmjs.com](https://www.npmjs.com/) 에 존재합니다.

npm이 유일한 옵션은 아닙니다. 자체 패키지 레지스트리를 관리할 수도 있습니다. [Microsoft Azure](https://azure.microsoft.com/) 와 같은 제품에서는 npm 레지스트리에 대한 프록시를 생성할 수 있으며(특정 패키지를 재정의하거나 잠글 수 있음), [GitHub에서도 패키지 레지스트리 서비스를 제공](https://github.com/features/packages) 하며, 시간이 지남에 따라 더 많은 옵션이 등장할 가능성이 높습니다.

중요한 것은 자신에게 가장 적합한 레지스트리를 선택했는지 확인하는 것입니다. 많은 프로젝트가 npm을 사용하며, 이 모듈의 나머지 부분에서는 예제에서 이를 고수할 것입니다.

## 패키지 에코시스템 사용하기

패키지 관리자와 레지스트리를 사용하여 명령줄 유틸리티를 설치하는 예제를 통해 시작해보겠습니다.

[Parcel](https://parceljs.org/) 은 개발자가 개발 과정에서 흔히 사용하는 또 다른 도구입니다. Parcel은 코드에서 종속성에 대한 호출을 감시하고 코드에 필요하다고 판단되는 종속성을 자동으로 설치한다는 점에서 똑똑합니다. 또한 코드를 자동으로 빌드할 수도 있습니다.

### 앱을 npm 패키지로 설정하기

먼저 실험용 앱을 저장할 새 디렉터리를 다시 찾을 수 있는 적당한 곳에 만듭니다. 이 디렉터리를 parcel-experiment라고 부르겠지만 원하는 대로 불러도 됩니다:

```bash
mkdir parcel-experiment
cd parcel-experiment
```

다음으로, 앱을 npm 패키지로 초기화하여 나중에 이 환경을 다시 만들거나 npm 레지스트리에 패키지를 게시할 경우를 대비하여 구성 세부 정보를 저장할 수 있는 구성 파일(`package.json`)을 생성해 보겠습니다(이 글의 범위를 다소 벗어나는 부분이지만).

다음 명령을 입력하여 `parcel-experiment` 디렉터리 안에 있는지 확인합니다:

```bash
npm init
```

이제 몇 가지 질문이 표시되며, npm은 답변에 따라 기본 `package.json` 파일을 생성합니다:

- `name`: 앱을 식별할 이름입니다.

  <kbd>Return</kbd>

  을 누르면 기본 `parcel-experiment` 실험을 수락합니다.

- `version`: 앱의 시작 버전 번호입니다. `기본 1.0.0`을 수락하려면 다시

  <kbd>Return</kbd>

  키를 누르기만 하면 됩니다.

- `description`: 앱의 용도에 대한 간단한 설명입니다. 예를 들어 "npm 사용에 대해 배울 수 있는 간단한 npm 패키지"와 같이 아주 간단한 내용을 입력한 다음

  <kbd>Return</kbd>

  키를 누릅니다.

- `entry point`: 앱의 최상위 자바스크립트 파일이 됩니다. 현재로서는 기본 index.js를 사용해도 괜찮습니다.

  <kbd>Return</kbd>

  키를 누릅니다.

- `test command`, `git repository` 및 `keywords`: 현재로서는 각각을 비워두려면

  <kbd>Return</kbd>

  키를 누릅니다.

- `author`: 프로젝트의 작성자. 자신의 이름을 입력하고

  <kbd>Return</kbd>

  키를 누릅니다.

- `license`: 패키지를 게시할 라이선스입니다. 현재 기본값을 수락하려면

  <kbd>Return</kbd>

  키를 누릅니다.

이 설정을 수락하려면 <kbd>Return</kbd> 키를 한 번 더 누릅니다.

`parcel-experiment` 디렉토리로 이동하면 이제 package.json 파일이 있습니다. 파일을 열면 다음과 같이 보일 것입니다:

```json
{
  "name": "parcel-experiment",
  "version": "1.0.0",
  "description": "A simple npm package to learn about using npm",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Chris Mills",
  "license": "ISC"
}
```

이것이 패키지를 정의하는 구성 파일입니다. 지금은 이 정도면 충분하니 계속 진행하겠습니다.

### Parcel 설치하기

다음 명령을 실행하여 로컬에 Parcel을 설치합니다:

```bash
npm install parcel-bundler
```

모든 작업이 완료되면 이제 "최신 클라이언트 측 개발"(빌드 도구를 사용하여 개발자 경험을 조금 더 쉽게 만드는 것을 의미)을 할 준비가 되었습니다. 하지만 먼저 package.json 파일을 다시 한 번 살펴보세요. npm이 의존성이라는 새로운 필드를 추가한 것을 볼 수 있습니다:

```json
"dependencies": {
  "parcel-bundler": "^1.12.4"
}
```

나중에 코드베이스를 다른 위치, 다른 컴퓨터로 옮길 경우 `npm install` 명령을 실행하여 동일한 설정을 다시 만들 수 있으며, npm이 종속성을 확인하고 설치해 줍니다.

한 가지 단점은 Parcel은 `parcel-experiment` 앱 내에서만 사용할 수 있으며 다른 디렉토리에서 실행할 수 없다는 것입니다. 하지만 장점은 단점보다 훨씬 큽니다.

### 예제 앱 설정하기

이제 설정을 시작하겠습니다.

Parcel은 `index.html`과 `index.js` 파일을 사용할 것으로 예상하지만, 그 외에는 프로젝트를 어떻게 구성하는지에 대해 매우 자유롭습니다. 다른 도구는 매우 다를 수 있지만, 적어도 Parcel은 초기 실험을 쉽게 해줍니다.

이제 작업 디렉터리에 `index.html` 파일을 추가해야 합니다. 테스트 디렉토리에 `index.html`을 생성하고 다음과 같은 내용을 추가합니다:

```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title>My test page</title>
  </head>
  <body>
    <script src="./index.js"></script>
  </body>
</html>
```

다음으로 `index.html`과 같은 디렉터리에 `index.js` 파일을 추가해야 합니다. 지금은 `index.js`를 비워도 되지만, 존재하기만 하면 됩니다. 지금 생성하세요

### Parcel 즐기기

이제 새로 설치한 Parcel 도구를 실행해 보겠습니다. 터미널에서 다음 명령을 실행합니다:

```bash
 parcel index.html
```

터미널에 다음과 같은 내용이 인쇄되어 있을 것입니다:

```bash
Server running at http://localhost:1234
✨  Built in 193ms.
```

> **참고:** 터미널에서 "명령을 찾을 수 없음" 유형 오류를 반환하는 데 문제가 있는 경우 `npx` 유틸리티를 사용하여 위의 명령을 실행해 보세요(예: `npx parcel index.html`).

이제 전체 JavaScript 패키지 에코시스템의 이점을 누릴 준비가 되었습니다. 우선 `http://localhost:1234` 에서 로컬 웹 서버가 실행 중입니다. 지금 바로 이곳으로 이동하면 지금은 아무것도 표시되지 않지만, 앱을 변경하면 Parcel이 앱을 다시 빌드하고 서버를 자동으로 새로 고쳐서 업데이트 효과를 즉시 확인할 수 있다는 점이 멋집니다.

이제 일부 페이지 콘텐츠를 살펴보겠습니다. "2시간 전", "4일 전" 등과 같이 사람이 읽을 수 있는 상대적인 날짜를 표시하고 싶다고 가정해 봅시다. [`date-fns`](https://date-fns.org/) 패키지의 `formatDistanceToNow()` 메서드가 유용합니다(같은 기능을 하는 다른 패키지도 있습니다).

`index.js` 파일에 다음 코드를 추가하고 저장합니다:

```js
import { formatDistanceToNow } from "date-fns";

const date = "1996-09-13 10:00:00";
document.body.textContent = `${formatDistanceToNow(new Date(date))} ago`;
```

`http://localhost:1234` 으로 돌아가면 작성자가 18세가 된 지 얼마나 되었는지 확인할 수 있습니다.

위 코드에서 특히 특별한 점은 우리가 설치하지 않은 `date-fns` 패키지의 `formatDistanceToNow()` 함수를 사용하고 있다는 점입니다! Parcel은 사용자가 이 모듈이 필요하다는 것을 알아차리고 `npmjs.com` 패키지 레지스트리에서 해당 모듈을 검색하여 자동으로 로컬에 설치해 주었습니다. `package.json` 파일을 다시 살펴보면 `dependencies` 필드가 업데이트된 것을 확인할 수 있습니다:

```json
"dependencies": {
  "date-fns": "^2.12.0",
  "parcel-bundler": "^1.12.4"
}
```

Parcel은 다른 사람이 이 프로젝트를 선택하고 우리가 사용한 모든 종속성을 설치하는 데 필요한 파일도 추가했습니다. `parcel` 명령을 실행한 디렉토리를 살펴보면 여러 개의 새로운 파일을 찾을 수 있는데, 그중 가장 흥미로운 파일은 다음과 같습니다:

- `node_modules`: Parcel과 date-fns의 의존성 파일.
- `dist`: 배포 디렉토리 - Parcel이 자동으로 패키징하고 축소한 파일과 `localhost:1234`에서 서비스하는 파일입니다. 사이트를 온라인에 공개할 때 웹 서버에 업로드하는 파일입니다.

패키지 이름만 알고 있으면 코드에서 해당 이름을 사용할 수 있으며, Parcel은 패키지를 가져와서 로컬 디렉토리(`node_modules` 아래)에 설치(실제로는 "복사")합니다.

### 프로덕션용 코드 빌드

하지만 이 코드는 아직 프로덕션에 사용할 준비가 되지 않았습니다. 대부분의 빌드 툴링 시스템에는 "개발 모드"와 "프로덕션 모드"가 있습니다. 중요한 차이점은 "핫 모듈 교체", "라이브 리로딩", "압축되지 않고 주석 처리된 소스 코드" 등 개발에서 사용할 유용한 기능 중 상당수가 최종 사이트에서는 필요하지 않으므로 프로덕션에서는 제거된다는 점입니다. 이러한 기능은 개발 단계에서는 매우 유용하지만 프로덕션에서는 그다지 유용하지 않은 일반적인 웹 개발 기능 중 일부입니다. 프로덕션 환경에서는 사이트를 부풀리기만 할 뿐입니다.

이제 <kbd>Ctrl</kbd> + <kbd>C</kbd>를 사용하여 이전 Parcel 명령을 중지합니다.

이제 가상의 배포를 위해 베어본 예제 사이트를 준비할 수 있습니다. Parcel은 게시에 적합한 파일을 생성하는 추가 명령을 제공하여 빌드 옵션으로 번들(앞서 언급한)을 만듭니다.

다음 명령을 실행합니다:

```bash
parcel build index.html
```

다음과 같은 출력이 표시됩니다:

```bash
✨  Built in 9.35s.

dist/my-project.fb76efcf.js.map    648.58 KB     64ms
dist/my-project.fb76efcf.js        195.74 KB    8.43s
dist/index.html                        288 B    806ms
```

다시 말하지만, 프로덕션 파일의 대상은 `dist` 디렉터리입니다.

### 앱의 파일 크기 줄이기

그러나 개발자를 "도와주는" 모든 도구가 그렇듯, 종종 장단점이 있습니다. 이 특별한 경우에는 파일 크기입니다. JavaScript 번들인 my-project.fb76efcf.js는 텍스트 한 줄을 인쇄하기만 한다는 점을 감안하면 무려 195K에 달해 매우 큽니다. 물론 계산이 필요하긴 하지만, 이 작업을 수행하기 위해 195K의 JavaScript가 필요한 것은 아닙니다!

개발 도구를 사용할 때는 해당 도구가 자신에게 적합한지 의심해 볼 필요가 있습니다. 이 경우 번들에는 우리가 사용 중인 함수뿐만 아니라 전체 `date-fns` 라이브러리가 포함되어 있기 때문에 거의 200K에 육박합니다.

개발 도구를 사용하지 않고 `<script src="">` 요소에 호스팅된 `date-fns` 버전을 가리켰다면 브라우저에서 예제 페이지가 로드될 때 라이브러리 전체가 다운로드되는 거의 동일한 상황이 발생했을 것입니다.

하지만 바로 이 지점에서 개발 도구가 빛을 발할 수 있습니다. 개발 툴을 사용하는 동안 소프트웨어에 코드 사용을 검사하고 실제로 프로덕션에서 사용하는 함수만 포함하도록 요청할 수 있는데, 이를 '트리 쉐이킹'이라고 합니다.

이는 파일 크기를 줄여 앱을 최대한 빠르게 로드하고자 할 때 매우 유용합니다. 다양한 툴을 사용하면 다양한 방식으로 트리 셰이킹을 수행할 수 있습니다.

매월 목록이 늘어나지만, 소스 코드에서 번들을 생성하는 도구는 크게 세 가지가 있습니다: Webpack, [Rollup](https://rollupjs.org/guide/en/), Parcel입니다. 이 외에도 더 많은 도구가 있지만, 이 세 가지가 인기 있는 도구입니다:

- 롤업 도구는 트리 쉐이킹과 코드 분할을 핵심 기능으로 제공합니다.
- 웹팩은 약간의 구성이 필요합니다(일부 개발자의 웹팩 구성이 복잡하다는 점을 감안하면 "약간"이라는 표현이 과소평가된 것일 수 있습니다).
- Parcel(Parcel 버전 2 이전)의 경우, 빌드하는 동안 트리 쉐이킹을 수행하는 특수 플래그인 `--experimental-scope-hoisting`이 필요합니다.

이미 설치되어 있으므로 지금은 Parcel을 계속 사용하겠습니다. 다음 명령을 실행해 보세요:

```bash
parcel build index.html --experimental-scope-hoisting
```

이것이 큰 차이를 만든다는 것을 알 수 있을 것입니다:

```bash
✨  Built in 7.87s.

dist/my-project.86f8a5fc.js    10.34 KB    7.17s
dist/index.html                   288 B    753ms
```

이제 번들은 약 10K입니다. 훨씬 낫네요.

이 프로젝트를 서버에 릴리스하려면 `dist` 폴더에 있는 파일만 릴리스해야 합니다. Parcel이 모든 파일 이름 변경을 자동으로 처리해 주었습니다. Parcel이 자동으로 어떤 변경을 수행했는지 보려면 `dist/index.html`의 소스 코드를 살펴보는 것이 좋습니다.

> **참고:** 이 글을 작성할 당시에는 Parcel 2가 출시되지 않았습니다. 그러나 Parcel 개발자가 도구 이름을 약간 다르게 지었기 때문에 출시되더라도 이러한 명령은 모두 계속 작동합니다. Parcel 1.x를 설치하려면 `parcel-bundler`를 설치해야 하지만, Parcel 2.x는 `parcel`이라고 합니다.

사용 가능한 도구가 많고 JavaScript 패키지 생태계는 전례 없는 속도로 성장하고 있으며 장단점이 있습니다. 항상 개선이 이루어지고 있으며, 좋든 나쁘든 선택의 폭은 계속 넓어지고 있습니다. 압도적인 도구 선택의 폭에 직면했을 때 가장 중요한 교훈은 선택한 도구가 무엇을 할 수 있는지 파악하는 것입니다.

## 패키지 관리자 클라이언트에 대한 대략적인 가이드

이 튜토리얼에서는 npm을 사용하여 Parcel 패키지를 설치했지만 앞서 언급했듯이 몇 가지 대안이 있습니다. 적어도 이러한 도구가 있다는 것을 알고 여러 도구에서 공통적으로 사용되는 명령어에 대해 어느 정도는 알고 있는 것이 좋습니다. 이미 몇 가지가 실제로 작동하는 것을 보셨겠지만, 다른 것들도 살펴봅시다.

시간이 지남에 따라 목록은 계속 늘어날 것이지만, 이 글을 쓰는 시점에서는 다음과 같은 주요 패키지 관리자를 사용할 수 있습니다:

- npm ([npmjs.org](https://www.npmjs.com/))
- pnpm ([pnpm.js.org](https://pnpm.js.org/))
- Yarn ([yarnpkg.com](https://yarnpkg.com/))

명령줄 관점에서 보면 npm과 pnpm은 비슷하지만, 실제로 pnpm은 npm이 제공하는 인수 옵션에 대해 완전한 동등성을 갖는 것을 목표로 합니다. 하지만 컴퓨터에 패키지를 다운로드하고 저장하는 데 다른 방법을 사용하여 필요한 전체 디스크 공간을 줄이는 것을 목표로 한다는 점에서 다릅니다.

아래 예제에서 npm이 표시된 곳에 pnpm을 대체할 수 있으며 명령이 작동합니다.

설치 프로세스 측면에서 Yarn이 npm보다 빠르다고 생각하는 경우가 많습니다(개인차가 있을 수 있지만). 종속 요소가 설치되고 컴퓨터에 복사될 때까지 기다리는 데 상당한 시간이 낭비될 수 있기 때문에 개발자에게는 이 점이 중요합니다.

> **참고:** npm 패키지 관리자는 이름이 같더라도 npm 레지스트리의 패키지를 설치할 **필요는 없습니다**. pnpm과 Yarn은 npm과 동일한 `package.json` 형식을 사용할 수 있으며 npm 및 기타 패키지 레지스트리의 모든 패키지를 설치할 수 있습니다.

패키지 관리자로 수행할 수 있는 일반적인 작업을 검토해 보겠습니다.

### 새 프로젝트 초기화

```bash
npm init
yarn init
```

위와 같이 프로젝트에 대한 설명(이름, 라이선스, 설명 등)을 위한 일련의 질문을 표시하고 안내한 다음 프로젝트 및 해당 종속성에 대한 메타 정보가 포함된 `package.json`을 생성합니다.

### 종속성 설치

```bash
npm install date-fns
yarn add date-fns
```

위에서 실제로 `설치`하는 모습도 보았습니다. 이렇게 하면 `date-fns` 패키지가 `date-fns`의 자체 종속 요소와 함께 `node_modules`라는 하위 디렉터리에 있는 작업 디렉터리에 직접 추가됩니다.

기본적으로 이 명령은 최신 버전의 `date-fns`를 설치하지만 이 역시 사용자가 제어할 수 있습니다. `date-fns@1`을 요청하면 최신 1.x 버전(1.30.1)을 받을 수 있습니다. 또는 2.3.0(이 글을 쓰는 시점에 2.8.1)을 포함한 최신 버전을 의미하는 `date-fns@^2.3.0`을 사용해 볼 수도 있습니다.

### 종속성 업데이트

```bash
npm update
yarn upgrade
```

현재 설치된 종속성을 살펴보고 사용 가능한 업데이트가 있는 경우 패키지에 지정된 범위 내에서 업데이트합니다.

범위는 `package.json`의 종속성 버전에 지정됩니다(예: `date-fns@^2.0.1`). 이 경우 캐럿 문자 `^`는 3.0.0을 제외한 2.0.1 이후의 모든 마이너 및 패치 릴리스를 의미합니다.

이는 [semver](https://semver.org/) 라는 시스템을 사용하여 결정되는데, 문서에서는 다소 복잡해 보일 수 있지만 요약 정보만 고려하고 버전이 `MAJOR.MINOR.PATCH`로 표시된다는 점(예: 2.0.1은 메이저 버전 2, 패치 버전 1)을 고려하면 단순화할 수 있습니다. semver 값을 사용해 보는 가장 좋은 방법은 [semver 계산기](https://semver.npmjs.com/) 를 사용하는 것입니다.

`npm update`는 `package.json`에 정의된 범위 이상으로 종속성을 업그레이드하지 않으며, 이를 위해서는 해당 버전을 직접 설치해야 한다는 점을 기억하는 것이 중요합니다.

### 취약점 감사

```bash
npm audit
yarn audit
```

프로젝트의 모든 종속성 트리를 확인하고 취약성 데이터베이스에 대해 사용 중인 특정 버전을 실행하여 프로젝트에 잠재적으로 취약한 패키지가 있는지 알려줍니다.

취약점에 대해 배우기 위한 좋은 출발점은 JavaScript 패키지와 다른 프로그래밍 언어를 모두 다루는 [Snyk 프로젝트](https://snyk.io/) 입니다.

### 종속성 확인

```bash
npm ls date-fns
yarn why date-fns
```

이 명령은 설치된 종속성의 버전과 프로젝트에 종속성이 포함되게 된 경로를 표시합니다. 다른 최상위 패키지가 `date-fns`를 가져왔을 수도 있습니다. 프로젝트에 여러 버전의 패키지가 있을 수도 있지만(이상적이지는 않지만) 이는 매우 유용하기 때문에 [lodash](https://lodash.com/) 패키지에서 여러 번 볼 수 있습니다.

패키지 관리자가 패키지의 중복을 제거하기 위해 최선을 다하겠지만 어떤 버전이 설치되어 있는지 정확히 조사하는 것이 좋습니다.

### 추가 명령

[npm](https://docs.npmjs.com/cli-documentation/) 과  [yarn](https://classic.yarnpkg.com/en/docs/cli/) 의 개별 명령에 대한 자세한 내용은 온라인에서 확인할 수 있습니다. 다시 말하지만, [pnpm](https://pnpm.js.org/en/cli/add) 명령은 몇 가지 추가 사항을 제외하고는 npm과 동등합니다.

## 나만의 명령어 만들기

패키지 관리자는 자신만의 명령을 만들어 명령줄에서 실행하는 기능도 지원합니다. 예를 들어 다음과 같은 명령을 만들 수 있습니다:

```bash
npm run dev
# or yarn run dev
```

이렇게 하면 "개발 모드"에서 프로젝트를 시작하기 위한 사용자 정의 스크립트가 실행됩니다. 실제로 로컬 개발 설정은 프로덕션에서 실행되는 방식과 약간 다르게 실행되는 경향이 있기 때문에 모든 프로젝트에 이 기능을 정기적으로 포함시킵니다.

이전 Parcel 테스트 프로젝트에서 이 스크립트를 실행하면 "dev script is missing"이라는 메시지가 표시될 수 있습니다. 이는 npm, Yarn 등이 `package.json` 파일의 `scripts` 속성에서 dev라는 속성을 찾고 있기 때문입니다.

Parcel은 `parcel serve filename.html` 명령을 사용하여 개발 서버를 실행할 수 있으며, 개발 중에 이 명령을 자주 사용하고자 합니다.

따라서 `package.json`에 사용자 지정 단축 명령인 "dev"를 만들어 보겠습니다.

If you followed the tutorial from earlier, you should have a `package.json` file inside your parcel-experiment directory. Open it up, and its `scripts` member should look like this:
앞의 튜토리얼을 따랐다면 parcel-experiment 디렉토리에 `package.json` 파일이 있을 것입니다. 파일을 열면 해당 `scripts` 멤버가 다음과 같이 보일 것입니다:

```json
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
},
```

다음과 같이 보이도록 업데이트하고 파일을 저장합니다:

```json
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "dev": "parcel serve index.html"
},
```

사용자 정의 `dev` 명령을 npm 스크립트로 추가했습니다.

이제 터미널에서 다음을 실행하여 `parcel-experiment` 디렉터리 안에 있는지 확인합니다:

```bash
 npm run dev
```

이렇게 하면 앞서 살펴본 것처럼 Parcel이 시작되고 로컬 개발 서버에서 `index.html`이 제공될 것입니다:

```bash
Server running at http://localhost:1234
✨  Built in 5.48s.
```

또한 npm(및 yarn) 명령은 기존 방법(컴퓨터가 일반적으로 소프트웨어를 저장하고 찾을 수 있도록 허용하는 방법)으로 찾기 전에 프로젝트에 로컬로 설치된 명령줄 도구를 검색한다는 점에서 영리합니다. 대부분의 경우 자체 스크립트가 정상적으로 실행되지만 [`run` 명령의 기술적인 복잡성에 대해 자세히 알아볼](https://docs.npmjs.com/cli/run-script/) 수 있습니다.

`scripts` 속성에 작업 수행에 도움이 되는 모든 종류의 항목을 추가할 수 있습니다. 저희도 그랬고 [다른 사람들도 마찬가지](https://github.com/facebook/create-react-app/blob/c5b96c2853671baa3f1f297ec3b36d7358898304/package.json#L6) 입니다.

## 요약

이것으로 패키지 관리자 둘러보기가 끝났습니다. 다음 단계는 지금까지 배운 모든 것을 실제로 적용하여 샘플 툴체인을 구축하는 것입니다.

{{PreviousMenuNext("Learn/Tools_and_testing/Understanding_client-side_tools/Command_line","Learn/Tools_and_testing/Understanding_client-side_tools/Introducing_complete_toolchain", "Learn/Tools_and_testing/Understanding_client-side_tools")}}

## 참고 항목

- [npm 스크립트 레퍼런스](https://docs.npmjs.com/cli/v8/using-npm/scripts/)
- [package.json 레퍼런스](https://docs.npmjs.com/cli/v8/configuring-npm/package-json/)
