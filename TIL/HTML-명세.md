# HTML 명세

HTML은 문서의 골격, 의미, 느낌을 전달하는 언어이다.

```html
<p>
  <a>
    <div>해당 마크업은 적절한가?</div>
  </a>
</p>
```

W3C에서 제공하는 HTML 명세는 브라우저 제조사들의 연합인 WHATWG(왓워킹그룹)의 명세로 대체되었다.
HTML 표준 명세를 제공하고 있더라도 브라우저 제조사가 구현하지 않으면 의미가 없다.
따라서 구현된 표준인지를 [caniuse.com](https://caniuse.com/ciu/comparison)에서 확인하여야 한다.

## HTML 콘텐츠 분류

<img width="400" alt="스크린샷 2022-02-25 오후 3 08 46" src="https://user-images.githubusercontent.com/100114050/155663644-f2750c4c-a167-421f-8934-34776aa36985.png">

<img width="1100" alt="스크린샷 2022-02-25 오후 3 12 49" src="https://user-images.githubusercontent.com/100114050/155664068-c519e417-9709-422a-beb9-912bc3650943.png">

### Flow Content

body에 포함할 수 있는 모든 요소로, 예전에 Block, Inline 컨테이너로 분류되던 요소들도 모두 포함된다.

### Metadata Content

주로 문서에 head 안에 포함되는 요소이나 `<script>`나 `<template>` 같은 요소들은 head, body에 모두 사용할 수 있다.
즉, `<script>`, `<template>`는 경우에 따라 Flow Content가 될 수 있는 요소들이다.
`display: none`으로 렌더링된다.

### Heading Content

- h1~h6, hgroup

Sectioning Content가 없어도 Heading Content가 있으면 암시적 개요가 형성된다.

### Sectioning Content

- article, aside, nav, section
- `display: block`으로 렌더링된다.

각 Sectioning Content는 암시적 개요를 형성하고, Heading Content를 함께 사용하면 명시적 개요를 형성한다.

### Phrasing Content

단락을 형성하는 콘텐츠로, 예전에 Inline 컨테이너라고 부르던 요소들이 대부분 여기에 속한다.
`display: inline | inline-block | none`으로 렌더링된다.

### Embeded Content

- iframe, picture, video...

외부 자원을 참조하는 콘텐츠로 모든 Embeded Content는 Phrasing Content다.
`display: inline | inline-block`으로 렌더링된다.

### Interactive Content

사용자와 상호작용할 수 있는 콘텐츠로, 입력 장치로 조작할 수 있다.
`display: inline | inline-block`으로 렌더링된다.

### Palpable Content

비어 있지 않은, hidden 속성이 없는, 볼 수 있는 콘텐츠를 가리킨다.

### Script-supporting Element

- script, template

렌더링되지는 않지만 사용자에게 어떤 기능을 제공해주는 요소들이다.

### Transparent Content

부모의 콘텐츠 모델을 따르며, 해당 요소를 제거해도 부모 자식 관계가 문법적으로 유효해야 한다.

## HTML 명세의 구성

[a 엘리먼트 명세](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-a-element)

<img width="1100" alt="스크린샷 2022-02-25 오후 3 12 49" src="https://user-images.githubusercontent.com/100114050/155664068-c519e417-9709-422a-beb9-912bc3650943.png">

- Categories
- Context in which this element can be used
  : 해당 엘리먼트를 허용하는 부모 요소를 유추할 수 있다. 단, 대체적으로 이러하다는 비규범적인 설명이다.
- Content Model : 반드시 따라야 하는 규범적인 설명이다.
- Tag omission in text/html
- Content attributes

```html
<p>
  <a>
    <div>해당 마크업은 적절한가?</div>
  </a>
</p>
```

p 요소의 Content Model은 Phrasing Content, a 요소의 Content Model은 Transparent Content이므로 부모의 콘텐츠 모델을 따른다.
따라서 a 요소의 자식 요소로는 Phrasing Content만 허용되는데 div 요소의 Content Model은 Flow, Palpable Content이므로 유효하지 않다.
