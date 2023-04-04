---
title: Introducing JavaScript objects
slug: Learn/JavaScript/Objects
---

{{LearnSidebar}}

자바스크립트에서는 배열과 같은 핵심 자바스크립트 기능부터 자바스크립트 위에 구축된 브라우저 {{Glossary("API", "API")}} 에 이르기까지 대부분의 사물이 객체입니다. 심지어 자신만의 객체를 생성하여 관련 함수와 변수를 효율적인 패키지로 캡슐화하고 편리한 데이터 컨테이너 역할을 할 수도 있습니다. JavaScript의 객체 기반 특성은 언어에 대한 지식을 더 발전시키고자 하는 경우 이해하는 것이 중요하므로 이 모듈을 통해 도움을 드리고자 합니다. 여기서는 객체 이론과 구문을 자세히 설명한 다음 자신만의 객체를 만드는 방법을 살펴봅니다.

> **Callout:**
>
> #### 프론트엔드 웹 개발자가 되고 싶으신가요?
>
> 목표를 달성하는 데 필요한 모든 필수 정보가 포함된 과정을 준비했습니다.
>
> [**시작하기**](/ko/docs/Learn/Front-end_web_developer)

## 사전 필요 지식

이 모듈을 시작하기 전에 {{Glossary("HTML")}} 과 {{Glossary("CSS")}} 에 어느 정도 익숙해야 합니다. 자바스크립트를 시작하기 전에 [HTML 소개](/ko/docs/Learn/HTML/Introduction_to_HTML) 및 [CSS 소개](/ko/docs/Learn/CSS/First_steps) 모듈을 먼저 살펴보는 것이 좋습니다.

또한 JavaScript 객체를 자세히 살펴보기 전에 JavaScript 기본 사항을 어느 정도 숙지하고 있어야 합니다. 이 모듈을 시작하기 전에 [JavaScript 첫 단계](/ko/docs/Learn/JavaScript/First_steps) 와 [JavaScript 빌딩 블록](/ko/docs/Learn/JavaScript/Building_blocks) 을 살펴보세요.

> **참고:** 직접 파일을 만들 수 없는 컴퓨터/태블릿/기타 디바이스에서 작업하는 경우,  [JSBin](https://jsbin.com/) 이나 [Glitch](https://glitch.com/) 와 같은 온라인 코딩 프로그램에서 코드 예제(대부분)를 사용해 볼 수 있습니다.

## 가이드

- [객체 기초](/ko/docs/Learn/JavaScript/Objects/Basics)
  - : 자바스크립트 객체를 살펴보는 첫 번째 글에서는 기본적인 자바스크립트 객체 구문을 살펴보고, 강좌의 앞부분에서 이미 살펴본 자바스크립트 기능을 다시 살펴보면서 이미 다룬 많은 기능이 실제로는 객체라는 사실을 다시 한 번 강조할 것입니다.
- [객체 프로토타입](/ko/docs/Learn/JavaScript/Objects/Object_prototypes)
  - : 프로토타입은 자바스크립트 객체가 서로의 기능을 상속하는 메커니즘으로, 기존 객체 지향 프로그래밍 언어의 상속 메커니즘과는 다르게 작동합니다. 이 글에서는 프로토타입 체인이 어떻게 작동하는지 살펴봅니다.
- [객체 지향 프로그래밍](/ko/docs/Learn/JavaScript/Objects/Object-oriented_programming)
  - : 이 글에서는 "고전적" 객체 지향 프로그래밍의 몇 가지 기본 원칙을 설명하고, 자바스크립트의 프로토타입 모델과 어떻게 다른지 살펴봅니다.
- [자바스크립트의 클래스](/ko/docs/Learn/JavaScript/Objects/Classes_in_JavaScript)
  - : 자바스크립트는 "고전적인" 객체 지향 프로그램을 구현하고자 하는 사람들을 위해 몇 가지 기능을 제공하며, 이 글에서는 이러한 기능에 대해 설명합니다.
- [JSON 데이터로 작업하기](/ko/docs/Learn/JavaScript/Objects/JSON)
  - : JSON(JavaScript 객체 표기법)은 JavaScript 객체 구문을 기반으로 구조화된 데이터를 표현하는 표준 텍스트 기반 형식으로, 웹에서 데이터를 표현하고 전송할 때(즉, 일부 데이터를 서버에서 클라이언트로 전송하여 웹 페이지에 표시할 수 있도록 할 때) 일반적으로 사용됩니다. 자주 접하게 될 것이므로 이 글에서는 JSON을 구문 분석하여 그 안의 데이터 항목에 액세스하고 직접 JSON을 작성하는 등 JavaScript를 사용하여 JSON으로 작업하는 데 필요한 모든 것을 제공합니다.
- [객체 작성 실습](/ko/docs/Learn/JavaScript/Objects/Object_building_practice)
  - : 이전 글에서는 자바스크립트 객체 이론과 구문 세부 사항을 살펴봄으로써 탄탄한 기초를 다질 수 있었습니다. 이번 글에서는 색색의 튀어 오르는 공과 같은 재미있고 다채로운 결과물을 만들어내는 커스텀 자바스크립트 객체를 구축하는 연습을 더 해보겠습니다.

## 평가

- [바운싱 볼에 기능 추가하기 데모](/ko/docs/Learn/JavaScript/Objects/Adding_bouncing_balls_features)
  - : 이 평가에서는 이전 문서의 바운싱 볼 데모를 시작점으로 삼아 여기에 새롭고 흥미로운 기능을 추가해야 합니다.

## 참고 자료

- [자바스크립트 배우기](https://learnjavascript.online/)
  - : 웹 개발자 지망생을 위한 훌륭한 리소스 - 자동 평가에 따라 안내되는 짧은 강의와 대화형 테스트를 통해 대화형 환경에서 JavaScript를 배워보세요. 처음 40개 강의는 무료이며, 전체 강의는 소액의 일회성 결제로 이용할 수 있습니다.
볼