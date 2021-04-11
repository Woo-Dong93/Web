# React에서 css-module, sass, css-in-js

### 1. CSS 활용

- 장점 : 러닝커드가 없다. 문법이 쉽다.
- 단점
  - 서로다른 CSS파일에서 불러와 컴포넌트에 적용할 때 파일은 다르지만 `Class`명이 같을 경우 충돌이 발생하여 덮어 씌워지는 현상이 발생합니다.
  - 즉 하나의 CSS파일만 적용됩니다.



### 2. CSS-module

- 장점 

  - css-module을 이용하면 클래스명이 충돌하는 단점을 극복할 수 있습니다.
    - class 이름에 고유한 hash값을 붙여서 부여합니다.
  - css-module은 간결한 클래스명을 이용해서 컴포넌트 단위로 스타일을 적용할 때 좋습니다.

  - `{이름}.module.css`

```css
// Box1.css
.big {width : 200px;}
.small {width : 100px;}
.box {
    height : 50px;
    background-color: #aaaaaa;
}
```

```react
// 컴포넌트
import style from './Button1.module.css'

export default function Button({size}) {
    if (size==='big') {
        return <button className={`${style.button} ${style.big}`}>큰 버튼</button>
    } else {
        return <button className={`${style.button} ${style.big}`}> 작은 버튼</button>
    }
}
```





### 3. SASS

- Sass는 CSS와 비슷하지만, 별도의 문법 변수,믹스인(mixin)등의 개념이 있습니다. 이런 문법을 이용해 재사용성을 높힐 수 있습니다.
- Sass문법으로 작성한 파일은 별도의 빌드단계를 거쳐 CSS파일로 변환됩니다. CRA에서 Scss를 사용하고싶다면 **node-sass패키지**를 설치합니다.

```react
// Button3.js
import React from 'react'
import style from './Button3.module.scss'

export default function Button({size}) {
    if (size==='big') {
        return <button className={`${style.button} ${style.big}`}>큰 버튼</button>
    } else {
        return <button className={`${style.button} ${style.big}`}> 작은 버튼</button>
    }
}

//Button3.module.scss
@import './shared.scss';
.big {
    width:100px;
}
.small{
    width:50px;
}
.button{
    height:30px;
    background-color: $infoColor;
}
```



### 4. css-in-js

- CSS코드를 자바스크립트 파일안에서 작성합니다.
- 자바스크립트 내에서 관리하기 때문에 내부응집도가 올라가고, 동적으로 CSS를 변경하기도 쉽습니다.
- 템플릿 리터럴를 이용해 표현됩니다.
- `props`에 따라 컴포넌트의 CSS를 동적으로 변환할 수 있어서 재사용 가능한 컴포넌트를 만들 수 있습니다.
- 라이브러리 종류 : **styled-components**, **emotion**

```react
// Box4.js
import React from 'react';
import styled from 'styled-components'

const BoxCommon = styled.div`
    width : ${props=> (props.isBig? 200:100)}px;    // (1)
    height : 50px;
    background-color:#aaaaaa;
`;
export default function Box({size}) {    //(2)
    const isBig = size==='big';
    const label = isBig? '큰 박스' : '작은 박스'
    return <BoxCommon isBig={isBig}>{label}</BoxCommon>
}
```

- 단점
  - 러닝 커브 발생
  - 번들 크기가 커진다.
    - CSS-in-JS를 사용하려면 각종 라이브러리를 설치해야 하지만 일반 CSS-in-CSS는 별도의 라이브러리가 필요 없고 브라우저가 css를 알아서 해석합니다.
    - 즉 라이브러리를 추가한다는 것은 번들 사이즈가 커진다는 의미이고 다운로드 시간이 길어지므로 초기 진입이 느려질 수 있다.
    - 또한 JS가 모두 로딩된 후에 CSS 코드가 생성되기 때문에 더욱 느려질 수 밖에 없다.
    - 그래서 이 부분을 초기에 SSR을 통해 해결할 수 있지만 동적 인터랙션이 필요한 웹사이트는 CSS가 삽입되기 전까지 제대로 된 인터랙션이 적용되지 않을 수 있다.
  - CSS-in-JS를 사용하면 인터랙티브한 웹페이지의 성능을 저하시킨다. 
    - CSS-in-CSS는 모든 상태에 맞는 스타일을 전부 만들어두기 때문에 컴포넌트의 상태가 변경된다 하더라도 바로바로 적용이 가능하다. 하지만, CSS-in-JS의 경우, 상태가 변경되면 우선 JS의 CSS 코드를 읽어와서 파싱하는 단계부터 시작하기 때문에 아무래도 늦어질 수 밖에 없다. 
  - 인터랙션이나 속도가 중요한 웹사이트라면 CSS-in-JS보다는 CSS-in-CSS를 방식이 바람직하다. 