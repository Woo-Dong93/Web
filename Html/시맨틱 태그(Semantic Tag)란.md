# 시맨틱 태그(Semantic Tag)란?

- HTML5에 도입된 시맨틱 태그는 개발자와 브라우저에게 의미있는 태그를 제공하게 된다.
- 예를 들어, `<div>` 태그는 non-semantic 태그라고 할 수 있고, `<table>`, `<article>` 등의 태그는 semantic 태그라고 볼 수 있다.

```html
<div class="header"> 
<div id="footer">
```

```html
<header>
<footer>
```

- 헤더 정보 표현을 위해 `<div class='head'>` `<div class='hd'>` `<div class='hdr'>` 등 여러 방법으로 표현이 가능하지만, HTML5에서는 **시맨틱 태그**를 제공하여 HTML태그의 의미를 명확하게 할 수 있다는 것이다.



### 종류

- `<article>`
- `<aside>`
- `<details>`
- `<figcaption>`
- `<figure>`
- `<footer>`
- `<header>`
- `<main>`
- `<mark>`
- `<nav>`
- `<section>`
- `<summary>`
- `<time>`



### **왜 시맨틱 태그를 사용해야 하는가?**

- 기존에는 `<div>` 태그 안에 id나 class 속성으로 개발자별로 각자 이름을 지정하였기 때문에, 검색엔진이 html 파일을 분석할 때 정확하게 컨텐츠를 식별하기가 힘들었다.
- HTML5에서는 정해진 시맨틱 태그를 사용하기로 규약을 정한 거라고 보면 될 것 같다.