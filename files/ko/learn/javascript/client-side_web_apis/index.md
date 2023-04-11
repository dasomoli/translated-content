---
title: Client-side web APIs
slug: Learn/JavaScript/Client-side_web_APIs
---

{{LearnSidebar}}

웹 사이트나 애플리케이션을 위한 클라이언트 측 JavaScript를 작성할 때 **애플리케이션 프로그래밍 인터페이스**(**API**)를 자주 접하게 됩니다. API는 사이트가 실행 중인 브라우저와 운영 체제의 다양한 측면을 조작하거나 다른 웹사이트나 서비스의 데이터를 조작하기 위한 프로그래밍 기능입니다. 이 모듈에서는 API가 무엇인지, 개발 작업에서 자주 접하게 될 가장 일반적인 API를 사용하는 방법을 살펴봅니다.

> **Callout:**
>
> #### 프론트엔드 웹 개발자가 되고 싶으신가요?
>
> 목표를 달성하는 데 필요한 모든 필수 정보가 포함된 과정을 준비했습니다.
>
> [**시작하기**](/ko/docs/Learn/Front-end_web_developer)

## 전제 조건

이 모듈을 최대한 활용하려면 시리즈의 이전 JavaScript 모듈([첫 번째 단계](/ko/docs/Learn/JavaScript/First_steps), [빌딩 블록](/ko/docs/Learn/JavaScript/Building_blocks) 및 [JavaScript 객체](/ko/docs/Learn/JavaScript/Objects))을 모두 학습한 상태여야 합니다. 이러한 모듈은 일반적으로 간단한 API 사용을 포함하며, 이러한 모듈 없이는 클라이언트 측 JavaScript 예제를 작성하기 어려운 경우가 많기 때문입니다. 이 튜토리얼에서는 여러분이 핵심 JavaScript 언어에 대해 잘 알고 있다고 가정하고 일반적인 웹 API를 좀 더 자세히 살펴보겠습니다.

[HTML](/ko/docs/Learn/HTML)과 [CSS](/ko/docs/Learn/CSS)에 대한 기본 지식도 유용할 것입니다.

> **참고:** 직접 파일을 생성할 수 없는 기기에서 작업하는 경우 [JSBin](https://jsbin.com/) 이나 [Glitch](https://glitch.com/) 와 같은 온라인 코딩 프로그램에서 코드 예제의 대부분을 사용해 볼 수 있습니다.

## 가이드

- [웹 API 소개](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Introduction)
  - : 먼저 API란 무엇이고, 어떻게 작동하며, 코드에서 어떻게 사용하고, 어떻게 구조화되어 있는지 등 높은 수준에서 API를 살펴보는 것부터 시작하겠습니다. 또한 API의 다양한 주요 클래스가 무엇이며 어떤 용도로 사용되는지 살펴볼 것입니다.
- [문서 조작하기](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents)
  - : 웹 페이지와 앱을 작성할 때 가장 흔히 하는 일 중 하나는 어떤 식으로든 웹 문서를 조작하는 것입니다. 이는 일반적으로 {{domxref("Document")}} 객체를 많이 사용하는 HTML 및 스타일링 정보를 제어하기 위한 API 집합인 문서 객체 모델(DOM)을 사용하여 수행됩니다. 이 글에서는 DOM을 사용하는 방법과 환경을 흥미로운 방식으로 변경할 수 있는 몇 가지 흥미로운 API를 자세히 살펴봅니다.
- [서버에서 데이터 가져오기](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data)
  - : 최신 웹사이트와 애플리케이션에서 매우 일반적인 또 다른 작업은 완전히 새로운 페이지를 로드하지 않고도 서버에서 개별 데이터 항목을 검색하여 웹페이지의 섹션을 업데이트하는 것입니다. 이 사소해 보이는 세부 사항은 사이트의 성능과 동작에 큰 영향을 미칩니다. 이 글에서는 이 개념에 대해 설명하고 이를 가능하게 하는 기술인 {{domxref("XMLHttpRequest")}}와 [Fetch API](/ko/docs/Web/API/Fetch_API) 에 대해 살펴보겠습니다.
- [서드파티 API](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Third_party_APIs)
  - : 지금까지 살펴본 API는 브라우저에 내장되어 있지만 모든 API가 내장되어 있는 것은 아닙니다. Google 지도, 트위터, 페이스북, 페이팔 등 많은 대형 웹사이트와 서비스는 개발자가 데이터(예: 블로그에 트위터 스트림 표시) 또는 서비스(예: 사이트에 맞춤 Google 지도 표시 또는 페이스북 로그인을 사용하여 사용자 로그인)를 사용할 수 있도록 API를 제공합니다. 이 문서에서는 브라우저 API와 타사 API의 차이점을 살펴보고 후자의 일반적인 사용법을 소개합니다.
- [그래픽 그리기](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Drawing_graphics)
  - : 브라우저에는 확장 가능한 벡터 그래픽([SVG](/ko/docs/Web/SVG)) 언어부터 HTML {{htmlelement("canvas")}} 요소에 그리기 위한 API까지 매우 강력한 그래픽 프로그래밍 도구가 포함되어 있습니다([The Canvas API](/ko/docs/Web/API/Canvas_API) 및 [WebGL](/ko/docs/Web/API/WebGL_API) 참조). 이 문서에서는 캔버스 API에 대한 소개와 더 자세히 알아볼 수 있는 추가 리소스를 제공합니다.
- [비디오 및 오디오 API](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Video_and_audio_APIs)
  - : HTML에는 문서에 리치 미디어를 삽입하기 위한 요소인 {{htmlelement("video")}} 및 {{htmlelement("audio")}} 가 포함되어 있으며, 이 요소에는 재생, 검색 등을 제어하기 위한 자체 API가 함께 제공됩니다. 이 문서에서는 사용자 정의 재생 컨트롤을 만드는 것과 같은 일반적인 작업을 수행하는 방법을 보여줍니다.
- [클라이언트 측 저장소](/ko/docs/Learn/JavaScript/Client-side_web_APIs/Client-side_storage)
  - : 최신 웹 브라우저에는 웹 사이트와 관련된 데이터를 저장하고 필요할 때 검색하여 데이터를 장기간 보존하고 사이트를 오프라인으로 저장하는 등의 작업을 수행할 수 있는 여러 가지 기술이 탑재되어 있습니다. 이 문서에서는 이러한 기술이 어떻게 작동하는지에 대한 기본 사항을 설명합니다.
