# CSS Transition

- 전환은 효과(**css의 여러가지 효과들, 속성들의 값들이 변경**)가 변경되었을 때 부드럽게 처리해주는 CSS의 기능입니다. 이와 관련된 것으로는 아래와 같은 속성들이 있습니다. 
  - transition-duration
    - `transition-duration: 1s` : 전환이 1초동안에 거쳐서 일어난다.
  - transition-property : 어떤 효과에 전환을 줄 것인지 선택하기, 띄어쓰기로 구분
    - `transition-property: all` : 해당 태그의 모든 효과에 대해서 변화가 일어났을 때 전환이 일어난다는 의미
  - transition-delay : 효과를 지연하고 싶을 때 사용한다.
    - `transition-delay: 1s`: 1초뒤에 효과가 진행된다.
  - transition-timing-function : transition이 일어날 때의 속도를 개발자 마음대로 조정할 수 있습니다.
  - transition : 함축적으로 사용할 수 있는 속성입니다.
    - `transition: property timing-function duration delay | initial | inherit`
    - `transition-property ` + `transition-duration`
    - `transition: font-size 1s, transform 0.1s;`
    - **initial :** 기본값으로 설정합니다.
    - **inherit :** 부모 요소의 속성값을 상속받습니다.

```html
<!doctype html>
<html>
<head>
  <style>
    a{
      font-size:3rem;
      display:inline-block;
	  /*	
      transition-property: font-size transform;
      transition-duration: 0.1s;
      transition:all 0.1s;
	  */	
      transition:all 0.1s;
      transition-delay: 1s;
    }
    /* 사용자가 클릭했을 때 */
    /* transform은 block or lnline-block 이여야 동작한다. */  
    /* translate : x축, y축으로 이동 */
    a:active{
      transform:translate(20px, 20px);
      font-size:2rem;
    }
  </style>
</head>
<body>
  <a href="#">Click</a>
</body>
</html>
```



- `transition-timing-function`
  - `transition-timing-function: ease` : 기본 값
  -  css에서 제공하지 않는 것들은 **ceaser**에서 가져다 사용하면 됩니다.

```html
<!doctype html>
<html>
<head>
  <style>
    body{
      background-color: black;
      transition:all 1s;
    }
    div{
      background-color: black;
      color:white;
      padding:10px;
      width:100px;
      height:50px;
      -webkit-transition: all 500ms cubic-bezier(0.680, 0, 0.265, 1); /* older webkit */
      -webkit-transition: all 500ms cubic-bezier(0.680, -0.550, 0.265, 1.550); 
         -moz-transition: all 500ms cubic-bezier(0.680, -0.550, 0.265, 1.550); 
           -o-transition: all 500ms cubic-bezier(0.680, -0.550, 0.265, 1.550); 
              transition: all 500ms cubic-bezier(0.680, -0.550, 0.265, 1.550); /* easeInOutBack */
 
      -webkit-transition-timing-function: cubic-bezier(0.680, 0, 0.265, 1); /* older webkit */
      -webkit-transition-timing-function: cubic-bezier(0.680, -0.550, 0.265, 1.550); 
         -moz-transition-timing-function: cubic-bezier(0.680, -0.550, 0.265, 1.550); 
           -o-transition-timing-function: cubic-bezier(0.680, -0.550, 0.265, 1.550); 
              transition-timing-function: cubic-bezier(0.680, -0.550, 0.265, 1.550); /* easeInOutBack */
    }
    div:hover{
      height:400px;
    }
  </style>
</head>
<body onload="document.querySelector('body').style.backgroundColor='white';">
  <div>
    TRANSITION
  </div>
</body>
</html>
```

