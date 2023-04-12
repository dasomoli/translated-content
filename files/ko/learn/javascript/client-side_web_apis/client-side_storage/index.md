---
title: Client-side storage
slug: Learn/JavaScript/Client-side_web_APIs/Client-side_storage
---

{{LearnSidebar}}

{{PreviousMenu("Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs", "Learn/JavaScript/Client-side_web_APIs")}}

최신 웹 브라우저는 웹사이트가 사용자의 허락을 받아 사용자의 컴퓨터에 데이터를 저장한 후 필요할 때 검색할 수 있는 다양한 방법을 지원합니다. 이를 통해 장기 저장을 위해 데이터를 보존하고, 오프라인 사용을 위해 사이트나 문서를 저장하고, 사이트에 대한 사용자별 설정을 유지하는 등의 작업을 수행할 수 있습니다. 이 문서에서는 이러한 기능이 어떻게 작동하는지에 대한 기본 사항을 설명합니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        JavaScript 기초(
        <a href="/ko/docs/Learn/JavaScript/First_steps">첫 번째 단계</a>,
        <a href="/ko/docs/Learn/JavaScript/Building_blocks"
          >빌딩 블록</a
        >,
        <a href="/ko/docs/Learn/JavaScript/Objects">JavaScript 객체</a> 참조),
        <a href="/ko/docs/Learn/JavaScript/Client-side_web_APIs/Introduction"
          >클라이언트 측 API의 기초</a
        >
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        클라이언트 측 스토리지 API를 사용하여 애플리케이션 데이터를 저장하는 방법을 배웁니다.
      </td>
    </tr>
  </tbody>
</table>

## 클라이언트 측 스토리지?

MDN 학습 영역의 다른 부분에서 [정적 사이트](/ko/docs/Learn/Server-side/First_steps/Client-Server_overview#static_sites) 와 [동적 사이트](/ko/docs/Learn/Server-side/First_steps/Client-Server_overview#dynamic_sites) 의 차이점에 대해 이야기했습니다. 대부분의 주요 최신 웹사이트는 일종의 데이터베이스(서버 측 스토리지)를 사용하여 서버에 데이터를 저장한 다음 [서버 측](/ko/docs/Learn/Server-side) 코드를 실행하여 필요한 데이터를 검색하고 정적 페이지 템플릿에 삽입한 다음 결과 HTML을 클라이언트에 제공하여 사용자의 브라우저에 표시합니다.

클라이언트 측 저장소는 비슷한 원리로 작동하지만 용도는 다릅니다. 클라이언트 측 저장소는 데이터를 클라이언트(즉, 사용자 컴퓨터에)에 저장한 다음 필요할 때 검색할 수 있는 JavaScript API로 구성됩니다. 다음과 같이 다양한 용도로 사용됩니다:

- 사이트 기본 설정 개인화(예: 사용자가 선택한 사용자 지정 위젯, 색 구성표 또는 글꼴 크기 표시).
- 이전 사이트 활동 유지(예: 이전 세션의 장바구니 콘텐츠 저장, 사용자가 이전에 로그인했는지 기억).
- 데이터 및 자산을 로컬에 저장하여 사이트를 더 빠르게 다운로드하거나 네트워크 연결 없이도 사용할 수 있도록(잠재적으로 더 저렴한 비용으로) 합니다.
- 웹 애플리케이션에서 생성된 문서를 로컬에 저장하여 오프라인에서 사용

클라이언트 측 스토리지와 서버 측 스토리지를 함께 사용하는 경우가 많습니다. 예를 들어, 웹 게임이나 음악 플레이어 애플리케이션에서 사용하는 음악 파일을 일괄적으로 다운로드하여 클라이언트 측 데이터베이스에 저장한 후 필요에 따라 재생할 수 있습니다. 사용자는 음악 파일을 한 번만 다운로드하면 되고, 이후 방문 시에는 데이터베이스에서 음악 파일이 검색됩니다.

> **참고:** 클라이언트 측 저장소 API를 사용하여 저장할 수 있는 데이터의 양에는 제한이 있습니다(개별 API당 및 누적 기준). 정확한 제한은 브라우저에 따라 다르며 사용자 설정에 따라 달라질 수 있습니다. 자세한 내용은 [브라우저 저장 용량 할당량 및 퇴거 기준](/ko/docs/Web/API/Storage_API/Storage_quotas_and_eviction_criteria) 을 참조하세요.

### 올드 스쿨: 쿠키

클라이언트 측 저장소 개념은 오래전부터 존재해 왔습니다. 웹 초창기부터 사이트에서는 [쿠키](/ko/docs/Web/HTTP/Cookies) 를 사용하여 정보를 저장하고 웹사이트의 사용자 경험을 개인화했습니다. 쿠키는 웹에서 일반적으로 사용되는 가장 초기의 클라이언트 측 저장소 형태입니다.

요즘에는 클라이언트 측 데이터를 저장하는 더 쉬운 메커니즘이 있으므로 이 글에서는 쿠키 사용 방법을 설명하지 않습니다. 하지만 쿠키가 최신 웹에서 완전히 쓸모없다는 의미는 아니며, 여전히 세션 ID 및 액세스 토큰 등 사용자 개인화 및 상태와 관련된 데이터를 저장하는 데 쿠키가 일반적으로 사용됩니다. 쿠키에 대한 자세한 내용은 [HTTP 쿠키 사용](/ko/docs/Web/HTTP/Cookies) 문서를 참조하세요.

### 새 학교: 웹 스토리지 및 IndexedDB

위에서 언급한 "더 쉬운" 기능은 다음과 같습니다:

- [웹 스토리지 API](/ko/docs/Web/API/Web_Storage_API) 는 이름과 해당 값으로 구성된 더 작은 데이터 항목을 저장하고 검색할 수 있는 메커니즘을 제공합니다. 이는 사용자의 이름, 로그인 여부, 화면 배경에 사용할 색상 등과 같은 간단한 데이터만 저장해야 할 때 유용합니다.
- [IndexedDB API](/ko/docs/Web/API/IndexedDB_API) 는 복잡한 데이터를 저장할 수 있는 완전한 데이터베이스 시스템을 브라우저에 제공합니다. 이는 전체 고객 기록 세트부터 오디오나 비디오 파일과 같은 복잡한 데이터 유형까지 다양한 용도로 사용할 수 있습니다.

아래에서 이러한 API에 대해 자세히 알아보세요.

### 캐시 API

{{domxref("Cache")}} API는 특정 요청에 대한 HTTP 응답을 저장하기 위해 설계되었으며, 웹사이트 자산을 오프라인에 저장하여 나중에 네트워크 연결 없이 사이트를 사용할 수 있도록 하는 등의 작업을 수행하는 데 매우 유용합니다. 캐시는 일반적으로 [서비스 워커 API](/ko/docs/Web/API/Service_Worker_API) 와 함께 사용되지만 반드시 그럴 필요는 없습니다.

캐시 및 서비스 워커의 사용은 고급 주제이므로 이 글에서는 자세히 다루지 않겠지만 아래의 [오프라인 자산 저장소](#offline_asset_storage) 섹션에서 예제를 보여드리겠습니다.

## 간단한 데이터 저장 - 웹 스토리지

[웹 스토리지 API](/ko/docs/Web/API/Web_Storage_API) 는 간단한 이름/값 쌍의 데이터(문자열, 숫자 등으로 제한)를 저장하고 필요할 때 해당 값을 검색하는 등 사용이 매우 간편합니다.

### 기본 구문

방법을 보여드리겠습니다:

1. 먼저 GitHub의 [웹 스토리지 빈 템플릿](https://mdn.github.io/learning-area/javascript/apis/client-side-storage/web-storage/index.html) 으로 이동합니다(새 탭에서 열기).
2. 브라우저 개발자 도구의 JavaScript 콘솔을 엽니다.
3. 모든 웹 스토리지 데이터는 브라우저 내부의 두 개의 객체형 구조, 즉 {{domxref("Window.sessionStorage", "sessionStorage")}} 와 {{domxref("Window.localStorage", "localStorage")}} 에 포함됩니다. 첫 번째는 브라우저가 열려 있는 동안 데이터를 유지하며(브라우저를 닫으면 데이터가 손실됨), 두 번째는 브라우저를 닫았다가 다시 연 후에도 데이터를 유지합니다. 이 글에서는 일반적으로 두 번째가 더 유용하므로 두 번째를 사용하겠습니다.

   {{domxref("Storage.setItem()")}} 메서드를 사용하면 데이터 항목을 저장소에 저장할 수 있으며, 항목 이름과 값이라는 두 가지 매개 변수가 필요합니다. 자바스크립트 콘솔에 이 값을 입력해 보세요(원하는 경우 값을 원하는 이름으로 변경하세요!):

   ```js
   localStorage.setItem("name", "Chris");
   ```

4. {{domxref("Storage.getItem()")}} 메서드는 하나의 매개변수(검색하려는 데이터 항목의 이름)를 받아 항목의 값을 반환합니다. 이제 자바스크립트 콘솔에 다음 코드를 입력합니다:

   ```js
   let myName = localStorage.getItem("name");
   myName;
   ```

   두 번째 줄을 입력하면 이제 `myName` 변수에 `name` 데이터 항목의 값이 포함된 것을 볼 수 있습니다.

5. {{domxref("Storage.removeItem()")}} 메서드는 제거하려는 데이터 항목의 이름이라는 매개변수 하나를 받아 웹 스토리지에서 해당 항목을 제거합니다. 자바스크립트 콘솔에 다음 줄을 입력합니다:

   ```js
   localStorage.removeItem("name");
   myName = localStorage.getItem("name");
   myName;
   ```

   이제 세 번째 줄은 `null`을 반환해야 합니다. `name` 항목이 더 이상 웹 저장소에 존재하지 않습니다.

### 데이터는 지속됩니다!

웹 스토리지의 주요 기능 중 하나는 페이지가 로드될 때마다 데이터가 지속된다는 점입니다(`localStorage`의 경우 브라우저가 종료된 상태에서도). 실제로 어떻게 작동하는지 살펴봅시다.

1. 웹 스토리지 빈 템플릿을 다시 열되, 이번에는 이 튜토리얼을 열었던 브라우저와 다른 브라우저에서 열어보세요! 이렇게 하면 더 쉽게 처리할 수 있습니다.
2. 브라우저의 자바스크립트 콘솔에 다음 줄을 입력합니다:

   ```js
   localStorage.setItem("name", "Chris");
   let myName = localStorage.getItem("name");
   myName;
   ```

   이름 항목이 반환된 것을 볼 수 있을 것입니다.

3. 이제 브라우저를 닫았다가 다시 엽니다.
4. 다음 줄을 다시 입력합니다:

   ```js
   let myName = localStorage.getItem("name");
   myName;
   ```

   브라우저를 닫았다가 다시 열어도 값을 계속 사용할 수 있는 것을 확인할 수 있습니다.

### 각 도메인에 대한 별도의 저장소

각 도메인마다 별도의 데이터 저장소가 있습니다(브라우저에 로드되는 각각의 개별 웹 주소). 두 개의 웹사이트(예: google.com과 amazon.com)를 로드하고 한 웹사이트에 항목을 저장하려고 하면 다른 웹사이트에서는 해당 항목을 사용할 수 없는 것을 볼 수 있습니다.

웹사이트가 서로의 데이터를 볼 수 있다면 어떤 보안 문제가 발생할지 상상할 수 있습니다!

### 좀 더 복잡한 예

웹 스토리지를 어떻게 사용할 수 있는지에 대한 아이디어를 제공하기 위해 작업 예제를 작성하여 새로 알게 된 지식을 적용해 보겠습니다. 이 예제에서는 이름을 입력하면 페이지가 업데이트되어 개인화된 인사말을 제공합니다. 이름이 웹 스토리지에 저장되므로 페이지/브라우저를 다시 로드할 때에도 이 상태가 유지됩니다.

예제 HTML은 [personal-greeting.html](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/web-storage/personal-greeting.html) 에서 찾을 수 있으며, 여기에는 헤더, 콘텐츠, 바닥글이 있는 웹사이트와 이름을 입력하는 양식이 포함되어 있습니다.

![A Screenshot of a website that has a header, content and footer sections. The header has a welcome text to the left-hand side and a button labelled 'forget' to the right-hand side. The content has an heading followed by a two paragraphs of dummy text. The footer reads 'Copyright nobody. Use the code as you like'.](web-storage-demo.png)

작동 원리를 이해할 수 있도록 예제를 구축해 보겠습니다.

1. 먼저 컴퓨터의 새 디렉터리에 [personal-greeting.html](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/web-storage/personal-greeting.html) 파일의 로컬 복사본을 만듭니다.
2. 다음으로, HTML이 `<script src="index.js" defer></script>`와 같은 줄을 통해 `index.js`라는 JavaScript 파일을 참조하는 방식을 주목하세요. 이 파일을 생성하고 여기에 자바스크립트 코드를 작성해야 합니다. HTML 파일과 같은 디렉토리에 `index.js` 파일을 만듭니다.
3. 이 예제에서 조작해야 하는 모든 HTML 기능에 대한 참조를 만드는 것부터 시작하겠습니다. 이러한 참조는 앱의 수명 주기 동안 변경할 필요가 없으므로 모두 상수로 만들겠습니다. 자바스크립트 파일에 다음 줄을 추가합니다:

   ```js
   // create needed constants
   const rememberDiv = document.querySelector(".remember");
   const forgetDiv = document.querySelector(".forget");
   const form = document.querySelector("form");
   const nameInput = document.querySelector("#entername");
   const submitBtn = document.querySelector("#submitname");
   const forgetBtn = document.querySelector("#forgetname");

   const h1 = document.querySelector("h1");
   const personalGreeting = document.querySelector(".personal-greeting");
   ```

4. 다음으로, 제출 버튼을 눌렀을 때 양식이 실제로 제출되지 않도록 작은 이벤트 리스너를 포함시켜야 하는데, 이는 우리가 원하는 동작이 아니기 때문입니다. 이전 코드 아래에 이 스니펫을 추가하세요:

   ```js
   // Stop the form from submitting when a button is pressed
   form.addEventListener("submit", (e) => e.preventDefault());
   ```

5. 이제 "Say hello" 버튼을 클릭할 때 핸들러 함수가 실행될 이벤트 리스너를 추가해야 합니다. 주석에 각 비트의 기능이 자세히 설명되어 있지만, 기본적으로 여기서는 사용자가 텍스트 입력 상자에 입력한 이름을 가져와 `setItem()`을 사용하여 웹 스토리지에 저장한 다음 실제 웹사이트 텍스트 업데이트를 처리하는 `nameDisplayCheck()`라는 함수를 실행하고 있습니다. 이 함수를 코드 하단에 추가하세요:

   ```js
   // run function when the 'Say hello' button is clicked
   submitBtn.addEventListener("click", () => {
     // store the entered name in web storage
     localStorage.setItem("name", nameInput.value);
     // run nameDisplayCheck() to sort out displaying the personalized greetings and updating the form display
     nameDisplayCheck();
   });
   ```

6. 이 시점에서 "Forget" 버튼을 클릭했을 때 함수를 실행할 이벤트 핸들러도 필요합니다. 이 함수는 "Say hello" 버튼을 클릭한 후에만 표시됩니다(두 양식 상태가 앞뒤로 토글됨). 이 함수에서는 `removeItem()`을 사용하여 웹 스토리지에서 `name` 항목을 제거한 다음 `nameDisplayCheck()`를 다시 실행하여 디스플레이를 업데이트합니다. 이것을 하단에 추가합니다:

   ```js
   // run function when the 'Forget' button is clicked
   forgetBtn.addEventListener("click", () => {
     // Remove the stored name from web storage
     localStorage.removeItem("name");
     // run nameDisplayCheck() to sort out displaying the generic greeting again and updating the form display
     nameDisplayCheck();
   });
   ```

7. 이제 `nameDisplayCheck()` 함수 자체를 정의할 차례입니다. 여기서는 조건부 테스트로 `localStorage.getItem('name')`을 사용하여 이름 항목이 웹 스토리지에 저장되었는지 여부를 확인합니다. 이름이 저장되어 있으면 이 호출은 `true`으로 평가되고, 저장되어 있지 않으면 `false`으로 평가됩니다. 호출이 `true`로 평가되면 개인화된 인사말을 표시하고 양식의 "forget" 부분을 표시하고 양식의 "Say hello" 부분을 숨깁니다. 호출이 `false`으로 평가되면 일반 인사말을 표시하고 그 반대의 작업을 수행합니다. 다시 하단에 다음 코드를 넣습니다:

   ```js
   // define the nameDisplayCheck() function
   function nameDisplayCheck() {
     // check whether the 'name' data item is stored in web Storage
     if (localStorage.getItem("name")) {
       // If it is, display personalized greeting
       const name = localStorage.getItem("name");
       h1.textContent = `Welcome, ${name}`;
       personalGreeting.textContent = `Welcome to our website, ${name}! We hope you have fun while you are here.`;
       // hide the 'remember' part of the form and show the 'forget' part
       forgetDiv.style.display = "block";
       rememberDiv.style.display = "none";
     } else {
       // if not, display generic greeting
       h1.textContent = "Welcome to our website ";
       personalGreeting.textContent =
         "Welcome to our website. We hope you have fun while you are here.";
       // hide the 'forget' part of the form and show the 'remember' part
       forgetDiv.style.display = "none";
       rememberDiv.style.display = "block";
     }
   }
   ```

8. 마지막으로, 페이지가 로드될 때 `nameDisplayCheck()` 함수를 실행해야 합니다. 이 작업을 수행하지 않으면 페이지를 다시 로드할 때 개인화된 인사말이 유지되지 않습니다. 코드 하단에 다음을 추가합니다:

   ```js
   nameDisplayCheck();
   ```

예제가 완성되었습니다 - 잘했습니다! 이제 코드를 저장하고 브라우저에서 HTML 페이지를 테스트하는 일만 남았습니다. [완성된 버전은 여기에서 실시간으로 실행](https://mdn.github.io/learning-area/javascript/apis/client-side-storage/web-storage/personal-greeting.html) 되는 것을 확인할 수 있습니다.

> **참고:** [웹 스토리지 API 사용하기](/ko/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API) 에서 약간 더 복잡한 또 다른 예제를 살펴볼 수 있습니다.

> **참고:** 완성된 버전 소스의 `<script src="index.js" defer></script>` 줄에서 `defer` 속성은 페이지 로딩이 완료될 때까지 {{htmlelement("script")}} 요소의 콘텐츠가 실행되지 않도록 지정합니다.

## 복잡한 데이터 저장 - IndexedDB

[IndexedDB API](/ko/docs/Web/API/IndexedDB_API)(약칭 IDB)는 브라우저에서 사용할 수 있는 완전한 데이터베이스 시스템으로, 그 유형이 문자열이나 숫자와 같은 단순한 값에 국한되지 않는 복잡한 관련 데이터를 저장할 수 있습니다. 동영상, 이미지 등 거의 모든 종류의 데이터를 IndexedDB 인스턴스에 저장할 수 있습니다.

IndexedDB API를 사용하면 데이터베이스를 만든 다음 해당 데이터베이스 내에 객체 저장소를 만들 수 있습니다.
객체 저장소는 관계형 데이터베이스의 테이블과 같으며 각 객체 저장소에는 여러 개의 객체가 포함될 수 있습니다.
IndexedDB API에 대해 자세히 알아보려면 [IndexedDB 사용](/ko/docs/Web/API/IndexedDB_API/Using_IndexedDB) 을 참조하세요.

그러나 여기에는 대가가 따릅니다. IndexedDB는 웹 스토리지 API보다 사용하기가 훨씬 더 복잡합니다. 이 섹션에서는 인덱싱된 데이터베이스의 기능 중 극히 일부만 소개하지만, 시작하기에 충분한 정보를 제공할 것입니다.

### 노트 스토리지 예제 살펴보기

여기서는 브라우저에 노트를 저장하고 원할 때 언제든 보고 삭제할 수 있는 예제를 통해 직접 구축해보고 IDB의 가장 기본적인 부분을 설명해 드리겠습니다.

앱은 다음과 같은 모습입니다:

![IndexDB notes demo screenshot with 4 sections. The first section is the header. The second section lists all the notes that have been created. It has two notes, each with a delete button. A third section is a form with 2 input fields for 'Note title' and 'Note text' and a button labeled 'Create new note'. The bottom section footer reads 'Copyright nobody. Use the code as you like'.](idb-demo.png)

각 노트에는 제목과 본문 텍스트가 있으며, 각각 개별적으로 편집할 수 있습니다. 아래에서 살펴볼 JavaScript 코드에는 무슨 일이 벌어지고 있는지 이해하는 데 도움이 되는 자세한 주석이 있습니다.

### 시작하기

1. 우선,  [`index.html`](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/indexeddb/notes/index.html), [`style.css`](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/indexeddb/notes/style.css), [`index-start.js`](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/indexeddb/notes/index-start.js) 파일의 로컬 복사본을 로컬 컴퓨터의 새 디렉터리에 만듭니다.
2. 파일을 살펴보세요. HTML은 머리글과 바닥글이 있는 웹사이트와 노트를 표시할 장소가 포함된 메인 콘텐츠 영역, 데이터베이스에 새 노트를 입력하는 양식을 정의하고 있음을 알 수 있을 것입니다. CSS는 무슨 일이 일어나고 있는지 더 명확히 알 수 있도록 몇 가지 스타일링을 제공합니다. JavaScript 파일에는 노트가 표시될 {{htmlelement("ul")}} 요소, 제목과 본문 {{htmlelement("input")}} 요소, {{htmlelement("form")}} 자체, {{htmlelement("button")}} 에 대한 참조를 포함하는 5개의 선언된 상수가 포함되어 있습니다.
3. JavaScript 파일의 이름을 `index.js`로 바꿉니다. 이제 코드를 추가할 준비가 되었습니다.

### 데이터베이스 초기 설정

이제 실제로 데이터베이스를 설정하기 위해 가장 먼저 해야 할 일을 살펴봅시다.

1. 상수 선언 아래에 다음 줄을 추가합니다:

   ```js
   // Create an instance of a db object for us to store the open database in
   let db;
   ```

   여기서는 `db`라는 변수를 선언하고 있는데, 이 변수는 나중에 데이터베이스를 나타내는 객체를 저장하는 데 사용됩니다. 이 변수는 나중에 데이터베이스를 나타내는 객체를 저장하는 데 사용됩니다.

2. 다음으로 다음을 추가합니다:

   ```js
   // Open our database; it is created if it doesn't already exist
   // (see the upgradeneeded handler below)
   const openRequest = window.indexedDB.open("notes_db", 1);
   ```

   이 줄은 `notes_db`라는 데이터베이스의 버전 `1`을 열기 위한 요청을 생성합니다. 이 데이터베이스가 아직 존재하지 않는 경우 후속 코드에서 생성됩니다. 이 요청 패턴은 IndexedDB 전체에서 매우 자주 사용되는 것을 볼 수 있습니다. 데이터베이스 작업에는 시간이 걸립니다. 결과를 기다리는 동안 브라우저를 중단하고 싶지 않기 때문에 데이터베이스 작업은 {{Glossary("asynchronous")}} 이며, 즉 즉시 수행되는 것이 아니라 미래의 어느 시점에 수행되고 완료되면 알림을 받습니다.

   IndexedDB에서 이 작업을 처리하려면 요청 객체를 생성합니다(원하는 대로 호출할 수 있습니다. 여기서는 `openRequest`라고 했으므로 용도가 분명합니다). 그런 다음 이벤트 핸들러를 사용하여 요청이 완료되거나 실패할 때 코드를 실행합니다(아래에서 사용 중임을 확인할 수 있습니다).

   > **참고:** 버전 번호가 중요합니다. 데이터베이스를 업그레이드하려면(예: 테이블 구조를 변경하는 등) 버전 번호를 늘리거나 `upgradeneeded` 처리기 내부에 다른 스키마를 지정하는 등의 방법으로 코드를 다시 실행해야 합니다(아래 참조). 이 튜토리얼에서는 데이터베이스 업그레이드를 다루지 않습니다.

3. 이제 이전에 추가한 바로 아래에 다음 이벤트 핸들러를 추가합니다.

   ```js
   // error handler signifies that the database didn't open successfully
   openRequest.addEventListener("error", () =>
     console.error("Database failed to open")
   );

   // success handler signifies that the database opened successfully
   openRequest.addEventListener("success", () => {
     console.log("Database opened successfully");

     // Store the opened database object in the db variable. This is used a lot below
     db = openRequest.result;

     // Run the displayData() function to display the notes already in the IDB
     displayData();
   });
   ```

   시스템에서 요청이 실패했다는 메시지가 돌아오면 {{domxref("IDBRequest/error_event", "error")}} 이벤트 처리기가 실행됩니다. 이를 통해 이 문제에 대응할 수 있습니다. 이 예제에서는 자바스크립트 콘솔에 메시지를 인쇄하기만 하면 됩니다.
   
   요청이 성공적으로 반환되면, 즉 데이터베이스가 성공적으로 열리면 {{domxref("IDBRequest/success_event", "success")}} 이벤트 핸들러가 실행됩니다. 이 경우 열린 데이터베이스를 나타내는 객체가 {{domxref("IDBRequest.result", "openRequest.result")}} 속성에서 사용 가능해져 데이터베이스를 조작할 수 있습니다. 나중에 사용할 수 있도록 앞서 만든 `db` 변수에 저장합니다. 또한 {{HTMLElement("ul")}} 안에 데이터베이스의 데이터를 표시하는 `displayData()`라는 함수를 실행합니다. 지금 이 함수를 실행하면 페이지가 로드되는 즉시 데이터베이스에 이미 있는 노트가 표시됩니다. 나중에 `displayData()`가 정의된 것을 보실 수 있습니다.

4. 마지막으로 이 섹션에서는 데이터베이스를 설정하는 데 가장 중요한 이벤트 핸들러인 {{domxref("IDBOpenDBRequest/upgradeneeded_event", "upgradeneeded")}} 를 추가하겠습니다. 이 핸들러는 데이터베이스가 아직 설정되지 않았거나 기존 저장된 데이터베이스보다 더 큰 버전 번호로 데이터베이스를 열 경우(업그레이드를 수행할 때) 실행됩니다. 이전 핸들러 아래에 다음 코드를 추가합니다:

   ```js
   // Set up the database tables if this has not already been done
   openRequest.addEventListener("upgradeneeded", (e) => {
     // Grab a reference to the opened database
     db = e.target.result;

     // Create an objectStore in our database to store notes and an auto-incrementing key
     // An objectStore is similar to a 'table' in a relational database
     const objectStore = db.createObjectStore("notes_os", {
       keyPath: "id",
       autoIncrement: true,
     });

     // Define what data items the objectStore will contain
     objectStore.createIndex("title", "title", { unique: false });
     objectStore.createIndex("body", "body", { unique: false });

     console.log("Database setup complete");
   });
   ```

   여기서 데이터베이스의 스키마(구조), 즉 데이터베이스에 포함된 열(또는 필드)의 집합을 정의합니다. 여기서는 먼저 `request` 객체인 이벤트 대상의 `result` 속성(`e.target.result`)에서 기존 데이터베이스에 대한 참조를 가져옵니다. 이는 `success` 이벤트 핸들러 내부의 `db = openRequest.result;` 줄과 동일하지만, `upgradeneeded` 이벤트 핸들러(필요한 경우)가 `success` 이벤트 핸들러보다 먼저 실행되므로 이 작업을 수행하지 않으면 `db` 값을 사용할 수 없으므로 여기서는 별도로 수행해야 합니다.

   그런 다음 {{domxref("IDBDatabase.createObjectStore()")}} 를 사용하여 열린 데이터베이스 내에 `notes_os`라는 새 객체 저장소를 만듭니다. 이것은 기존 데이터베이스 시스템에서 단일 테이블에 해당합니다. 여기에 notes라는 이름을 지정하고 `id`라는 `autoIncrement` 키 필드를 지정했습니다. 새 레코드가 생성될 때마다 자동으로 증가된 값이 주어지므로 개발자가 명시적으로 설정할 필요가 없습니다. 키가 되는 `id` 필드는 레코드를 삭제하거나 표시할 때와 같이 레코드를 고유하게 식별하는 데 사용됩니다.

   또한 {{domxref("IDBObjectStore.createIndex()")}} 메서드를 사용해 `title`(각 노트의 제목을 포함)과 `body`(노트의 본문 텍스트를 포함)이라는 두 개의 다른 색인(필드)을 만듭니다.

이 데이터베이스 스키마가 설정되었으므로 데이터베이스에 레코드를 추가하기 시작하면 각 레코드는 이 라인을 따라 하나의 객체로 표시됩니다:

```json
{
  "title": "Buy milk",
  "body": "Need both cows milk and soy.",
  "id": 8
}
```

### 데이터베이스에 데이터 추가하기

이제 데이터베이스에 레코드를 추가하는 방법을 살펴봅시다. 이 작업은 페이지의 양식을 사용하여 수행됩니다.

이전 이벤트 핸들러 아래에 다음 줄을 추가하여 양식이 제출될 때(제출 {{htmlelement("button")}} 을 눌러 양식 제출에 성공할 때) `addData()`라는 함수를 실행하는 `submit` 이벤트 핸들러를 설정합니다:

```js
// Create a submit event handler so that when the form is submitted the addData() function is run
form.addEventListener("submit", addData);
```

이제 `addData()` 함수를 정의해 보겠습니다. 이전 줄 아래에 추가하세요:

```js
// Define the addData() function
function addData(e) {
  // prevent default - we don't want the form to submit in the conventional way
  e.preventDefault();

  // grab the values entered into the form fields and store them in an object ready for being inserted into the DB
  const newItem = { title: titleInput.value, body: bodyInput.value };

  // open a read/write db transaction, ready for adding the data
  const transaction = db.transaction(["notes_os"], "readwrite");

  // call an object store that's already been added to the database
  const objectStore = transaction.objectStore("notes_os");

  // Make a request to add our newItem object to the object store
  const addRequest = objectStore.add(newItem);

  addRequest.addEventListener("success", () => {
    // Clear the form, ready for adding the next entry
    titleInput.value = "";
    bodyInput.value = "";
  });

  // Report on the success of the transaction completing, when everything is done
  transaction.addEventListener("complete", () => {
    console.log("Transaction completed: database modification finished.");

    // update the display of data to show the newly added item, by running displayData() again.
    displayData();
  });

  transaction.addEventListener("error", () =>
    console.log("Transaction not opened due to error")
  );
}
```

이는 매우 복잡한 문제이므로 세분화하여 설명합니다:

- 이벤트 객체에서 {{domxref("Event.preventDefault()")}} 를 실행하여 기존 방식으로 양식이 실제로 제출되는 것을 중지합니다(이 경우 페이지 새로 고침이 발생하여 경험이 손상될 수 있음).
- 데이터베이스에 입력할 레코드를 나타내는 객체를 생성하여 양식 입력값으로 채웁니다. 앞서 설명한 것처럼 `id` 값을 명시적으로 포함할 필요는 없습니다. 이 값은 자동으로 채워집니다.
- {{domxref("IDBDatabase.transaction()")}} 메서드를 사용하여 `notes_os` 객체 저장소에 대한 `readwrite` 트랜잭션을 엽니다. 이 트랜잭션 객체를 사용하면 객체 저장소에 액세스하여 새 레코드를 추가하는 등의 작업을 수행할 수 있습니다.
- {{domxref("IDBTransaction.objectStore()")}} 메서드를 사용하여 객체 저장소에 액세스하고 결과를 `objectStore` 변수에 저장합니다.
- {{domxref("IDBObjectStore.add()")}} 를 사용하여 데이터베이스에 새 레코드를 추가합니다. 이렇게 하면 앞서 살펴본 것과 동일한 방식으로 요청 객체가 생성됩니다.
- 라이프사이클의 중요한 지점에서 코드를 실행하기 위해 `request`과 `transaction` 객체에 여러 이벤트 핸들러를 추가합니다. 요청이 성공하면 다음 노트를 입력할 준비를 위해 양식 입력을 지웁니다. 트랜잭션이 완료되면 `displayData()` 함수를 다시 실행해 페이지의 노트 표시를 업데이트합니다.

### 데이터 표시

이미 코드에서 `displayData()` 함수를 두 번 참조했으므로 이 함수를 정의하는 것이 좋습니다. 이전 함수 정의 아래에 이 함수를 코드에 추가하세요:

```js
// Define the displayData() function
function displayData() {
  // Here we empty the contents of the list element each time the display is updated
  // If you didn't do this, you'd get duplicates listed each time a new note is added
  while (list.firstChild) {
    list.removeChild(list.firstChild);
  }

  // Open our object store and then get a cursor - which iterates through all the
  // different data items in the store
  const objectStore = db.transaction("notes_os").objectStore("notes_os");
  objectStore.openCursor().addEventListener("success", (e) => {
    // Get a reference to the cursor
    const cursor = e.target.result;

    // If there is still another data item to iterate through, keep running this code
    if (cursor) {
      // Create a list item, h3, and p to put each data item inside when displaying it
      // structure the HTML fragment, and append it inside the list
      const listItem = document.createElement("li");
      const h3 = document.createElement("h3");
      const para = document.createElement("p");

      listItem.appendChild(h3);
      listItem.appendChild(para);
      list.appendChild(listItem);

      // Put the data from the cursor inside the h3 and para
      h3.textContent = cursor.value.title;
      para.textContent = cursor.value.body;

      // Store the ID of the data item inside an attribute on the listItem, so we know
      // which item it corresponds to. This will be useful later when we want to delete items
      listItem.setAttribute("data-note-id", cursor.value.id);

      // Create a button and place it inside each listItem
      const deleteBtn = document.createElement("button");
      listItem.appendChild(deleteBtn);
      deleteBtn.textContent = "Delete";

      // Set an event handler so that when the button is clicked, the deleteItem()
      // function is run
      deleteBtn.addEventListener("click", deleteItem);

      // Iterate to the next item in the cursor
      cursor.continue();
    } else {
      // Again, if list item is empty, display a 'No notes stored' message
      if (!list.firstChild) {
        const listItem = document.createElement("li");
        listItem.textContent = "No notes stored.";
        list.appendChild(listItem);
      }
      // if there are no more cursor items to iterate through, say so
      console.log("Notes all displayed");
    }
  });
}
```

다시 한 번 자세히 살펴보겠습니다:

- 먼저 {{htmlelement("ul")}} 요소의 콘텐츠를 비운 다음 업데이트된 콘텐츠로 채웁니다. 이렇게 하지 않으면 업데이트할 때마다 중복된 콘텐츠가 엄청나게 많은 목록이 추가됩니다.
- 다음으로, `addData()`에서 했던 것처럼 {{domxref("IDBDatabase.transaction()")}} 및 {{domxref("IDBTransaction.objectStore()")}}를 사용하여 `notes_os` 객체 저장소에 대한 참조를 가져옵니다(단, 여기서는 한 줄로 연결한다는 점이 다릅니다).
- 다음 단계는 {{domxref("IDBObjectStore.openCursor()")}} 메서드를 사용하여 커서 요청을 여는 것입니다. 이 메서드는 객체 저장소의 레코드를 반복하는 데 사용할 수 있는 구조체입니다. 코드를 더 간결하게 만들기 위해 이 줄의 끝에 `success` 이벤트 핸들러를 연결하여 커서가 성공적으로 반환되면 핸들러가 실행됩니다.
- `const cursor = e.target.result`를 사용하여 커서 자체({{domxref("IDBCursor")}} 객체)에 대한 참조를 가져옵니다.
- 다음으로 커서에 데이터스토어의 레코드가 포함되어 있는지 확인합니다(`if (cursor){ }`) - 만약 그렇다면 DOM 조각을 생성하고 레코드의 데이터로 채운 다음 페이지에 삽입합니다(`<ul>` 요소 내부). 또한 삭제 버튼을 클릭하면 다음 섹션에서 살펴볼 `deleteItem()` 함수를 실행하여 해당 노트를 삭제하는 삭제 버튼도 포함합니다.
- `if` 블록의 마지막에는 {{domxref("IDBCursor.continue()")}} 메서드를 사용해 데이터스토어의 다음 레코드로 커서를 이동하고 `if` 블록의 내용을 다시 실행합니다. 반복할 다른 레코드가 있으면 해당 레코드가 페이지에 삽입된 다음 `continue()`가 다시 실행되는 식으로 반복됩니다.
- 반복할 레코드가 더 이상 없으면 `cursor`가 정의되지 않은 상태로 반환되므로 `if` 블록 대신 `else` 블록이 실행됩니다. 이 블록은 `<ul>`에 노트가 삽입되었는지 확인하고, 그렇지 않은 경우 노트가 저장되지 않았다는 메시지를 삽입합니다.

### 노트 삭제

위에서 설명한 것처럼 노트의 삭제 버튼을 누르면 노트가 삭제됩니다. 삭제는 다음과 같은 `deleteItem()` 함수를 통해 이루어집니다:

```js
// Define the deleteItem() function
function deleteItem(e) {
  // retrieve the name of the task we want to delete. We need
  // to convert it to a number before trying to use it with IDB; IDB key
  // values are type-sensitive.
  const noteId = Number(e.target.parentNode.getAttribute("data-note-id"));

  // open a database transaction and delete the task, finding it using the id we retrieved above
  const transaction = db.transaction(["notes_os"], "readwrite");
  const objectStore = transaction.objectStore("notes_os");
  const deleteRequest = objectStore.delete(noteId);

  // report that the data item has been deleted
  transaction.addEventListener("complete", () => {
    // delete the parent of the button
    // which is the list item, so it is no longer displayed
    e.target.parentNode.parentNode.removeChild(e.target.parentNode);
    console.log(`Note ${noteId} deleted.`);

    // Again, if list item is empty, display a 'No notes stored' message
    if (!list.firstChild) {
      const listItem = document.createElement("li");
      listItem.textContent = "No notes stored.";
      list.appendChild(listItem);
    }
  });
}
```

- 삭제할 레코드의 ID는 `Number(e.target.parentNode.getAttribute('data-note-id'))`를 사용하여 검색합니다. 레코드가 처음 표시될 때 `<li>`의 `data-note-id` 속성에 저장되었다는 점을 기억하세요. 그러나 이 속성은 데이터 유형이 문자열이므로 숫자를 기대하는 데이터베이스에서 인식하지 못하므로 글로벌 내장 [`Number()`](/ko/docs/Web/JavaScript/Reference/Global_Objects/Number) 객체를 통해 전달해야 합니다.
- 그런 다음 앞에서 본 것과 동일한 패턴을 사용하여 객체 저장소에 대한 참조를 가져오고 {{domxref("IDBObjectStore.delete()")}} 메서드를 사용하여 ID를 전달하여 데이터베이스에서 레코드를 삭제합니다.
- 데이터베이스 트랜잭션이 완료되면 DOM에서 노트의 `<li>`를 삭제하고 다시 한 번 `<ul>`이 비어 있는지 확인하여 적절하게 노트를 삽입합니다.

여기까지입니다! 이제 예제가 작동합니다.

문제가 있으시다면 [라이브 예제와 비교해 확인](https://mdn.github.io/learning-area/javascript/apis/client-side-storage/indexeddb/notes/) 해 보세요([소스 코드](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/indexeddb/notes/index.js) 도 참조하세요).

### IndexedDB를 통한 복잡한 데이터 저장

위에서 언급했듯이 IndexedDB는 단순한 텍스트 문자열 이상의 것을 저장하는 데 사용할 수 있습니다. 비디오나 이미지 블롭과 같은 복잡한 객체를 포함하여 원하는 거의 모든 것을 저장할 수 있습니다. 그리고 다른 유형의 데이터보다 훨씬 더 어렵지 않습니다.

이를 수행하는 방법을 보여드리기 위해 [IndexedDB 비디오 스토어](https://github.com/mdn/learning-area/tree/main/javascript/apis/client-side-storage/indexeddb/video-store) 라는 또 다른 예제를 작성했습니다([여기에서도 실행 중인 예제](https://mdn.github.io/learning-area/javascript/apis/client-side-storage/indexeddb/video-store/) 참조). 이 예제를 처음 실행하면 네트워크에서 모든 비디오를 다운로드하여 IndexedDB 데이터베이스에 저장한 다음 {{htmlelement("video")}} 요소 내부의 UI에 비디오를 표시합니다. 두 번째로 실행하면 데이터베이스에서 동영상을 찾아서 표시하기 전에 거기에서 가져와서 표시하므로 후속 로드가 훨씬 빠르고 대역폭을 덜 소모합니다.

이 예제에서 가장 흥미로운 부분을 살펴봅시다. 많은 부분이 이전 예제와 유사하며 코드에 주석이 잘 처리되어 있습니다.

1. 이 예제에서는 가져올 동영상의 이름을 객체 배열에 저장했습니다:

   ```js
   const videos = [
     { name: "crystal" },
     { name: "elf" },
     { name: "frog" },
     { name: "monster" },
     { name: "pig" },
     { name: "rabbit" },
   ];
   ```

2. 우선 데이터베이스가 성공적으로 열리면 `init()` 함수를 실행합니다. 이 함수는 여러 동영상 이름을 반복하여 각 이름으로 식별되는 레코드를 `videos` 데이터베이스에서 로드하려고 시도합니다.

   각 비디오가 데이터베이스에서 발견되면(`request.result`가 `true`로 평가되는지 확인하여 확인 - 레코드가 없으면 `undefined`) 해당 비디오 파일(블롭으로 저장됨)과 비디오 이름이 `displayVideo()` 함수에 바로 전달되어 UI에 배치됩니다. 그렇지 않은 경우, 비디오 이름은 네트워크에서 비디오를 가져오기 위해 `fetchVideoFromNetwork()` 함수에 전달됩니다.

   ```js
   function init() {
     // Loop through the video names one by one
     for (const video of videos) {
       // Open transaction, get object store, and get() each video by name
       const objectStore = db.transaction("videos_os").objectStore("videos_os");
       const request = objectStore.get(video.name);
       request.addEventListener("success", () => {
         // If the result exists in the database (is not undefined)
         if (request.result) {
           // Grab the videos from IDB and display them using displayVideo()
           console.log("taking videos from IDB");
           displayVideo(
             request.result.mp4,
             request.result.webm,
             request.result.name
           );
         } else {
           // Fetch the videos from the network
           fetchVideoFromNetwork(video);
         }
       });
     }
   }
   ```

3. 다음 코드 조각은 `fetchVideoFromNetwork()` 내부에서 가져온 것으로, 여기서는 두 개의 개별 {{domxref("fetch()")}} 요청을 사용하여 MP4 및 WebM 버전의 비디오를 가져옵니다. 그런 다음 {{domxref("Response.blob()")}} 메서드를 사용하여 각 응답의 본문을 블롭으로 추출하여 나중에 저장하고 표시할 수 있는 비디오의 객체 표현을 제공합니다.

   이 두 요청은 모두 비동기적이지만 두 약속이 모두 이행되었을 때만 비디오를 표시하거나 저장하려고 한다는 문제가 있습니다. 다행히도 이러한 문제를 처리하는 내장 메서드인 {{jsxref("Promise.all()")}} 이 있습니다. 이 메서드는 하나의 인수(이행 여부를 확인하려는 모든 개별 프로미스에 대한 참조를 배열에 배치)를 받아 모든 개별 프로미스가 이행될 때 이행된 프로미스를 반환합니다.

   이 프로미스에 대한 `then()` 핸들러 내부에서는 이전과 마찬가지로 `displayVideo()` 함수를 호출하여 UI에 동영상을 표시한 다음 `storeVideo()` 함수를 호출하여 해당 동영상을 데이터베이스에 저장합니다.

   ```js
   // Fetch the MP4 and WebM versions of the video using the fetch() function,
   // then expose their response bodies as blobs
   const mp4Blob = fetch(`videos/${video.name}.mp4`).then((response) =>
     response.blob()
   );
   const webmBlob = fetch(`videos/${video.name}.webm`).then((response) =>
     response.blob()
   );

   // Only run the next code when both promises have fulfilled
   Promise.all([mp4Blob, webmBlob]).then((values) => {
     // display the video fetched from the network with displayVideo()
     displayVideo(values[0], values[1], video.name);
     // store it in the IDB using storeVideo()
     storeVideo(values[0], values[1], video.name);
   });
   ```

4. 먼저 `storeVideo()`를 살펴봅시다. 이는 데이터베이스에 데이터를 추가하는 이전 예제에서 보았던 패턴과 매우 유사합니다. `readwrite` 트랜잭션을 열고 `videos_os` 객체 저장소에 대한 참조를 가져와서 데이터베이스에 추가할 레코드를 나타내는 객체를 만든 다음 {{domxref("IDBObjectStore.add()")}}를 사용하여 추가합니다.

   ```js
   // Define the storeVideo() function
   function storeVideo(mp4, webm, name) {
     // Open transaction, get object store; make it a readwrite so we can write to the IDB
     const objectStore = db
       .transaction(["videos_os"], "readwrite")
       .objectStore("videos_os");

     // Add the record to the IDB using add()
     const request = objectStore.add({ mp4, webm, name });

     request.addEventListener("success", () =>
       console.log("Record addition attempt finished")
     );
     request.addEventListener("error", () => console.error(request.error));
   }
   ```

5. 마지막으로, UI에 비디오를 삽입하는 데 필요한 DOM 요소를 생성한 다음 페이지에 추가하는 `displayVideo()` 함수가 있습니다. 이 중 가장 흥미로운 부분은 아래에 표시된 부분으로, 실제로 비디오 블롭을 `<video>` 요소에 표시하려면 {{domxref("URL.createObjectURL()")}} 메서드를 사용하여 객체 URL(메모리에 저장된 비디오 블롭을 가리키는 내부 URL)을 생성해야 합니다. 이 작업이 완료되면 객체 URL을 {{htmlelement("source")}} 요소의 `src` 속성의 값으로 설정하면 정상적으로 작동합니다.

   ```js
   // Define the displayVideo() function
   function displayVideo(mp4Blob, webmBlob, title) {
     // Create object URLs out of the blobs
     const mp4URL = URL.createObjectURL(mp4Blob);
     const webmURL = URL.createObjectURL(webmBlob);

     // Create DOM elements to embed video in the page
     const article = document.createElement("article");
     const h2 = document.createElement("h2");
     h2.textContent = title;
     const video = document.createElement("video");
     video.controls = true;
     const source1 = document.createElement("source");
     source1.src = mp4URL;
     source1.type = "video/mp4";
     const source2 = document.createElement("source");
     source2.src = webmURL;
     source2.type = "video/webm";

     // Embed DOM elements into page
     section.appendChild(article);
     article.appendChild(h2);
     article.appendChild(video);
     video.appendChild(source1);
     video.appendChild(source2);
   }
   ```

## 오프라인 자산 저장

위의 예시에서는 이미 대용량 자산을 두 번 이상 다운로드할 필요 없이 인덱싱된 데이터베이스에 저장하는 앱을 만드는 방법을 보여주었습니다. 이는 이미 사용자 경험을 크게 개선한 것이지만 여전히 한 가지 아쉬운 점이 있습니다. 사이트에 액세스할 때마다 기본 HTML, CSS 및 JavaScript 파일을 다운로드해야 하므로 네트워크에 연결되어 있지 않을 때는 작동하지 않습니다.

![Firefox offline screen with an illustration of a cartoon character to the left-hand side holding a two-pin plug in its right hand and a two-pin socket in its left hand. On the right-hand side there is an Offline Mode message and a button labeled 'Try again'.](ff-offline.png)

바로 이 부분에서 [서비스 워커](/ko/docs/Web/API/Service_Worker_API) 와 밀접하게 관련된 [캐시 API](/ko/docs/Web/API/Cache) 가 등장합니다.

서비스 워커는 브라우저에서 웹사이트에 액세스할 때 특정 출처(웹사이트 또는 특정 도메인의 웹사이트 일부)에 대해 등록되는 JavaScript 파일입니다. 등록되면 해당 오리진에서 사용 가능한 페이지를 제어할 수 있습니다. 로드된 페이지와 네트워크 사이에 위치하여 해당 오리진으로 향하는 네트워크 요청을 가로채는 방식으로 이를 수행합니다.

요청을 가로채면 원하는 모든 작업을 수행할 수 있지만([사용 사례 아이디어](/ko/docs/Web/API/Service_Worker_API#other_use_case_ideas) 참조), 대표적인 예는 네트워크 응답을 오프라인으로 저장한 다음 요청에 대한 응답으로 네트워크의 응답 대신 제공하는 것입니다. 사실상 웹사이트를 완전히 오프라인으로 작동시킬 수 있습니다.

캐시 API는 또 다른 클라이언트 측 저장 메커니즘이지만 약간의 차이가 있는데, HTTP 응답을 저장하도록 설계되었기 때문에 서비스 워커와 매우 잘 작동합니다.

### 서비스 워커 예시

예시를 통해 어떤 모습인지 조금이나마 이해할 수 있도록 예시를 살펴보겠습니다. 이전 섹션에서 살펴본 비디오 스토어 예제의 다른 버전을 만들었는데, 서비스 워커를 통해 캐시 API에 HTML, CSS 및 JavaScript를 저장하여 예제를 오프라인으로 실행할 수 있다는 점을 제외하면 동일한 기능을 수행합니다!

[서비스 워커가 실시간으로 실행되는 IndexedDB 비디오 스토어](https://mdn.github.io/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/) 를 참조하고 [소스 코드도 확인](https://github.com/mdn/learning-area/tree/main/javascript/apis/client-side-storage/cache-sw/video-store-offline) 하세요.

#### 서비스 워커 등록하기

가장 먼저 주목해야 할 것은 기본 JavaScript 파일에 추가 코드가 있다는 것입니다([index.js](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/cache-sw/video-store-offline/index.js) 참조). 먼저 기능 감지 테스트를 수행하여 {{domxref("Navigator")}} 객체에서 `serviceWorker` 멤버를 사용할 수 있는지 확인합니다. 이 테스트가 참으로 반환되면 최소한 서비스 워커의 기본 기능이 지원된다는 것을 알 수 있습니다. 여기에서는 {{domxref("ServiceWorkerContainer.register()")}} 메서드를 사용하여 `sw.js` 파일에 포함된 서비스 워커를 해당 서비스 워커가 상주하는 오리진에 등록하여 동일한 디렉토리 또는 하위 디렉터리에 있는 페이지를 제어할 수 있도록 합니다. 프로미스가 이행되면 서비스 워커가 등록된 것으로 간주됩니다.

```js
// Register service worker to control making site work offline
if ("serviceWorker" in navigator) {
  navigator.serviceWorker
    .register(
      "/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/sw.js"
    )
    .then(() => console.log("Service Worker Registered"));
}
```

> **참고:** 지정된 `sw.js` 파일의 경로는 코드가 포함된 JavaScript 파일이 아니라 사이트 원본을 기준으로 합니다. 서비스 워커는 `https://mdn.github.io/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/sw.js` 에 있습니다. 오리진은 `https://mdn.github.io`이므로 지정된 경로는 `/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/sw.js`여야 합니다. 이 예제를 자체 서버에서 호스팅하려면 이 경로를 적절히 변경해야 합니다. 다소 혼란스럽지만 보안상의 이유로 이 방식으로 작동해야 합니다.

#### 서비스 워커 설치

다음에 서비스 워커가 제어하는 페이지에 액세스할 때(예: 예제를 다시 로드할 때) 서비스 워커가 해당 페이지에 대해 설치되어 해당 페이지를 제어하기 시작합니다. 이 경우 서비스 워커에 대해 `install` 이벤트가 발생하므로 서비스 워커 자체 내부에서 설치에 응답하는 코드를 작성할 수 있습니다.

[sw.js](https://github.com/mdn/learning-area/blob/main/javascript/apis/client-side-storage/cache-sw/video-store-offline/sw.js) 파일(서비스 워커)의 예를 살펴봅시다. 설치 리스너가 `self`에 대해 등록되어 있는 것을 볼 수 있습니다. 이 `self` 키워드는 서비스 워커 파일 내부에서 서비스 워커의 전역 범위를 참조하는 방법입니다.

`install` 핸들러 내부에서는 이벤트 객체에서 사용할 수 있는 {{domxref("ExtendableEvent.waitUntil()")}} 메서드를 사용하여 내부의 프로미스가 성공적으로 이행될 때까지 브라우저가 서비스 워커의 설치를 완료해서는 안 된다는 신호를 보냅니다.

다음은 캐시 API가 실제로 작동하는 모습입니다. {{domxref("CacheStorage.open()")}} 메서드를 사용하여 응답을 저장할 수 있는 새 캐시 객체를 엽니다(IndexedDB 객체 저장소와 유사). 이 프로미스는 `video-store` 캐시를 나타내는 {{domxref("Cache")}} 객체로 이행됩니다. 그런 다음 {{domxref("Cache.addAll()")}} 메서드를 사용하여 일련의 에셋을 가져와서 해당 응답을 캐시에 추가합니다.

```js
self.addEventListener("install", (e) => {
  e.waitUntil(
    caches
      .open("video-store")
      .then((cache) =>
        cache.addAll([
          "/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/",
          "/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/index.html",
          "/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/index.js",
          "/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/style.css",
        ])
      )
  );
});
```

이제 설치가 완료되었습니다.

#### 추가 요청에 응답하기

서비스 워커가 HTML 페이지에 등록 및 설치되고 관련 에셋이 모두 캐시에 추가되었으므로 거의 모든 준비가 완료되었습니다. 남은 작업은 추가 네트워크 요청에 응답하는 코드를 작성하는 것뿐입니다.

이것이 `sw.js`의 두 번째 코드가 하는 일입니다. 서비스 워커 글로벌 범위에 다른 리스너를 추가하여 `fetch` 이벤트가 발생할 때 핸들러 함수를 실행합니다. 이는 브라우저가 서비스 워커가 등록된 디렉토리에 있는 에셋을 요청할 때마다 발생합니다.

핸들러 내부에서는 먼저 요청된 에셋의 URL을 기록합니다. 그런 다음 {{domxref("FetchEvent.respondWith()")}} 메서드를 사용하여 요청에 대한 사용자 정의 응답을 제공합니다.

Inside this block, we use {{domxref("CacheStorage.match()")}} to check whether a matching request (i.e. matches the URL) can be found in any cache. This promise fulfills with the matching response if a match is found, or `undefined` if it isn't.
이 블록 내부에서는 {{domxref("CacheStorage.match()")}} 를 사용하여 요청과 일치하는 요청(즉, URL과 일치하는 요청)을 캐시에서 찾을 수 있는지 확인합니다. 이 프로미스는 일치하는 요청이 발견되면 일치하는 응답으로 이행하고, 일치하지 않으면 `undefined`으로 이행합니다.

일치하는 항목이 발견되면 사용자 정의 응답으로 반환합니다. 그렇지 않은 경우 네트워크에서 응답을 [fetch()](/ko/docs/Web/API/fetch) 하여 대신 반환합니다.

```js
self.addEventListener("fetch", (e) => {
  console.log(e.request.url);
  e.respondWith(
    caches.match(e.request).then((response) => response || fetch(e.request))
  );
});
```

서비스 워커는 여기까지입니다. 서비스 워커로 할 수 있는 작업은 훨씬 더 많으며, 자세한 내용은 [서비스 워커 쿡북](https://github.com/mdn/serviceworker-cookbook) 을 참조하세요. 이 예제에 영감을 준 폴 킨란의 [웹 앱에 서비스 워커와 오프라인 추가하기](https://developers.google.com/codelabs/pwa-training/pwa03--going-offline#0) 문서에 감사드립니다.

#### 오프라인에서 예제 테스트하기

[서비스 워커 예제](https://mdn.github.io/learning-area/javascript/apis/client-side-storage/cache-sw/video-store-offline/) 를 테스트하려면 예제가 설치되었는지 확인하기 위해 몇 번 로드해야 합니다. 이 작업이 완료되면 테스트할 수 있습니다:

- 네트워크 플러그를 뽑거나 Wi-Fi를 끕니다.
- Firefox를 사용하는 경우 파일 > 오프라인으로 작업을 선택합니다.
- 개발 도구로 이동한 다음 애플리케이션 > 서비스 워커를 선택한 다음 Chrome을 사용하는 경우 오프라인 확인란을 선택합니다.

예제 페이지를 다시 새로 고치면 여전히 정상적으로 로드되는 것을 볼 수 있습니다. 페이지 자산은 캐시에, 동영상은 IndexedDB 데이터베이스에 저장되는 등 모든 것이 오프라인으로 저장됩니다.

## 요약

여기까지입니다. 클라이언트 측 스토리지 기술에 대한 요약이 도움이 되셨기를 바랍니다.

## 참고 항목

- [웹 스토리지 API](/ko/docs/Web/API/Web_Storage_API)
- [IndexedDB API](/ko/docs/Web/API/IndexedDB_API)
- [쿠키](/ko/docs/Web/HTTP/Cookies)
- [서비스 워커 API](/ko/docs/Web/API/Service_Worker_API)

{{PreviousMenu("Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs", "Learn/JavaScript/Client-side_web_APIs")}}
