---
title: JavaScript object basics
slug: Learn/JavaScript/Objects/Basics
---

{{LearnSidebar}}{{NextMenu("Learn/JavaScript/Objects/Object_prototypes", "Learn/JavaScript/Objects")}}

이 글에서는 기본적인 자바스크립트 객체 구문을 살펴보고, 과정의 앞부분에서 이미 살펴본 자바스크립트 기능 중 상당수가 객체라는 사실을 다시 한 번 강조하면서 몇 가지 기능을 다시 살펴보겠습니다.

<table>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>
        Basic computer literacy, a basic understanding of HTML and CSS,
        familiarity with JavaScript basics (see
        <a href="/ko/docs/Learn/JavaScript/First_steps">First steps</a> and
        <a href="/ko/docs/Learn/JavaScript/Building_blocks">Building blocks</a>).
      </td>
    </tr>
    <tr>
      <th scope="row">Objective:</th>
      <td>
        To understand the basics of working with objects in JavaScript: creating objects, accessing and modifying object properties, and using constructors.
      </td>
    </tr>
  </tbody>
</table>

## 객체 기본 사항

객체는 관련 데이터 및/또는 기능의 모음입니다. 일반적으로 여러 변수와 함수(객체 내부에 있는 경우 프로퍼티 및 메서드라고 함)로 구성됩니다. 예제를 통해 객체가 어떻게 생겼는지 이해해 보겠습니다.

먼저 [oojs.html](https://github.com/mdn/learning-area/blob/main/javascript/oojs/introduction/oojs.html) 파일의 로컬 복사본을 만듭니다. 여기에는 소스 코드를 작성하기 위한 {{HTMLElement("script")}} 요소만 포함되어 있습니다. 이 파일을 기본 객체 구문을 살펴보기 위한 기초로 사용할 것입니다. 이 예제를 작업하는 동안 개발자 도구 JavaScript 콘솔](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools#the_javascript_console) 을 열고 몇 가지 명령을 입력할 준비가 되어 있어야 합니다.

자바스크립트의 다른 많은 작업과 마찬가지로 객체 생성은 변수를 정의하고 초기화하는 것으로 시작하는 경우가 많습니다. 파일에 이미 있는 JavaScript 코드 아래에 다음 줄을 입력한 다음 저장하고 새로고침하세요:

```js
const person = {};
```

이제 브라우저의 [JavaScript 콘솔](/ko/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools#the_javascript_console) 을 열고 `person` 을 입력한 다음 <kbd>Enter</kbd>/<kbd>Return</kbd> 키를 누릅니다. 아래 줄 중 하나와 유사한 결과가 표시됩니다:

```
[object Object]
Object { }
{ }
```

축하합니다, 방금 첫 번째 객체를 만들었습니다. 잘했어요! 하지만 이것은 빈 객체이므로 실제로 할 수 있는 일이 많지 않습니다. 파일에서 자바스크립트 객체를 다음과 같이 업데이트해 봅시다:
객
```js
const person = {
  name: ["Bob", "Smith"],
  age: 32,
  bio: function () {
    console.log(`${this.name[0]} ${this.name[1]} is ${this.age} years old.`);
  },
  introduceSelf: function () {
    console.log(`Hi! I'm ${this.name[0]}.`);
  },
};
```

저장하고 새로고침한 후 브라과저 개발자 도구의 JavaScript 콘솔에 다음 중 일부를 입력해 보세요:

```js
person.name;
person.name[0];
person.age;
person.bio();
// "Bob Smith is 32 years old."
person.introduceSelf();
// "Hi! I'm Bob."
```

이제 객체 내부에 몇 가지 데이터와 기능이 생겼으며, 이제 간단한 구문으로 데이터와 기능에 액세스할 수 있습니다!

그럼 여기서 무슨 일이 일어나고 있을까요? 객체는 여러 멤버로 구성되며, 각 멤버는 이름(예: 위의 `name` 과 `age`)과 값(예: `['Bob', 'Smith']` 및 `32`)을 가집니다. 각 이름/값 쌍은 쉼표로 구분해야 하며, 각 경우의 이름과 값은 콜론으로 구분합니다. 구문은 항상 이 패턴을 따릅니다:

```js
const objectName = {
  member1Name: member1Value,
  member2Name: member2Value,
  member3Name: member3Value,
};
```

객체 멤버의 값은 거의 모든 것이 될 수 있습니다. 사람 객체에는 숫자, 배열, 함수 두 개가 있습니다. 처음 두 항목은 데이터 항목이며 객체의 **속성** 이라고 합니다. 마지막 두 항목은 객체가 해당 데이터로 어떤 작업을 수행할 수 있도록 하는 함수로, 객체의 **메서드** 라고 합니다.

객체의 멤버가 함수인 경우 더 간단한 구문이 있습니다. `bio: function ()` 대신 `bio()` 를 작성할 수 있습니다. 다음과 같이요:

```js
const person = {
  name: ["Bob", "Smith"],
  age: 32,
  bio() {
    console.log(`${this.name[0]} ${this.name[1]} is ${this.age} years old.`);
  },
  introduceSelf() {
    console.log(`Hi! I'm ${this.name[0]}.`);
  },
};
```

이제부터는 이 짧은 구문을 사용하겠습니다.

이와 같은 객체를 **객체 리터럴** 이라고 하는데, 객체를 생성할 때 객체의 내용을 문자 그대로 적었습니다. 이는 나중에 살펴볼 클래스에서 인스턴스화된 객체와는 다릅니다.

예를 들어 데이터베이스에 넣을 요청을 서버에 보내는 등 일련의 구조화된 관련 데이터 항목을 어떤 방식으로든 전송하려는 경우 객체 리터럴을 사용하여 객체를 생성하는 것이 매우 일반적입니다. 단일 객체를 전송하는 것이 여러 항목을 개별적으로 전송하는 것보다 훨씬 효율적이며, 이름으로 개별 항목을 식별하려는 경우 배열보다 작업하기가 더 쉽습니다.

## 점 표기법

위에서 **점 표기법** 을 사용하여 객체의 프로퍼티와 메서드에 액세스했습니다. 객체 이름(person)은 **네임스페이스** 역할을 하므로 객체 내부의 모든 항목에 액세스하려면 앞에 입력해야 합니다. 그 다음에는 점 다음에 액세스하려는 항목(예를 들어 단순한 프로퍼티의 이름, 배열 프로퍼티의 항목 또는 객체의 메서드 중 하나에 에한 호출 등)을 작성합니다:

```js
person.age;
person.bio();
```

### 객체 프로퍼티로서의 객체

객체 프로퍼티는 그 자체로 객체가 될 수 있습니다. 예를 들어 `name` 멤버를

```js
const person = {
  name: ["Bob", "Smith"],
};
```

다음처럼 바꿔 봅시다.

```js
const person = {
  name: {
    first: "Bob",
    last: "Smith",
  },
  // …
};
```

이러한 항목에 액세스하려면 추가 단계를 다른 점으로 끝에 연결하기만 하면 됩니다. JS 콘솔에서 시도해 보세요:

```js
person.name.first;
person.name.last;
```

이 경우 메소드 코드를 살펴보고 다음과 같은 인스턴스가 있으면

```js
name[0];
name[1];
```

다음과 같이 변경해야 합니다.

```js
name.first;
name.last;
```

그렇지 않으면 방법이 더 이상 작동하지 않습니다.

## 대괄호 표기법

대괄호 표기법은 객체 속성에 액세스하는 다른 방법을 제공합니다. 다음과 같이 [점 표기법](#dot_notation) 을 사용하는 대신:

```js
person.age;
person.name.first;
```

대괄호를 사용할 수 있습니다:

```js
person["age"];
person["name"]["first"];
```

이는 배열의 항목에 액세스하는 방식과 매우 유사하며, 기본적으로 인덱스 번호를 사용하여 항목을 선택하는 대신 각 멤버의 값과 연관된 이름을 사용한다는 점에서 동일합니다. 배열이 숫자를 값에 매핑하는 것과 같은 방식으로 문자열을 값에 매핑하는 객체를 **연관 배열** 이라고 부르는 것은 당연합니다.

일반적으로 점 표기법이 대괄호 표기법보다을더 간결하고 읽기 쉽기 때문에 점 표기법이 선호됩니다. 그러나 대괄호를 사용해야 하는 경우도 있습니다. 예를 들어 객체 속성 이름이 변수에 들어 있는 경우 점 표기법을 사용하여 값에 액세스할 수 없지만 대괄호 표기법을 사용하여 값에 액세스할 수 있습니다.

아래 예제에서 `logProperty()` 함수는 `person[propertyName]`을 사용하여 `propertyName`에 지정된 속성 값을 찾을 수 있습니다.

```js
const person = {
  name: ["Bob", "Smith"],
  age: 32,
};

function logProperty(propertyName) {
  console.log(person[propertyName]);
}

logProperty("name");
// ["Bob", "Smith"]
logProperty("age");
// 32
```

## 객체 멤버 설정하기

지금까지는 객체 멤버를 검색(또는 **가져오기**)하는 방법만 살펴봤는데, 다음과 같이 설정하려는 멤버를 점 또는 대괄호 표기법을 사용하여 선언하여 객체 멤버의 값을 **설정** (업데이트)할 수도 있습니다:

```js
person.age = 45;
person["name"]["last"] = "Cratchit";
```

위의 줄을 입력한 다음 멤버를 다시 가져와서 다음과 같이 멤버가 어떻게 변경되었는지 확인합니다:

```js
person.age;
person["name"]["last"];
```

멤버 설정은 기존 프로퍼티와 메서드의 값을 업데이트하는 것에서 그치지 않고 완전히 새로운 멤버를 만들 수도 있습니다. JS 콘솔에서 다음과 같이 해보세요:

```js
person["eyes"] = "hazel";
person.farewell = function () {
  console.log("Bye everybody!");
};
```

이제 새 멤버를 테스트할 수 있습니다:

```js
person["eyes"];
person.farewell();
// "Bye everybody!"
```

대괄호 표기법의 한 가지 유용한 측면은 멤버 값뿐만 아니라 멤버 이름도 동적으로 설정하는 데 사용할 수 있다는 점입니다. 사용자가 두 개의 텍스트 입력에 구성원 이름과 값을 입력하여 사용자 지정 값 유형을 사람 데이터에 저장할 수 있도록 하려고 한다고 가정해 보겠습니다. 다음과 같은 값을 얻을 수 있습니다:

```js
const myDataName = nameInput.value;
const myDataValue = nameValue.value;
```

그런 다음 이 새 멤버 이름과 값을 다음과 같이 `person` 객체에 추가할 수 있습니다:

```js
person[myDataName] = myDataValue;
```

이를 테스트하려면 `person` 객체의 닫는 중괄호 바로 아래에 다음 줄을 코드에 추가해 보세요:

```js
const myDataName = "height";
const myDataValue = "1.75m";
person[myDataName] = myDataValue;
```

이제 저장하고 새로고침한 후 텍스트 입력란에 다음을 입력해 보세요:

```js
person.height;
```

이름을 가리키는 변수 값이 아닌 리터럴 멤버 이름만 허용하는 점 표기법에서는 위의 방법을 사용하여 객체에 프로퍼티를 추가할 수 없습니다.

## "this"란 무엇인가요?

저희 방식에서 약간 이상한 점을 발견하셨을 수도 있습니다. 예를 들어 이걸 보세요:

```js
introduceSelf() {
  console.log(`Hi! I'm ${this.name[0]}.`);
}
```

"this"가 무엇인지 궁금할 것입니다. `this` 키워드는 코드가 작성되고 있는 현재 객체를 가리키며, 이 경우 `this` 키워드는 `person` 에 해당합니다. 그렇다면 왜 그냥 `person` 이라고 쓰지 않을까요?

객체 리터럴을 하나만 생성해야 하는 경우에는 그렇게 유용하지 않습니다. 하지만 둘 이상을 생성하면 `this`를 써서 생성하는 모든 객체에 대해 동일한 메서드 정의를 사용할 수 있습니다.

단순화된 person 객체 쌍을 통해 그 의미를 설명해 보겠습니다:

```js
const person1 = {
  name: "Chris",
  introduceSelf() {
    console.log(`Hi! I'm ${this.name}.`);
  },
};

const person2 = {
  name: "Deepti",
  introduceSelf() {
    console.log(`Hi! I'm ${this.name}.`);
  },
};
```

이 경우 `person1.introduceSelf()` 는 "Hi! I'm Chris."를 출력하고, 반면에  `person2.introduceSelf()` 는 "Hi! I'm Deepti."를 출력하지만 메서드의 코드는 각 경우에서 정확히 동일합니다. 이 기능은 객체 리터럴을 직접 작성할 때는 크게 유용하지 않지만, **생성자** 를 사용해 하나의 객체 정의에서 둘 이상의 객체를 생성하기 시작할 때 필수적이며, 다음 섹션의 주제입니다.

## 생성자 소개

객체 리터럴을 사용하는 것은 객체를 하나만 생성해야 할 때는 괜찮지만, 이전 섹션에서처럼 둘 이상을 생성해야 하는 경우에는 매우 부적절합니다. 생성하는 모든 객체에 대해 동일한 코드를 작성해야 하고, `height` 프로퍼티를 추가하는 등 객체의 일부 프로퍼티를 변경하려면 모든 객체를 업데이트해야 합니다.

객체의 "형태"(메서드 집합과 객체가 가질 수 있는 속성)를 정의한 다음, 원하는 만큼 객체를 생성하고 다른 속성의 값만 업데이트하는 방법을 원합니다.

첫 번째 버전은 그냥 함수입니다:

```js
function createPerson(name) {
  const obj = {};
  obj.name = name;
  obj.introduceSelf = function () {
    console.log(`Hi! I'm ${this.name}.`);
  };
  return obj;
}
```

이 함수는 호출할 때마다 새 객체를 생성하고 반환합니다. 객체에는 두 개의 멤버가 있습니다:

- 속성 `name`
- 메서드 `introduceSelf()`.

`createPerson()` 은 `name` 속성 값을 설정하기 위해 매개변수 `name` 을 받지만, 이 함수를 사용하여 생성된 모든 객체에 대해 `introduceSelf()` 메서드의 값은 동일합니다. 이는 객체를 생성할 때 매우 일반적인 패턴입니다.

이제 정의를 재사용하여 원하는 만큼의 객체를 만들 수 있습니다:

```js
const salva = createPerson("Salva");
salva.name;
salva.introduceSelf();
// "Hi! I'm Salva."

const frankie = createPerson("Frankie");
frankie.name;
frankie.introduceSelf();
// "Hi! I'm Frankie."
```

이 방법은 잘 작동하지만 빈 객체를 생성하고 초기화하여 반환해야 하므로 다소 시간이 오래 걸립니다. 더 나은 방법은 **생성자**. 를 사용하는 것입니다. 생성자는 {{jsxref("operators/new", "new")}}  키워드를 사용하여 호출되는 함수입니다. 생성자를 호출하면:

- 새 객체를 생성합니다.
- `this` 를 새 객체에 바인딩하여 생성자 코드에서 `this` 로 참조할 수 있도록 합니다.
- 생성자 코드에서 코드를 실행합니다.
- 새 객체를 반환합니다.

생성자는 관례에 따라 대문자로 시작하며 생성하는 객체 유형에 따라 이름이 지정됩니다. 따라서 예제를 다음과 같이 다시 작성할 수 있습니다:

```js
function Person(name) {
  this.name = name;
  this.introduceSelf = function () {
    console.log(`Hi! I'm ${this.name}.`);
  };
}
```

생성자로 `Person()` 을 호출하려면 `new` 를 사용합니다:

```js
const salva = new Person("Salva");
salva.name;
salva.introduceSelf();
// "Hi! I'm Salva."

const frankie = new Person("Frankie");
frankie.name;
frankie.introduceSelf();
// "Hi! I'm Frankie."
```

## 계속 객체를 사용해 왔습니다.

이 예제를 살펴보면서 여러분은 아마도 지금까지 사용해온 점 표기법이 매우 익숙하다고 생각했을 것입니다. 그도 그럴 것이 이 과정을 통해 계속 사용해왔기 때문입니다! 내장된 브라우저 API나 자바스크립트 객체를 사용하는 예제를 살펴볼 때마다 객체를 사용해왔는데, 이러한 기능은 기본 사용자 정의 예제보다 복잡하긴 하지만 여기서 살펴본 것과 똑같은 종류의 객체 구조를 사용하여 구축되기 때문입니다.

따라서 다음과 같은 문자열 메서드를 사용했을 때

```js
myString.split(",");
```

[`String`](/ko/docs/Web/JavaScript/Reference/Global_Objects/String) 객체에서 사용할 수 있는 메서드를 사용하고 있었습니다. 코드에서 문자열을 생성할 때마다 해당 문자열은 자동으로 `String` 의 인스턴스로 생성되므로 몇 가지 일반적인 메서드와 속성을 사용할 수 있습니다.

다음과 같은 줄을 사용하여 문서 객체 모델에 액세스한 경우:

```js
const myDiv = document.createElement("div");
const myVideo = document.querySelector("video");
```

[`Document`](/ko/docs/Web/API/Document) 객체에서 사용할 수 있는 메서드를 사용하고 있었습니다. 웹페이지가 로드될 때마다 전체 페이지의 구조, 콘텐츠 및 URL과 같은 기타 기능을 나타내는 `document` 라는 `Document` 인스턴스가 생성됩니다. 다시 말하지만, 이 인스턴스에는 몇 가지 일반적인 메서드와 속성을 사용할 수 있습니다.

[`Array`](/ko/docs/Web/JavaScript/Reference/Global_Objects/Array), [`Math`](/ko/docs/Web/JavaScript/Reference/Global_Objects/Math) 등 기존에 사용하던 거의 모든 내장 객체나 API도 마찬가지입니다.

기본 제공 객체와 API가 항상 객체 인스턴스를 자동으로 생성하는 것은 아닙니다. 예를 들어 최신 브라우저에서 시스템 알림을 실행할 수 있는 [Notifications API](/ko/docs/Web/API/Notifications_API) 의 경우, 실행하려는 각 알림에 대해 생성자를 사용하여 새 객체 인스턴스를 인스턴스화해야 합니다. 자바스크립트 콘솔에 다음을 입력해 보세요:

```js
const myNotification = new Notification("Hello!");
```

## 실력을 테스트해 보세요!

이 글을 끝까지 읽었지만 가장 중요한 정보를 기억할 수 있나요? 계속 진행하기 전에 이 정보를 잘 기억하고 있는지 확인할 수 있는 몇 가지 추가 테스트가 있으니, [실력을 테스트해 보세요!: 객체 기초](/ko/docs/Learn/JavaScript/Objects/Test_your_skills:_Object_basics) 를 참조하세요.

## 요약

이제 간단한 객체 생성을 포함해 자바스크립트에서 객체로 작업하는 방법에 대해 잘 이해하셨을 것입니다. 또한 객체가 관련 데이터와 기능을 저장하는 구조로 매우 유용하다는 사실에 감사해야 합니다. `person` 객체의 모든 프로퍼티와 메서드를 별도의 변수와 함수로 추적하려고 하면 비효율적이고 답답할 뿐 아니라 이름이 같은 다른 변수 및 함수와 충돌할 위험에 처할 수 있습니다. 객체를 사용하면 정보를 자체 패키지에 안전하게 보관할 수 있습니다.

다음 글에서는 자바스크립트에서 객체가 다른 객체로부터 속성을 상속할 수 있는 기본적인 방법인 **프로토타입** 에 대해 살펴보겠습니다.

{{NextMenu("Learn/JavaScript/Objects/Object_prototypes", "Learn/JavaScript/Objects")}}
