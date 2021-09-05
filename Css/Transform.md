# Transform

- 요소에 이동(translate), 회전(rotate), 확대축소(scale), 비틀기(skew) 효과를 부여하기 위한 함수를 제공
- 단 애니메이션 효과를 제공하지는 않기 때문에 정의된 프로퍼티가 바로 적용되어 화면에 표시 
- 트랜스폼은 애니메이션 효과를 위해 사용하여야 하는 것은 아니지만 애니메이션 효과를 부여할 필요가 있다면 트랜지션이나 애니메이션과 함께 사용
- **CSS3 애니메이션 관련 속성**들이며 GPU가속을 이용하는 속성을 사용해서 더 빠른 애니메이션 처리

| transform function    | 설명                                                         |     단위      |
| :-------------------- | :----------------------------------------------------------- | :-----------: |
| translate(x,y)        | 요소의 위치를 X축으로 x만큼, Y축으로 y만큼 이동시킨다.       | px, %, em 등  |
| translateX(n)         | 요소의 위치를 X축으로 x만큼 이동시킨다.                      | px, %, em 등  |
| translateY(n)         | 요소의 위치를 Y축으로 y만큼 이동시킨다.                      | px, %, em 등  |
| scale(x,y)            | 요소의 크기를 X축으로 x배, Y축으로 y배 확대 또는 축소 시킨다. |   0과 양수    |
| scaleX(n)             | 요소의 크기를 X축으로 x배 확대 또는 축소 시킨다.             |   0과 양수    |
| scaleY(n)             | 요소의 크기를 Y축으로 y배 확대 또는 축소 시킨다.             |   0과 양수    |
| skew(x-angle,y-angle) | 요소를 X축으로 x 각도만큼, Y축으로 y 각도만큼 기울인다.      | +/- 각도(deg) |
| skewX(x-angle)        | 요소를 X축으로 x 각도만큼 기울인다.                          | +/- 각도(deg) |
| skewY(y-angle)        | 요소를 Y축으로 y 각도만큼 기울인다.                          | +/- 각도(deg) |
| rotate(angle)         | 요소를 angle만큼 회전시킨다.                                 | +/- 각도(deg) |

```css
/* 변환함수를 프로퍼티값으로 쉼표없이 나열 => 나열순서에 따라 차례대로 효과가 적용 */
transform: func1 func2 func3 ...;
```

- 예시 코드

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      .box {
        width: 95px;
        height: 95px;
        line-height: 95px;
        color: white;
        text-align: center;
        border-radius: 6px;
      }
      .original {
        margin: 30px;
        border: 1px dashed #cecfd5;
        background: #eaeaed;
        float: left;
      }
      .child {
        background: #2db34a;
        cursor: pointer;
      }
      .translate {
        transform: translate(10px, 50px);
      }
      .scale {
        transform: scale(0.75);
      }
      .skew {
        transform: skew(5deg, -20deg);
      }
      .rotate {
        transform: rotate(70deg);
      }
      .complex {
        transform: scale(0.5) rotate(20deg);
      }

      /* Animation Effect */
      .translate:hover {
        transition: transform 1s linear;
        transform: translate(0px, 0px);
      }

      .scale:hover {
        transition: transform 1s linear;
        transform: scale(1);
      }
      .skew:hover {
        transition: transform 1s linear;
        transform: skew(0, 0);
      }
      .rotate:hover {
        transition: transform 1s linear;
        transform: rotate(0);
      }
      .complex:hover {
        transition: transform 1s linear;
        transform: scale(1) rotate(0);
      }
    </style>
  </head>
  <body>
    <div class="original box">
      <div class="child box translate">translate</div>
    </div>
    <div class="original box">
      <div class="child box scale">scale</div>
    </div>
    <div class="original box">
      <div class="child box skew">skew</div>
    </div>
    <div class="original box">
      <div class="child box rotate">rotate</div>
    </div>
    <div class="original box">
      <div class="child box complex">complex</div>
    </div>
  </body>
</html>

```



## 참고 사이트

- https://poiemaweb.com/css3-transform
- https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions



