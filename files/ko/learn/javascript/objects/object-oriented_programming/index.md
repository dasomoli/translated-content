---
title: Object-oriented programming
slug: Learn/JavaScript/Objects/Object-oriented_programming
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Objects/Object_prototypes", "Learn/JavaScript/Objects/Classes_in_JavaScript", "Learn/JavaScript/Objects")}}

객체 지향 프로그래밍(OOP)은 Java와 C++를 비롯한 많은 프로그래밍 언어의 기본이 되는 프로그래밍 패러다임입니다. 이 글에서는 OOP의 기본 개념에 대한 개요를 제공합니다. **클래스와 인스턴스**, **상속**, **캡슐화** 라는 세 가지 주요 개념에 대해 설명하겠습니다. 지금은 특별히 JavaScript를 참조하지 않고 이러한 개념을 설명할 것이므로 모든 예제는 {{Glossary("Pseudocode", "pseudocode")}} 로 제공됩니다.

> **참고:** 정확히 말하자면, 여기에 설명된 기능은 **클래스 기반** 또는 "클래식" OOP라고 하는 특정 스타일의 OOP에 속합니다. 사람들이 OOP에 대해 이야기할 때 일반적으로 이 유형을 의미합니다.

그 다음에는 자바스크립트에서 생성자와 프로토타입 체인이 이러한 OOP 개념과 어떤 관련이 있고 어떻게 다른지 살펴볼 것입니다. 다음 글에서는 객체 지향 프로그램을 더 쉽게 구현할 수 있는 자바스크립트의 몇 가지 추가 기능에 대해 살펴보겠습니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        JavaScript 함수에 대한 이해, JavaScript 기본 사항
        (<a href="/ko/docs/Learn/JavaScript/First_steps">첫 번째 단계</a> 및
        <a href="/ko/docs/Learn/JavaScript/Building_blocks"
          >빌딩 블록</a
        > 참조), 및 OOJS 기본 사항 (<a href="/ko/docs/Learn/JavaScript/Objects/Basics"
          >객체 소개</a
        > 및 <a href="/ko/docs/Learn/JavaScript/Objects/Object_prototypes">객체 프로토타입</a> 참조)에 익숙해야 합니다..
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        클래스 기반 객체 지향 프로그래밍의 기본 개념을 이해합니다.
      </td>
    </tr>
  </tbody>
</table>

객체 지향 프로그래밍은 시스템을 객체의 집합으로 모델링하는 것으로, 각 객체는 시스템의 특정 측면을 나타냅니다. 객체에는 함수(또는 메서드)와 데이터가 모두 포함됩니다. 객체는 이를 사용하려는 다른 코드에 공용 인터페이스를 제공하지만 자체의 비공개 내부 상태를 유지하므로 시스템의 다른 부분은 객체 내부에서 무슨 일이 일어나는지 신경 쓸 필요가 없습니다.

## 클래스 및 인스턴스

OOP에서 객체 측면에서 문제를 모델링할 때는 시스템에 갖고자 하는 객체 유형을 나타내는 추상적인 정의를 만듭니다. 예를 들어 학교를 모델링하는 경우 교수를 나타내는 객체가 필요할 수 있습니다. 모든 교수는 이름과 가르치는 과목이 있다는 몇 가지 공통 속성을 가지고 있습니다. 또한 모든 교수는 특정 작업을 수행할 수 있습니다. 예를 들어, 모든 교수는 논문을 채점할 수 있고 연초에 학생들에게 자신을 소개할 수 있습니다.

따라서 `Professor` 는 우리 시스템에서 하나의 **클래스** 가 될 수 있습니다. 클래스의 정의에는 모든 교수가 가지고 있는 데이터와 방법이 나열되어 있습니다.

의사 코드에서 `Professor` 클래스는 다음과 같이 작성할 수 있습니다:

```
class Professor
    properties
        name
        teaches
    methods
        grade(paper)
        introduceSelf()
```

`Professor` 클래스를 정의합니다:

- 두 개의 데이터 속성: `name` 과 `teaches`
- 두 개의 메서드: 논문을 채점하는 `grade()`와 자신을 소개하는 `introduceSelf()`

클래스는 그 자체로는 아무 것도 하지 않습니다. 클래스는 해당 유형의 구체적인 객체를 생성하기 위한 일종의 템플릿입니다. 우리가 생성하는 각각의 구체적인 교수를 `Professor` 클래스의 **인스턴스** 라고 합니다. 인스턴스를 생성하는 과정은 **생성자** 라는 특수 함수에 의해 수행됩니다. 새 인스턴스에서 초기화하려는 내부 상태에 대한 값을 생성자에게 전달합니다.

일반적으로 생성자는 클래스 정의의 일부로 작성되며 일반적으로 클래스 자체와 같은 이름을 갖습니다:

```
class Professor
    properties
        name
        teaches
    constructor
        Professor(name, teaches)
    methods
        grade(paper)
        introduceSelf()
```

이 생성자는 두 개의 매개 변수를 사용하므로 새로운 구체적인 교수를 생성할 때 `name`과 `teaches` 속성을 초기화할 수 있습니다.

이제 생성자가 생겼으니 교수를 몇 개 생성할 수 있습니다. 프로그래밍 언어에서는 생성자가 호출되고 있음을 알리기 위해 `new`라는 키워드를 사용하는 경우가 많습니다.

```js
walsh = new Professor("Walsh", "Psychology");
lillian = new Professor("Lillian", "Poetry");

walsh.teaches; // 'Psychology'
walsh.introduceSelf(); // 'My name is Professor Walsh and I will be your Psychology professor.'

lillian.teaches; // 'Poetry'
lillian.introduceSelf(); // 'My name is Professor Lillian and I will be your Poetry professor.'
```

이렇게 하면 두 개의 객체가 생성되며, 두 객체 모두 `Professor` 클래스의 인스턴스입니다.

## 상속

우리 학교에서도 학생을 대표하고 싶다고 가정해 보겠습니다. 교수와 달리 학생은 논문을 채점할 수 없고, 특정 과목을 가르치지 않으며, 특정 학년에 속하지 않습니다.

하지만 학생은 이름이 있고 자신을 소개하고 싶을 수도 있으므로 학생 클래스의 정의를 다음과 같이 작성할 수 있습니다:

```
class Student
    properties
        name
        year
    constructor
        Student(name, year)
    methods
        introduceSelf()
```

학생과 교수가 일부 속성을 공유한다는 사실, 더 정확하게는 어느 정도 수준에서는 같은 종류의 존재라는 사실을 표현할 수 있다면 도움이 될 것입니다. **상속** 을 통해 이를 구현할 수 있습니다.

먼저 학생과 교수 모두 사람이며, 사람은 이름을 가지고 있고 자신을 소개하고자 한다는 점을 관찰합니다. 사람의 모든 공통 속성을 정의하는 새로운 클래스 `Person`을 정의하여 이를 모델링할 수 있습니다. 그런 다음 `Professor`와 `Student`은 모두 `Person`에서 **파생** 되어 추가 속성을 추가할 수 있습니다:

```
class Person
    properties
        name
    constructor
        Person(name)
    methods
        introduceSelf()

class Professor : extends Person
    properties
        teaches
    constructor
        Professor(name, teaches)
    methods
        grade(paper)
        introduceSelf()

class Student : extends Person
    properties
        year
    constructor
        Student(name, year)
    methods
        introduceSelf()
```

이 경우 `Person`은 `Professor`와 `Student` 모두의 **슈퍼클래스** 또는 **상위 클래스** 라고 할 수 있습니다. 반대로 `Professor`와 `Student`은 `Person`의 **서브클래스** 또는 **자식 클래스** 입니다.

`introduceSelf()` 가 세 클래스 모두에 정의되어 있는 것을 볼 수 있습니다. 그 이유는 모든 사람이 자신을 소개하기를 원하지만 소개하는 방식이 다르기 때문입니다:

```js
walsh = new Professor("Walsh", "Psychology");
walsh.introduceSelf(); // 'My name is Professor Walsh and I will be your Psychology professor.'

summers = new Student("Summers", 1);
summers.introduceSelf(); // 'My name is Summers and I'm in the first year.'
```

학생이나 교수가 아닌 사용자를 위해 `introduceSelf()`의 기본 구현이 있을 수 있습니다:

```js
pratt = new Person("Pratt");
pratt.introduceSelf(); // 'My name is Pratt.'
```

메서드의 이름은 같지만 다른 클래스에서 구현이 다른 경우 이 기능을 **다형성** 이라고 합니다. 서브클래스의 메서드가 슈퍼클래스의 구현을 대체하는 경우, 서브클래스가 슈퍼클래스의 버전을 **오버라이드** 한다고 말합니다.

## 캡슐화

객체는 객체를 사용하고자 하는 다른 코드에 인터페이스를 제공하지만 자체 내부 상태를 유지합니다. 객체의 내부 상태는 **비공개** 로 유지되므로 다른 객체가 아닌 객체 자체 메서드에서만 액세스할 수 있습니다. 객체의 내부 상태를 비공개로 유지하고 일반적으로 공개 인터페이스와 비공개 내부 상태를 명확하게 구분하는 것을 **캡슐화** 라고 합니다.

이 기능은 프로그래머가 객체를 사용하는 모든 코드를 찾아 업데이트할 필요 없이 객체의 내부 구현을 변경할 수 있게 해주며, 객체와 나머지 시스템 사이에 일종의 방화벽을 생성하기 때문에 유용한 기능입니다.

예를 들어, 2학년 이상의 학생에게 양궁을 배울 수 있도록 허용한다고 가정해 보겠습니다. 학생의 `year` 속성을 노출하는 것만으로 이를 구현할 수 있으며, 다른 코드에서 이를 검사하여 해당 학생의 수강 가능 여부를 결정할 수 있습니다:

```js
if (student.year > 1) {
  // allow the student into the class
}
```

문제는 학생이 양궁을 공부할 수 있도록 허용하는 기준을 변경하기로 결정하면(예: 부모 또는 보호자의 허락을 받아야 함) 이 테스트를 수행하는 시스템의 모든 위치를 업데이트해야 한다는 것입니다. 한 곳에서 로직을 구현하는 `Student` 객체의 `canStudyArchery()` 메서드를 사용하는 것이 더 좋습니다:

```
class Student : extends Person
    properties
       year
    constructor
       Student(name, year)
    methods
       introduceSelf()
       canStudyArchery() { return this.year > 1 }
```

```js
if (student.canStudyArchery()) {
  // allow the student into the class
}
```

이렇게 하면 양궁 공부에 대한 규칙을 변경하려는 경우 `Student` 클래스만 업데이트하면 되며, 이 클래스를 사용하는 모든 코드는 계속 작동합니다.

많은 OOP 언어에서는 일부 프로퍼티를 `private`로 표시하여 다른 코드가 객체의 내부 상태에 액세스하지 못하도록 할 수 있습니다. 이렇게 하면 객체 외부의 코드가 해당 프로퍼티에 액세스하려고 하면 오류가 발생합니다:

```
class Student : extends Person
    properties
       private year
    constructor
        Student(name, year)
    methods
       introduceSelf()
       canStudyArchery() { return this.year > 1 }

student = new Student('Weber', 1)
student.year // error: 'year' is a private property of Student
```

이와 같은 액세스를 강제하지 않는 언어에서는 프로그래머가 이름을 밑줄로 시작하는 등의 명명 규칙을 사용하여 해당 속성이 비공개로 간주되어야 함을 나타냅니다.

## OOP 및 JavaScript

이 글에서는 Java 및 C++와 같은 언어로 구현된 클래스 기반 객체 지향 프로그래밍의 기본 기능 몇 가지에 대해 설명했습니다.

앞선 두 개의 글에서는 [생성자](/ko/docs/Learn/JavaScript/Objects/Basics) 와 [프로토타입](/ko/docs/Learn/JavaScript/Objects/Object_prototypes) 이라는 두 가지 핵심 자바스크립트 기능을 살펴보았습니다. 이러한 기능은 위에서 설명한 일부 OOP 개념과 어느 정도 관련이 있습니다.

- 자바스크립트의 **생성자** 는 클래스 정의와 같은 기능을 제공하여 객체에 포함된 메서드를 포함한 객체의 "형태"를 한 곳에서 정의할 수 있게 해줍니다. 하지만 여기에서도 프로토타입을 사용할 수 있습니다. 예를 들어 생성자의 `prototype` 프로퍼티에 메서드가 정의되어 있으면 해당 생성자를 사용해 생성된 모든 객체는 프로토타입을 통해 해당 메서드를 가져오고, 생성자에서 메서드를 정의할 필요가 없습니다.

- **프로토타입 체인** 은 상속을 구현하는 자연스러운 방법처럼 보입니다. 예를 들어 프로토타입이 `Person`인 `Student` 객체가 있다면 이 객체는 `name`을 상속하고 `introduceSelf()`를 재정의할 수 있습니다.

하지만 이러한 기능과 위에서 설명한 "고전적인" OOP 개념의 차이점을 이해하는 것이 좋습니다. 여기서는 그 중 몇 가지를 강조하겠습니다.

첫째, 클래스 기반 OOP에서 클래스와 객체는 서로 분리된 두 가지 구조이며 객체는 항상 클래스의 인스턴스로 생성됩니다. 또한 클래스를 정의하는 데 사용되는 기능(클래스 구문 자체)과 객체를 인스턴스화하는 데 사용되는 기능(생성자)이 구분됩니다. 자바스크립트에서는 함수나 객체 리터럴을 사용해 별도의 클래스 정의 없이 객체를 생성할 수 있으며, 실제로 그렇게 하는 경우가 많습니다. 이를 통해 객체 작업이 기존 OOP보다 훨씬 가벼워질 수 있습니다.

둘째, 프로토타입 체인은 상속 계층 구조처럼 보이고 어떤 면에서는 상속 계층 구조처럼 동작하지만, 다른 면에서는 다릅니다. 서브클래스가 인스턴스화되면 서브클래스에 정의된 프로퍼티와 계층 구조 상위에 정의된 프로퍼티를 결합한 단일 객체가 생성됩니다. 프로토타이핑을 사용하면 계층 구조의 각 레벨이 별도의 객체로 표시되며 `__proto__` 속성을 통해 서로 연결됩니다. 프로토타입 체인의 동작은 상속보다는 **위임** 에 가깝습니다. 위임은 객체가 작업을 수행하라는 요청을 받으면 스스로 작업을 수행하거나 다른 객체(**위임자**)에게 대신 작업을 수행하도록 요청할 수 있는 프로그래밍 패턴입니다. 여러 가지 면에서 위임은 상속보다 객체를 더 유연하게 결합하는 방법입니다(우선, 런타임에 위임자를 변경하거나 완전히 교체할 수 있습니다).

즉, 생성자와 프로토타입은 자바스크립트에서 클래스 기반 OOP 패턴을 구현하는 데 사용할 수 있습니다. 하지만 상속과 같은 기능을 구현하는 데 직접 사용하는 것은 까다롭기 때문에 자바스크립트에서는 프로토타입 모델 위에 클래스 기반 OOP의 개념에 더 직접적으로 매핑되는 추가 기능을 계층화하여 제공합니다. 이러한 추가 기능은 다음 글에서 다룰 주제입니다.

## 요약

이 글에서는 클래스 기반 객체지향 프로그래밍의 기본 기능을 설명하고 자바스크립트 생성자와 프로토타입이 이러한 개념과 어떻게 비교되는지 간략하게 살펴봤습니다.

다음 글에서는 자바스크립트가 클래스 기반 객체 지향 프로그래밍을 지원하기 위해 제공하는 기능에 대해 살펴보겠습니다.

{{PreviousMenuNext("Learn/JavaScript/Objects/Object_prototypes", "Learn/JavaScript/Objects/Classes_in_JavaScript", "Learn/JavaScript/Objects")}}
