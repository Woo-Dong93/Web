# Inline element 와 Block element

### 1. Block element

- 화면 전체를 차지 하는 박스형태을 가지는 성질입니다. 그렇기 때문에 기본적으로 block은 width값이 100%가 됩니다. 그리고 라인이 새로 추가된다는 것을 알 수 있습니다. 
- height와 width 값을 지정 할 수 있다.
- margin과 padding을 지정 할 수 있다.
- 종류

```html
<address>, <article>, <aside>, <blockgquote>, <canvas>, <dd>, <div>, <dl>, <hr>, <header>, <form>,<h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <table>, <pre>, <ul>, <p>, <ol>, <video>
```



### 2. Inline element

- inline은 화면의 일부를 차지하는 태그로서 주로 텍스트를 주입 할 때 사용 되는 형태입니다. 
- 그렇기 때문에 기본적으로 block처럼 width값이 100%가 아닌 컨텐츠 영역 만큼 자동으로 잡히게 되며 라인이 새로 추가 되지 않습니다. 
- 높이 또한 폰트의 크기만큼 잡힙니다. (line-height로 설정이 가능 하긴 합니다.)
- width와 height를 명시 할 수 없다.
- margin은 위아래엔 적용 되지 않는다.
- padding은 좌우는 공간과 시각적인 부분이 모두 적용 되지만 위아래는 시각적으로는 추가되지만 공간을 차지 하지는 않는다.
- 종류

```html
<a>, <i>, <span>, <abbr>, <img>, <strong>, <b>, <input>, <sub>, <br>, <code>, <em>, <small>, <tt>, <map>, <textarea>, <label>, <sup>, <q>, <button>, <cite>
```



### 3. inline-block

-  **inline**의 특징과 **block**의 특징을 모두 가진 요소입니다.
- 줄바꿈이 이루어지지 않는다.
- block처럼 width와 height를 지정 할 수 있다.
- 만약 width와 height를 지정하지 않을 경우, inline과 같이 컨텐츠만큼 영역이 잡힌다.



### 4. display 속성

- 요소를 어떻게 표시할지 선택하는 속성입니다.
- 종류
  - `display: inline`
  - `display: block`
  - `display: none` : 차지하고 있던 공간이 사라지며 텍스트만 표시 된다.
  - `display: inline-block`