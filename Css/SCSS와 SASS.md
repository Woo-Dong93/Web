# SCSS와 SASS

- SCSS와 SASS는 CSS를 편리하게 이용할 수있도록 도와주며 추가 기능도 있는 CSS를 확장한 스크립팅 언어입니다.

- CSS

```css
.list {
    width: 100px;
    float: left;
}
li {
    color: red;
    background: url("./image.jpg");
}
li:last-child {
    margin-right: -10px;
}
```

- SCSS

```css
.list {
  width: 100px;
  float: left;
  li {
    color: red;
    background: url("./image.jpg");
    &:last-child {
      margin-right: -10px;
    }
  }
}
```

- SASS

```css
.list
  width: 100px
  float: left
  li
    color: red
    background: url("./image.jpg")
    &:last-child
      margin-right: -10px
```



### 왜 사용하는 것일 까?

- 프로젝트가 커지면 불필요한 선택자 등 CSS 구조가 복잡해집니다.
- SCSS와 SASS는 CSS 작업을 쉽게 도와주며 가독성과 재사용성을 높여주어 유지보수가 쉬어제기 도와줍니다.
  - 일반 코드 작성하는 것처럼 부모, 자식 관계를 중괄호나 여백으로 쉽게 작성할 수 있다.
- CSS의 태생적 한계를 보완하기 위해 SASS는 추가 기능과 유용한 도구를 제공한다.
  - 변수의 사용
  - 조건문 반복문
  - Import
  - Nesting
  - Mixin : 연관성 없는 선택자의 중복 코드제거, 연관성은 없지만 코드가 겹치는 선택자들에 사용
    - SCSS에서 연관성 없는 `class`에 `extend`키워드를 사용해서 컬러를 똑같이 재사용 했을 때 CSS로 컴파일 되면 `.main_conatiner, .view_container, .detail_container {  color: #f00;  }` 이런식으로 뭉쳐지게 됩니다.
    - 서로 연관성이 없는 클래스에 단순히 같은 속성을 부여하기 위해서 `extend`를 사용할 경우 이러한 문제점이 생깁니다.
    - 여기서 SASS 문법인 `mixin`을 사용하면 연관성이 없는 반복되는 규칙을 따로 만들어서 사용합니다.
    - `.main_conatiner {  color: #f00;} .view_container {  color: #f00;* .detail_container {  color: #f00;}`
  - Extend/Inheritance : 연관성이 있는 코드에 사용



### SASS와 SCSS의 차이는 무엇이냐?

- SASS보다 SCSS가 뒤에 나왔고 여러가지 문법의 차이가 있지만 SCSS가 더 넓은 범용성과 CSS 호환성 등의 장점으로 **SCSS**를 사용하기를 권장하고 있다. (공식문서도 SCSS를 기준으로 나와 있다.)
  - SCSS 문법으로 작성한 SASS는 모든 CSS버전과 완전히 호환됩니다.
- 그래서 통상적으로 SASS를 SCSS라고 부릅니다.
- **공식 문법**: 공식 레퍼런스는 SCSS 문법을 기준으로 모든 문법을 설명하고 예시를 보여줍니다.
- **더 넓은 사용자**: 다수의 라이브러리, 프레임워크가 SCSS 문법을 활용하는 등 새로운 문법이 더욱 널리 쓰입니다.
- **CSS 호환성**: 친근한 CSS 문법은 Sass와 CSS 사이의 심리적 틈을 줄여주고, 기능적으로도 확장성을 높입니다.
- **여러 줄 쓰기 지원**: Sass 문법은 들여쓰기와 줄 바꿈이 문법의 중요한 요소이기 때문에, 반대로 여러 줄 쓰기를 지원하지 않습니다.



### SASS와 SCSS는 CSS 전처리기

- Sass(SCSS)를 **CSS pre-processor**(전 처리기)라고도 하는데 이는 Sass자체로 브라우저에 적용하는 것이 아니라 CSS를 확장해서 쉽고 편리하게 쓰기 위해 쓰는 스크립팅 언어이기 때문입니다.
- 따라서 Sass로 작성한 코드는 컴파일을 해서 일반 CSS의 문법으로 바꾼 뒤 적용합니다.
  