---
title: Introduction to web APIs
slug: Learn/JavaScript/Client-side_web_APIs/Introduction
---

{{LearnSidebar}}{{NextMenu("Learn/JavaScript/Client-side_web_APIs/Manipulating_documents", "Learn/JavaScript/Client-side_web_APIs")}}

먼저 API란 무엇이고, 어떻게 작동하며, 코드에서 어떻게 사용하고, 어떻게 구조화되어 있는지 등 높은 수준에서 API를 살펴보는 것부터 시작하겠습니다. 또한 API의 다양한 주요 클래스가 무엇이며 어떤 용도로 사용되는지 살펴볼 것입니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
      기본적인 컴퓨터 활용 능력,
        <a href="/ko/docs/Learn/HTML">HTML</a> 및
        <a href="/ko/docs/Learn/CSS">CSS</a>에 대한 기본적인 이해, JavaScript 기초(
        <a href="/ko/docs/Learn/JavaScript/First_steps">첫 번째 단계</a>,
        <a href="/ko/docs/Learn/JavaScript/Building_blocks"
          >빌딩 블록</a
        >,
        <a href="/ko/docs/Learn/JavaScript/Objects"> JavaScript 객체</a> 참조).
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        API가 무엇인지, 무엇을 할 수 있는지, 코드에서 API를 어떻게 사용할 수 있는지 알아보세요.
      </td>
    </tr>
  </tbody>
</table>

## API란 무엇인가요?

API(애플리케이션 프로그래밍 인터페이스)는 개발자가 복잡한 기능을 더 쉽게 만들 수 있도록 프로그래밍 언어로 제공되는 구조입니다. API는 복잡한 코드를 추상화하여 대신 사용할 수 있는 더 쉬운 구문을 제공합니다.

실제 예를 들어 집, 아파트 또는 기타 주거지의 전기 공급을 생각해 보세요. 집에서 가전제품을 사용하려면 플러그 소켓에 플러그를 꽂으면 작동합니다. 전원 공급 장치에 직접 연결하는 것은 매우 비효율적이며 전기 기술자가 아니라면 시도하기 어렵고 위험할 수 있습니다.

![Two multi-plug holders are plugged into two different plug outlet sockets. Each multi-plug holder has a plug slot on it's top and to it's front side. Two plugs are plugged into each multi-plug holder.](plug-socket.png)

_Image source: [Overloaded plug socket](https://www.flickr.com/photos/easy-pics/9518184890/in/photostream/lightbox/) by [The Clear Communication People](https://www.flickr.com/photos/easy-pics/), on Flickr._

마찬가지로 3D 그래픽을 프로그래밍하려면 컴퓨터의 GPU나 기타 그래픽 기능을 직접 제어하는 저수준 코드(예: C 또는 C++)를 직접 작성하는 것보다 JavaScript나 Python과 같은 상위 언어로 작성된 API를 사용하는 것이 훨씬 더 쉽습니다.

> **참고:** 자세한 설명은 [API 용어집 항목](/ko/docs/Glossary/API) 을 참조하세요.

### 클라이언트 측 JavaScript의 API

특히 클라이언트 측 자바스크립트에는 자바스크립트 언어 자체의 일부가 아니라 핵심 자바스크립트 언어 위에 구축되어 자바스크립트 코드에서 사용할 수 있는 추가 기능을 제공하는 많은 API가 있습니다. 일반적으로 두 가지 범주로 나뉩니다:

- **브라우저 API** 는 웹 브라우저에 내장되어 있으며 브라우저와 주변 컴퓨터 환경의 데이터를 노출하고 이를 통해 유용하고 복잡한 작업을 수행할 수 있습니다. 예를 들어 [웹 오디오 API](/ko/docs/Web/API/Web_Audio_API) 는 브라우저에서 오디오 트랙을 가져오고, 볼륨을 변경하고, 효과를 적용하는 등 오디오를 조작하기 위한 자바스크립트 구성을 제공합니다. 백그라운드에서 브라우저는 실제로 복잡한 하위 수준 코드(예: C++ 또는 Rust)를 사용하여 실제 오디오 처리를 수행합니다. 하지만 이 복잡성은 API를 통해 추상화됩니다.
- **타사 API** 는 기본적으로 브라우저에 내장되어 있지 않으므로 일반적으로 웹 어딘가에서 해당 코드와 정보를 검색해야 합니다. 예를 들어, [트위터 API](https://developer.twitter.com/en/docs) 를 사용하면 웹사이트에 내 최신 트윗을 표시하는 등의 작업을 수행할 수 있습니다. 이 API는 트위터 서비스를 쿼리하고 특정 정보를 반환하는 데 사용할 수 있는 특수한 구조체 집합을 제공합니다.

![A screenshot of the browser with the home page of firefox browser open. There are APIs built into the browser by default. Third party APIs are not built into the browser by default. Their code and information has to be retrieved from somewhere on the web to utilize them.](browser.png)

### 자바스크립트, API 및 기타 자바스크립트 도구 간의 관계

지금까지 클라이언트 측 JavaScript API가 무엇인지, 그리고 JavaScript 언어와의 관계에 대해 설명했습니다. 더 명확하게 이해하기 위해 다시 한 번 요약하고 다른 JavaScript 도구가 어디에 적합한지 언급해 보겠습니다:

- JavaScript - 웹 페이지/앱에서 기능을 구현할 수 있도록 브라우저에 내장된 고급 스크립팅 언어입니다. JavaScript는 [Node](/ko/docs/Learn/Server-side/Express_Nodejs/Introduction)와 같은 다른 프로그래밍 환경에서도 사용할 수 있습니다.
- 브라우저 API — 브라우저에 내장된 구조체로, JavaScript 언어 위에 위치하며 기능을 더 쉽게 구현할 수 있도록 해줍니다.
- 타사 API — 타사 플랫폼(예: 트위터, 페이스북)에 내장된 구조체로, 내 웹 페이지에서 해당 플랫폼의 일부 기능을 사용할 수 있습니다(예: 내 웹 페이지에 내 최신 트윗 표시).
- 자바스크립트 라이브러리 — 일반적으로 웹 페이지에 첨부하여 일반적인 기능의 작성 속도를 높이거나 활성화할 수 있는 [사용자 지정 함수](/ko/docs/Learn/JavaScript/Building_blocks/Functions#custom_functions) 가 포함된 하나 이상의 자바스크립트 파일입니다. 예를 들면 jQuery, Mootools, React 등이 있습니다.
- 자바스크립트 프레임워크 —라이브러리에서 한 단계 더 발전한 자바스크립트 프레임워크(예: Angular 및 Ember)는 HTML, CSS, 자바스크립트 및 기타 기술을 패키지로 구성하여 설치한 다음 전체 웹 애플리케이션을 처음부터 작성하는 데 사용하는 경우가 대부분입니다. 라이브러리와 프레임워크의 주요 차이점은 "제어의 역전"입니다. 라이브러리에서 메서드를 호출할 때 개발자가 제어권을 갖습니다. 프레임워크를 사용하면 제어권이 반전되어 프레임워크가 개발자의 코드를 호출합니다.

## API는 무엇을 할 수 있나요?

최신 브라우저에는 코드에서 다양한 작업을 수행할 수 있는 수많은 API가 있습니다. [MDN API 색인 페이지](/ko/docs/Web/API) 를 살펴보면 이를 확인할 수 있습니다.

### 일반적인 브라우저 API

특히 이 모듈에서 더 자세히 다루게 될 가장 일반적인 브라우저 API 카테고리는 다음과 같습니다:

- 브라우저에 로드된 **문서를 조작하기 위한 API**. 가장 눈에 띄는 예는 [DOM (Document Object Model) API](/ko/docs/Web/API/Document_Object_Model) 로, HTML을 생성, 제거, 변경하고 페이지에 새 스타일을 동적으로 적용하는 등 HTML과 CSS를 조작할 수 있습니다. 예를 들어 페이지에 팝업 창이 나타나거나 새로운 콘텐츠가 표시될 때마다 DOM이 작동합니다. [문서 조작하기](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents) 에서 이러한 유형의 API에 대해 자세히 알아보세요
- **서버에서 데이터를 가져와** 웹페이지의 작은 섹션을 자체적으로 업데이트하는 **API**는 매우 일반적으로 사용됩니다. 주식 목록이나 이용 가능한 새 기사 목록만 업데이트해야 하는 경우 서버에서 전체 페이지를 다시 로드할 필요 없이 즉시 업데이트하면 사이트나 앱의 반응 속도가 훨씬 빨라지고 "빠른" 느낌을 줄 수 있습니다. 이를 위해 사용되는 주요 API는 [Fetch API](/ko/docs/Web/API/Fetch_API) 이지만, 이전 코드에서는 여전히 [`XMLHttpRequest`](/ko/docs/Web/API/XMLHttpRequest) API를 사용할 수 있습니다. 이 기술을 설명하는 **Ajax** 라는 용어를 접할 수도 있습니다. 이러한 API에 대한 자세한 내용은 [서버에서 데이터 가져오기](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data) 에서 확인하세요.
- **그래픽을 그리고 조작하기 위한 API** 는 브라우저에서 광범위하게 지원되며, 가장 많이 사용되는 API는 HTML {{htmlelement("canvas")}} 요소에 포함된 픽셀 데이터를 프로그래밍 방식으로 업데이트하여 2D 및 3D 장면을 만들 수 있는 [Canvas](/ko/docs/Web/API/Canvas_API) 와 [WebGL](/ko/docs/Web/API/WebGL_API) 입니다. 예를 들어 직사각형이나 원과 같은 도형을 그리거나 이미지를 캔버스로 가져온 다음 캔버스 API를 사용하여 세피아나 회색조와 같은 필터를 적용하거나 WebGL을 사용하여 조명과 텍스처가 포함된 복잡한 3D 장면을 만들 수 있습니다. 이러한 API는 애니메이션 루프를 생성하는 API(예: {{domxref("window.requestAnimationFrame()")}}) 등과 결합하여 만화나 게임과 같이 지속적으로 업데이트되는 장면을 만드는 데 사용됩니다.
- **[오디오 및 비디오 API](/ko/docs/Web/Guide/Audio_and_video_delivery)**(예: {{domxref("HTMLMediaElement")}}, [웹 오디오 API](/ko/docs/Web/API/Web_Audio_API), [WebRTC](/ko/docs/Web/API/WebRTC_API))를 사용하면 오디오 및 비디오 재생을 위한 사용자 지정 UI 컨트롤 생성, 동영상과 함께 캡션 및 자막과 같은 텍스트 트랙 표시, 웹 카메라에서 동영상을 가져와 캔버스(위 참조)를 통해 조작하거나 웹 회의에서 다른 사람의 컴퓨터에 표시, 오디오 트랙에 효과(게인, 왜곡, 패닝 등) 추가 등 멀티미디어로 정말 흥미로운 작업을 할 수 있습니다.
- **장치 API** 를 사용하면 장치 하드웨어와 상호 작용할 수 있습니다(예: [지리적 위치 API](/ko/docs/Web/API/Geolocation_API) 를 사용하여 사용자의 위치를 찾기 위해 장치 GPS에 액세스).
- **클라이언트 측 스토리지 API** 를 사용하면 클라이언트 측에 데이터를 저장할 수 있으므로 페이지 로드 사이에 상태를 저장하고 디바이스가 오프라인 상태에서도 작동하는 앱을 만들 수 있습니다. [웹 스토리지 API](/ko/docs/Web/API/Web_Storage_API) 를 사용한 간단한 이름/값 저장, [IndexedDB API](/ko/docs/Web/API/IndexedDB_API) 를 사용한 보다 복잡한 데이터베이스 저장 등 여러 가지 옵션을 사용할 수 있습니다.

### 일반적인 타사 API

타사 API는 매우 다양한 종류가 있으며, 조만간 사용할 가능성이 높은 몇 가지 인기 있는 API는 다음과 같습니다:

- [트위터 API](https://developer.twitter.com/en/docs) 는 웹사이트에 최신 트윗을 표시하는 등의 작업을 수행할 수 있게 해줍니다.
- 웹 페이지에서 지도로 다양한 작업을 할 수 있는 [Mapquest](https://developer.mapquest.com/) 및 [Google 지도 API](https://developers.google.com/maps/) 와 같은 지도 API.
- Facebook 로그인으로 앱 로그인 제공, 인앱 결제 수락, 타겟팅 광고 캠페인 실행 등 Facebook 생태계의 다양한 부분을 사용하여 앱에 혜택을 줄 수 있는 [Facebook API 제품군](https://developers.facebook.com/docs/) 입니다.
- 봇을 지원할 뿐만 아니라 웹사이트에 텔레그램 채널의 콘텐츠를 임베드할 수 있는 [텔레그램 API](https://core.telegram.org/api).
- 사이트에 YouTube 동영상을 임베드하고, YouTube를 검색하고, 재생목록을 만드는 등의 작업을 할 수 있는 [YouTube API](https://developers.google.com/youtube/).
- Pinterest 보드와 핀을 관리하여 웹사이트에 포함할 수 있는 도구를 제공하는 [Pinterest API](https://developers.pinterest.com/).
- 앱에 음성 및 영상 통화 기능을 구축하고 앱에서 SMS/MMS를 전송하는 등의 기능을 구축하기 위한 프레임워크를 제공하는 [Twilio API](https://www.twilio.com/).
- 마스토돈 소셜 네트워크의 기능을 프로그래밍 방식으로 조작할 수 있는 [마스토돈 API](https://docs.joinmastodon.org/api/).

> **참고:** [프로그래밍 가능한 웹 API 디렉토리](https://www.programmableweb.com/category/all/apis) 에서 더 많은 타사 API에 대한 정보를 찾을 수 있습니다.

## API는 어떻게 작동하나요?

자바스크립트 API마다 작동 방식은 조금씩 다르지만 일반적으로 공통된 기능과 비슷한 주제를 가지고 있습니다.

### 객체를 기반으로 합니다.

코드는 하나 이상의 [JavaScript 객체](/ko/docs/Learn/JavaScript/Objects) 를 사용하여 API와 상호 작용하며, 이 객체는 API가 사용하는 데이터(객체 속성에 포함됨)와 API가 제공하는 기능(객체 메서드에 포함됨)을 담는 컨테이너 역할을 합니다.

> **참고:** 객체의 작동 방식에 익숙하지 않은 경우 계속하기 전에 [JavaScript 객체](/ko/docs/Learn/JavaScript/Objects) 모듈로 돌아가서 작업해야 합니다.

웹 오디오 API의 예로 돌아가서, 이 API는 여러 개의 객체로 구성된 상당히 복잡한 API입니다. 가장 눈에 띄는 것은 다음과 같습니다:

- 브라우저 내에서 재생되는 오디오를 조작하는 데 사용할 수 있는 [audio graph](/ko/docs/Web/API/Web_Audio_API/Basic_concepts_behind_Web_Audio_API#audio_graphs) 를 나타내며, 해당 오디오를 조작하는 데 사용할 수 있는 여러 메서드와 프로퍼티가 있는 {{domxref("AudioContext")}}.
- 오디오 컨텍스트 내에서 재생하고 조작하려는 사운드가 포함된 {{htmlelement("audio")}} 요소를 나타내는 {{domxref("MediaElementAudioSourceNode")}}.
- 오디오의 대상, 즉 실제로 오디오를 출력할 컴퓨터의 장치(일반적으로 스피커나 헤드폰)를 나타내는 {{domxref("AudioDestinationNode")}}.

그렇다면 이러한 객체들은 어떻게 상호작용할까요? [간단한 웹 오디오 예시](https://github.com/mdn/learning-area/blob/main/javascript/apis/introduction/web-audio/index.html) ([라이브 보기](https://mdn.github.io/learning-area/javascript/apis/introduction/web-audio/))를 보면 먼저 다음 HTML을 볼 수 있습니다:

```html
<audio src="outfoxing.mp3"></audio>

<button class="paused">Play</button>
<br />
<input type="range" min="0" max="1" step="0.01" value="1" class="volume" />
```

우선 페이지에 MP3를 임베드하는 `<audio>` 요소를 포함합니다. 기본 브라우저 컨트롤은 포함하지 않습니다. 다음으로 음악을 재생하고 중지하는 데 사용할 {{htmlelement("button")}}과 트랙이 재생되는 동안 볼륨을 조정하는 데 사용할 {{htmlelement("input")}} 요소를 포함시킵니다.

이제 이 예제의 자바스크립트를 살펴봅시다.

먼저 트랙을 조작할 `AudioContext` 인스턴스를 생성합니다:

```js
const AudioContext = window.AudioContext || window.webkitAudioContext;
const audioCtx = new AudioContext();
```

다음으로, `<audio>`, `<button>`, `<input>` 요소에 대한 참조를 저장하는 상수를 생성하고 {{domxref("AudioContext.createMediaElementSource()")}} 메서드를 사용하여 오디오의 소스를 나타내는 `MediaElementAudioSourceNode`를 생성합니다 - `<audio>` 요소가 재생될 곳입니다:

```js
const audioElement = document.querySelector('audio');
const playBtn = document.querySelector('button');
const volumeSlider = document.querySelector('.volume');

const audioSource = audioCtx.createMediaElementSource(audioElement);
```

다음으로 버튼을 눌렀을 때 재생과 일시정지 사이를 전환하고 노래 재생이 끝나면 디스플레이를 처음으로 리셋하는 두 가지 이벤트 핸들러가 포함되어 있습니다:

```js
// play/pause audio
playBtn.addEventListener('click', () => {
  // check if context is in suspended state (autoplay policy)
  if (audioCtx.state === 'suspended') {
     audioCtx.resume();
  }

  // if track is stopped, play it
  if (playBtn.getAttribute('class') === 'paused') {
    audioElement.play();
    playBtn.setAttribute('class', 'playing');
    playBtn.textContent = 'Pause'
    // if track is playing, stop it
} else if (playBtn.getAttribute('class') === 'playing') {
    audioElement.pause();
    playBtn.setAttribute('class', 'paused');
    playBtn.textContent = 'Play';
  }
});

// if track ends
audioElement.addEventListener('ended', () => {
  playBtn.setAttribute('class', 'paused');
  playBtn.textContent = 'Play'
});
```

> **참고:** 트랙을 재생하고 일시 정지하는 데 사용되는 `play()` 및 `pause()` 메서드가 웹 오디오 API의 일부가 아니라 서로 다르지만 밀접한 관련이 있는 {{domxref("HTMLMediaElement")}} API의 일부라는 것을 눈치채신 분들도 계실 것입니다

다음으로, 오디오를 통해 공급되는 오디오의 볼륨을 조정하는 데 사용할 수 있는 {{domxref("BaseAudioContext/createGain", "AudioContext.createGain()")}} 메서드를 사용하여 {{domxref("GainNode")}} 객체를 생성하고 슬라이더 값이 변경될 때마다 오디오 그래프의 게인(볼륨) 값을 변경하는 또 다른 이벤트 핸들러를 생성합니다:

```js
// volume
const gainNode = audioCtx.createGain();

volumeSlider.addEventListener('input', () => {
  gainNode.gain.value = volumeSlider.value;
});
```

이를 작동시키기 위해 마지막으로 해야 할 일은 오디오 그래프의 여러 노드를 연결하는 것으로, 모든 노드 유형에서 사용할 수 있는 {{domxref("AudioNode.connect()")}} 메서드를 사용하여 수행합니다:

```js
audioSource.connect(gainNode).connect(audioCtx.destination);
```

오디오가 소스에서 시작되면 게인 노드에 연결되어 오디오의 볼륨을 조절할 수 있습니다. 그런 다음 게인 노드가 대상 노드에 연결되어 컴퓨터에서 사운드를 재생할 수 있습니다({{domxref("BaseAudioContext/destination", "AudioContext.destination")}} 속성은 컴퓨터 하드웨어(예: 스피커)에서 사용할 수 있는 기본 {{domxref("AudioDestinationNode")}} 를 나타냅니다).

### 알아볼 수 있는 진입점이 있습니다.

API를 사용할 때는 API의 진입점이 어디에 있는지 알아야 합니다. 웹 오디오 API에서 이것은 매우 간단합니다. 오디오 조작을 할 때 사용해야 하는 {{domxref("AudioContext")}} 객체입니다.

문서 객체 모델(DOM) API도 진입점이 간단합니다. 예를 들어, 해당 기능은 {{domxref("Document")}} 객체 또는 어떤 식으로든 영향을 주고자 하는 HTML 요소의 인스턴스에 매달려 있는 경우가 많습니다:

```js
const em = document.createElement('em'); // create a new em element
const para = document.querySelector('p'); // reference an existing p element
em.textContent = 'Hello there!'; // give em some text content
para.appendChild(em); // embed em inside para
```

[캔버스 API](/ko/docs/Web/API/Canvas_API) 는 또한 사물을 조작하는 데 사용할 컨텍스트 객체를 가져오는 데 의존하지만, 이 경우에는 오디오 컨텍스트가 아닌 그래픽 컨텍스트입니다. 컨텍스트 객체는 그리려는 {{htmlelement("canvas")}} 요소에 대한 참조를 가져온 다음 해당 {{domxref("HTMLCanvasElement.getContext()")}} 메서드를 호출하여 생성됩니다:

```js
const canvas = document.querySelector('canvas');
const ctx = canvas.getContext('2d');
```

그런 다음 캔버스에 하고 싶은 작업은 컨텍스트 객체(예: {{domxref("CanvasRenderingContext2D")}} 의 인스턴스)의 프로퍼티와 메서드를 호출하여 수행합니다:

```js
Ball.prototype.draw = function() {
  ctx.beginPath();
  ctx.fillStyle = this.color;
  ctx.arc(this.x, this.y, this.size, 0, 2 * Math.PI);
  ctx.fill();
};
```

> **참고:** [바운싱볼 데모](https://github.com/mdn/learning-area/blob/main/javascript/apis/introduction/bouncing-balls.html) 에서 이 코드가 실제로 작동하는 모습을 확인할 수 있습니다([실시간으로 실행](https://mdn.github.io/learning-area/javascript/apis/introduction/bouncing-balls.html) 되는 모습도 참조하세요).

### 상태 변경을 처리하기 위해 이벤트를 사용하는 경우가 많습니다.

이벤트가 무엇이며 코드에서 어떻게 사용되는지 자세히 살펴보는 [이벤트 소개](/ko/docs/Learn/JavaScript/Building_blocks/Events) 글에서 이미 이벤트에 대해 설명했습니다. 클라이언트 측 웹 API 이벤트의 작동 방식에 익숙하지 않다면 계속하기 전에 이 글을 먼저 읽어보시기 바랍니다.

일부 웹 API에는 이벤트가 없지만 대부분은 최소한 몇 가지 이벤트를 포함합니다. 이벤트가 발생할 때 함수를 실행할 수 있는 핸들러 속성은 일반적으로 참조 자료에 별도의 "이벤트 핸들러" 섹션에 나열되어 있습니다.

위의 웹 오디오 API 예제에서 이미 여러 이벤트 핸들러가 사용 중인 것을 보았습니다:

```js
// play/pause audio
playBtn.addEventListener('click', () => {
  // check if context is in suspended state (autoplay policy)
  if (audioCtx.state === 'suspended') {
     audioCtx.resume();
  }

  // if track is stopped, play it
  if (playBtn.getAttribute('class') === 'paused') {
    audioElement.play();
    playBtn.setAttribute('class', 'playing');
    playBtn.textContent = 'Pause'
    // if track is playing, stop it
} else if (playBtn.getAttribute('class') === 'playing') {
    audioElement.pause();
    playBtn.setAttribute('class', 'paused');
    playBtn.textContent = 'Play';
  }
});

// if track ends
audioElement.addEventListener('ended', () => {
  playBtn.setAttribute('class', 'paused');
  playBtn.textContent = 'Play'
});
```

### 적절한 경우 추가 보안 메커니즘이 있습니다.

WebAPI 기능에는 JavaScript 및 기타 웹 기술과 동일한 보안 고려 사항(예: [동일 출처 정책](/ko/docs/Web/Security/Same-origin_policy))이 적용되지만, 경우에 따라 추가 보안 메커니즘이 적용되기도 합니다. 예를 들어, 일부 최신 WebAPI는 잠재적으로 민감한 데이터를 전송하기 때문에 HTTPS를 통해 제공되는 페이지에서만 작동합니다(예: [서비스 워커](/ko/docs/Web/API/Service_Worker_API) 및 [푸시](/ko/docs/Web/API/Push_API)).

또한 일부 WebAPI는 코드에서 호출이 이루어지면 사용자에게 사용 권한을 요청합니다. 예를 들어 [알림 API](/ko/docs/Web/API/Notifications_API) 는 팝업 대화 상자를 사용하여 권한을 요청합니다:

![A screenshot of the notifications pop-up dialog provided by the Notifications API of the browser. 'mdn.github.io' website is asking for permissions to push notifications to the user-agent with an X to close the dialog and drop-down menu of options with 'always receive notifications' selected by default.](notification-permission.png)

웹 오디오 및 {{domxref("HTMLMediaElement")}} API에는 [자동 재생 정책](/ko/docs/Web/API/Web_Audio_API/Best_practices#autoplay_policy) 이라는 보안 메커니즘이 적용되며, 이는 기본적으로 페이지가 로드될 때 오디오를 자동으로 재생할 수 없으므로 사용자가 버튼과 같은 컨트롤을 통해 오디오 재생을 시작하도록 허용해야 한다는 의미입니다. 이는 오디오 자동 재생이 일반적으로 매우 성가신 일이기 때문에 사용자에게 오디오 자동 재생을 허용해서는 안 되기 때문입니다.

> **참고:** 브라우저의 보안 수준에 따라 웹 서버에서 실행하는 대신 브라우저에서 로컬 예제 파일을 로드하는 경우 이러한 보안 메커니즘으로 인해 예제가 로컬에서 작동하지 않을 수도 있습니다. 이 글을 쓰는 시점에서 웹 오디오 API 예제는 Google 크롬에서 로컬로 작동하지 않았으며, GitHub에 업로드해야만 작동했습니다.

## 요약

이쯤 되면 API가 무엇인지, 어떻게 작동하는지, 자바스크립트 코드에서 API로 무엇을 할 수 있는지 잘 알고 있을 것입니다. 이제 특정 API로 실제로 재미있는 작업을 시작하고 싶으실 텐데요, 그럼 시작해 보겠습니다! 다음에는 문서 객체 모델(DOM)로 문서를 조작하는 방법을 살펴보겠습니다.

{{NextMenu("Learn/JavaScript/Client-side_web_APIs/Manipulating_documents", "Learn/JavaScript/Client-side_web_APIs")}}
