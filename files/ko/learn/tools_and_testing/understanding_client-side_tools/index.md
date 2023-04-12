---
title: Understanding client-side web development tools
slug: Learn/Tools_and_testing/Understanding_client-side_tools
---

{{LearnSidebar}}

클라이언트 측 도구는 어렵게 느껴질 수 있지만, 이 일련의 글에서는 가장 일반적인 클라이언트 측 도구 유형의 목적을 설명하고, 함께 체인화할 수 있는 도구, 패키지 관리자를 사용하여 설치하는 방법, 명령줄을 사용하여 도구를 제어하는 방법을 설명하고자 합니다. 마지막으로 생산성을 높이는 방법을 보여주는 완전한 도구 체인 예제를 제공함으로써 마무리합니다.

## 전제 조건

여기에 설명된 도구를 사용하기 전에 먼저 핵심 [HTML](/ko/docs/Learn/HTML), [CSS](/ko/docs/Learn/CSS) 및 [JavaScript](/ko/docs/Learn/JavaScript) 언어의 기초를 익혀야 합니다.

> **Callout:**
>
> #### 프론트엔드 웹 개발자가 되고 싶으신가요?
>
> 목표를 달성하는 데 필요한 모든 필수 정보를 담은 강좌를 준비했습니다.
>
> [**시작하기**](/ko/docs/Learn/Front-end_web_developer)

## 가이드

- [1. 클라이언트 측 도구 개요](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Overview)
  - : 이 글에서는 최신 웹 도구에 대한 개요, 사용 가능한 도구의 종류, 웹 앱 개발 수명 주기에서 해당 도구를 만날 수 있는 위치, 개별 도구에 대한 도움말을 찾는 방법에 대해 설명합니다.
- [2. 명령줄 단기 속성 과정](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line)
  - : 개발 과정에서 터미널(또는 "명령줄")에서 몇 가지 명령을 실행해야 할 때가 있을 것입니다. 이 글에서는 터미널에 대한 소개, 터미널에 입력해야 하는 필수 명령어, 명령어를 서로 연결하는 방법, 자체 명령줄 인터페이스(CLI) 도구를 추가하는 방법에 대해 설명합니다.
- [3. 패키지 관리 기초](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management)
  - : 이 글에서는 프로젝트 도구 종속성을 설치하고, 최신 상태로 유지하는 등 프로젝트에서 패키지 관리자를 사용하는 방법을 이해하기 위해 패키지 관리자를 자세히 살펴봅니다.
- [4. 완전한 툴체인 소개](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Introducing_complete_toolchain)
  - : 시리즈의 마지막 두 글에서는 샘플 사례 연구 툴체인을 구축하는 과정을 안내하여 툴링 지식을 탄탄하게 다질 것입니다. 합리적인 개발 환경을 설정하고 변환 도구를 배치하는 것부터 넷플라이에 앱을 실제로 배포하는 것까지 모두 다룰 것입니다. 이 글에서는 사례 연구를 소개하고, 개발 환경을 설정하고, 코드 변환 도구를 설정합니다.
- [5. 앱 배포하기](/ko/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Deployment)
  - : 시리즈의 마지막 글에서는 이전 글에서 구축한 예제 툴체인에 샘플 앱을 배포할 수 있도록 추가합니다. 코드를 GitHub에 푸시하고, Netlify를 사용하여 배포하고, 프로세스에 간단한 테스트를 추가하는 방법까지 보여드리겠습니다.
