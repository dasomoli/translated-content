---
title: Asynchronous JavaScript
slug: Learn/JavaScript/Asynchronous
---

{{LearnSidebar}}

이 모듈에서는 비동기({{Glossary("asynchronous")}}) {{Glossary("JavaScript")}} 에 대해 살펴보고, 비동기 자바스크립트가 중요한 이유와 서버에서 리소스 가져오기와 같은 잠재적인 차단 작업을 효과적으로 처리하는 데 비동기 자바스크립트를 어떻게 사용할 수 있는지 알아봅니다.

> **Callout:**
>
> #### 프론트엔드 웹 개발자가 되고 싶으신가요?
>
> 목표를 달성하는 데 필요한 모든 필수 정보가 포함된 과정을 준비했습니다.
>
> [**시작하기**](/ko/docs/Learn/Front-end_web_developer)

## 전제 조건

비동기 자바스크립트는 상당히 고급 주제이므로 이 실습을 시도하기 전에 [자바스크립트 첫 단계](/ko/docs/Learn/JavaScript/First_steps) 와 [자바스크립트 빌딩 블록](/ko/docs/Learn/JavaScript/Building_blocks) 모듈을 먼저 살펴보는 것이 좋습니다.

> **참고:** 직접 파일을 만들 수 없는 컴퓨터/태블릿/기타 디바이스에서 작업하는 경우, [JSBin](https://jsbin.com/) 이나 [Glitch](https://glitch.com) 와 같은 온라인 코딩 프로그램에서 코드 예제(대부분)를 사용해 볼 수 있습니다.

## 가이드

- [비동기 자바스크립트 소개](/ko/docs/Learn/JavaScript/Asynchronous/Introducing)
  - : 이 글에서는 **동기** 및 **비동기** 프로그래밍에 대해 알아보고, 비동기 기술을 사용해야 하는 이유와 비동기 함수가 자바스크립트에서 역사적으로 구현된 방식과 관련된 문제점에 대해 알아봅니다.
- [프로미스 사용 방법](/ko/docs/Learn/JavaScript/Asynchronous/Promises)
  - : 여기서는 프로미스를 소개하고 프로미스 기반 API를 사용하는 방법을 보여드리겠습니다. 또한 `async` 및 `await` 키워드에 대해서도 소개합니다.
- [프로미스 기반 API 구현하기](/ko/docs/Learn/JavaScript/Asynchronous/Implementing_a_promise-based_API)
  - : 이 문서에서는 자체 프로미스 기반 API를 구현하는 방법을 간략하게 설명합니다.
- [워커 소개](/ko/docs/Learn/JavaScript/Asynchronous/Introducing_workers)
  - : 워커를 사용하면 메인 코드의 응답성을 유지하기 위해 별도의 스레드에서 특정 작업을 실행할 수 있습니다. 이 글에서는 워커를 사용하기 위해 장기 실행 동기 함수를 다시 작성해 보겠습니다.

## 평가

- [애니메이션 시퀀싱](/ko/docs/Learn/JavaScript/Asynchronous/Sequencing_animations)
  - : 평가에서는 프로미스를 사용하여 특정 시퀀스에서 일련의 애니메이션을 재생하도록 요청합니다.

## 참고 자료

- [비동기 프로그래밍](https://eloquentjavascript.net/11_async.html) 은 Marijn Haverbeke의 환상적인 [Eloquent JavaScript](https://eloquentjavascript.net/) 온라인 책에 수록되어 있습니다.
