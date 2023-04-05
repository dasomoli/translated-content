---
title: Classes in JavaScript
slug: Learn/JavaScript/Objects/Classes_in_JavaScript
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/JavaScript/Objects/Object-oriented_programming", "Learn/JavaScript/Objects/JSON", "Learn/JavaScript/Objects")}}

[지난 글](/ko/docs/Learn/JavaScript/Objects/Object-oriented_programming) 에서는 객체 지향 프로그래밍(OOP)의 몇 가지 기본 개념을 소개하고 OOP 원리를 사용하여 학교의 교수와 학생을 모델링한 예에 대해 설명했습니다.

또한 이러한 모델을 구현하기 위해 [프로토타입](/ko/docs/Learn/JavaScript/Objects/Object_prototypes) 과 [생성자](/ko/docs/Learn/JavaScript/Objects/Basics#introducing_constructors) 를 사용할 수 있는 방법과 자바스크립트가 고전적인 OOP 개념에 더 가깝게 매핑되는 기능을 제공한다는 사실에 대해서도 이야기했습니다.

이 글에서는 이러한 기능들을 살펴보겠습니다. 여기서 설명하는 기능들은 객체를 결합하는 새로운 방법이 아니며, 내부적으로는 여전히 프로토타입을 사용한다는 점을 명심할 필요가 있습니다. 프로토타입 체인을 더 쉽게 설정할 수 있는 방법일 뿐입니다.

<table>
  <tbody>
    <tr>
      <th scope="row">사전 요구 사항:</th>
      <td>
        기본적인 컴퓨터 활용 능력, HTML 및 CSS에 대한 기본적인 이해, JavaScript 기본 사항(<a href="/ko/docs/Learn/JavaScript/First_steps">첫걸음</a> 및
        <a href="/ko/docs/Learn/JavaScript/Building_blocks"
          >빌딩 블록</a
        >참조) 및 OOJS 기본 사항 (<a href="/ko/docs/Learn/JavaScript/Objects/Basics"
          >객체 소개</a
        >, <a href="/ko/docs/Learn/JavaScript/Objects/Object_prototypes">객체 프로토타입</a>, 및 <a href="/ko/docs/Learn/JavaScript/Objects/Object-oriented_programming">객체 지향 프로그래밍</a>참조)에 익숙해야 합니다.
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>
        JavaScript가 제공하는 기능을 사용하여 "고전적인" 객체 지향 프로그램을 구현하는 방법을 이해합니다.
      </td>
    </tr>
  </tbody>
<table>

## 클래스 및 생성자

{{jsxref("Statements/class", "class")}} 키워드를 사용하여 클래스를 선언할 수 있습니다. 이전 글에서 `Person`에 대한 클래스 선언은 다음과 같습니다:

```js
class Person {

  name;

  constructor(name) {
    this.name = name;
  }

  introduceSelf() {
    console.log(`Hi! I'm ${this.name}`);
  }

}
```

이것은 `Person`이라는 클래스를 선언합니다:

- `name` 프로퍼티.
- 새 객체의 `name` 속성을 초기화하는 데 사용되는 `name` 매개변수를 받는 생성자.
- `this`를 사용해 객체의 프로퍼티를 참조할 수 있는 `introduceSelf()` 메서드

`name;` 선언은 선택 사항이므로 생략할 수 있으며, 생성자에서 `this.name = name;` 줄을 사용하면 `name` 프로퍼티를 초기화하기 전에 생성됩니다. 그러나 클래스 선언에 프로퍼티를 명시적으로 나열하면 코드를 읽는 사람들이 어떤 프로퍼티가 이 클래스의 일부인지 쉽게 확인할 수 있습니다.

선언할 때 `name = '';` 같은 줄을 사용하여 프로퍼티를 기본값으로 초기화할 수도 있습니다.

생성자는 {{jsxref("Classes/constructor", "constructor")}} 키워드를 사용하여 정의됩니다. [클래스 정의 외부의 생성자](/ko/docs/Learn/JavaScript/Objects/Basics#introducing_constructors) 와 마찬가지로 생성자도 마찬가지입니다:

- 새 객체를 생성
- 새 객체에 `this`를 바인딩하여 생성자 코드에서 `this`를 참조할 수 있도록 합니다.
- 생성자 코드에서 코드를 실행
- 새 객체를 반환

위의 클래스 선언 코드가 주어지면 다음과 같이 새 `Person` 인스턴스를 생성하여 사용할 수 있습니다:

```js
const giles = new Person('Giles');

giles.introduceSelf(); // Hi! I'm Giles
```

이 예제에서는 `Person`이라는 클래스 이름을 사용하여 생성자를 호출합니다.

### 생성자 생략하기

특별한 초기화가 필요하지 않은 경우 생성자를 생략할 수 있으며 기본 생성자가 자동으로 생성됩니다:

```js
class Animal {

  sleep() {
    console.log('zzzzzzz');
  }

}

const spot = new Animal();

spot.sleep(); // 'zzzzzzz'
```

## 상속

위의 `Person` 클래스가 주어지면 `Professor` 서브클래스를 정의해 보겠습니다

```js
class Professor extends Person {

  teaches;

  constructor(name, teaches) {
    super(name);
    this.teaches = teaches;
  }

  introduceSelf() {
    console.log(`My name is ${this.name}, and I will be your ${this.teaches} professor.`);
  }

  grade(paper) {
    const grade = Math.floor(Math.random() * (5 - 1) + 1);
    console.log(grade);
  }

}
```

{{jsxref("Classes/extends", "extends")}} 키워드를 사용하여 이 클래스가 다른 클래스에서 상속된다는 것을 나타냅니다.

`Professor` 클래스는 새로운 속성 `teaches`을 추가하므로 이를 선언합니다.

새 `Professor`가 생성될 때 `teaches`을 설정하고 싶기 때문에 `name`과 `teaches`을 인수로 받는 생성자를 정의합니다. 이 생성자가 가장 먼저 하는 일은 {{jsxref("Operators/super", "super()")}} 를 사용하여 `name` 매개변수를 전달하면서 슈퍼클래스 생성자를 호출하는 것입니다. 수퍼클래스 생성자는 `name` 설정을 처리합니다. 그 후 `Professor` 생성자가 `teaches` 속성을 설정합니다.

> **참고:** 서브클래스에 자체 초기화 작업이 있는 경우, 먼저 슈퍼클래스 생성자가 예상하는 매개변수를 전달하면서 `super()`를 사용해 슈퍼클래스 생성자를 **호출해야** 합니다.

또한 슈퍼클래스의 `introduceSelf()` 메서드를 재정의하고 논문 채점을 위해 `grade()` 메서드를 새로 추가했습니다(우리 교수님은 그다지 좋지 않아서 논문에 무작위로 성적을 부여합니다).

이 선언을 통해 이제 교수를 생성하고 사용할 수 있습니다:

```js
const walsh = new Professor('Walsh', 'Psychology');
walsh.introduceSelf();  // 'My name is Walsh, and I will be your Psychology professor'

walsh.grade('my paper'); // some random grade
```

## 캡슐화

마지막으로 자바스크립트에서 캡슐화를 구현하는 방법을 살펴봅시다. 지난 글에서 `Student` 클래스를 사용하는 코드를 손상시키지 않고 양궁 클래스에 대한 규칙을 변경할 수 있도록 `Student`의 `year` 속성을 비공개로 설정하는 방법에 대해 설명했습니다.

다음은 바로 그렇게 하는 `Student` 클래스의 선언입니다:

```js
class Student extends Person {

  #year;

  constructor(name, year) {
    super(name);
    this.#year = year;
  }


  introduceSelf() {
    console.log(`Hi! I'm ${this.name}, and I'm in year ${this.#year}.`);
  }

  canStudyArchery() {
    return this.#year > 1;
  }

}
```

이 클래스 선언에서 `#year`는 [비공개 데이터 속성](/ko/docs/Web/JavaScript/Reference/Classes/Private_class_fields) 입니다. `Student` 객체를 생성하면 내부적으로 `#year`를 사용할 수 있지만 객체 외부의 코드가 `#year`에 액세스하려고 하면 브라우저에서 오류가 발생합니다:

```js
const summers = new Student('Summers', 2);

summers.introduceSelf(); // Hi! I'm Summers, and I'm in year 2.
summers.canStudyArchery(); // true

summers.#year; // SyntaxError
```

비공개 데이터 속성은 클래스 선언에서 선언해야 하며, 그 이름은 `#`으로 시작해야 합니다.

### 비공개 메서드

비공개 데이터 프로퍼티와 마찬가지로 비공개 메서드도 가질 수 있습니다. 비공개 데이터 프로퍼티와 마찬가지로 이름은 `#`으로 시작하며 객체의 자체 메서드에서만 호출할 수 있습니다:

```js
class Example {
  somePublicMethod() {
    this.#somePrivateMethod();
  }

  #somePrivateMethod() {
    console.log('You called me?');
  }
}

const myExample = new Example();

myExample.somePublicMethod(); // 'You called me?'

myExample.#somePrivateMethod(); // SyntaxError
```

## 실력을 테스트해 보세요!

이 글을 끝까지 읽었지만 가장 중요한 정보를 기억할 수 있나요? 다음 단계로 넘어가기 전에 이 정보를 잘 기억하고 있는지 확인할 수 있는 몇 가지 추가 테스트가 있으니, [실력을 테스트해 보세요: 객체 지향 자바스크립트](/ko/docs/Learn/JavaScript/Objects/Test_your_skills:_Object-oriented_JavaScript) 를 참조하세요.

## 요약

이 글에서는 객체 지향 프로그램 작성에 사용할 수 있는 JavaScript의 주요 도구에 대해 살펴봤습니다. 여기서 모든 것을 다루지는 않았지만 시작하기에 충분할 것입니다. 자세한 내용은 [클래스 문서](/ko/docs/Web/JavaScript/Reference/Classes) 를 참조하세요.
{{PreviousMenuNext("Learn/JavaScript/Objects/Object-oriented_programming", "Learn/JavaScript/Objects/JSON", "Learn/JavaScript/Objects")}}
