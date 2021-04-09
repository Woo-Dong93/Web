# Flex

- CSS의 flex는 엘리먼트들의 크기나 위치를 쉽게 잡아주는 도구입니다. 
- flex를 이용하면 레이아웃을 매우 효과적으로 표현할 수 있습니다. 
  - 예전에는 `table`을 사용해서 레이아웃을 구성하였다.
  - 문제점 : `table`은 정보를 정리정돈하기 위해 사용하는 것인데 의미가 없는 레이아웃으로 사용하다보니 검색엔진이나 스크린리더 등 html을 해석하는 S/W 입장에서는 표로 사용된 것인지 레이아웃으로 사용된 것인지 구분하기 어려웠다.
  - 또 `table`은 코드가 길어지면 복잡해지기 때문에 유지보수하기가 까다롭다.

```html
<container>
	<item></item>
	<item></item>
</containger>
```



- 사용방법
  - `display: flex;` : flex 선언하기
  - `flex-direction: row;` : flex 정렬 방법 선택하기( 가로, 세로, reverse ), 디폴트 값
    - `flex-direction: column`;
  - flex의 아이템들은 그 방향의 전체(100%)를 크기로 잡습니다.

```html
<!doctype>
<html>
<head>
    <style>
        .container{
            background-color: powderblue;
            height:200px;
            display:flex;
            flex-direction:row;
        }
        .item{
            background-color: tomato;
            color:white;
            border:1px solid white;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
</body>
</html>
```



- basis & grow
  - `flex-basis: 200px;` : flex 정렬된 방향으로 기본 크기 지정할 수 있습니다.
  - `flex-grow: 1` : 모든 아이템에게 부여하면 flex의 방향으로 일정한 비율을 통해 가득 채웁니다.
    - 기본값 : 0;
    - 만약 하나의 아이템에 `flex-grow: 2;`로 설정하면 나머지 조각은 1(1/6)의 비율을 가져가고 이 아이템은 2(2/6)의 비율을가져갑니다.

```html
<head>
    <style>
        .container{
            background-color: powderblue;
            height:200px;
            display:flex;
            flex-direction:row;
        }
        .item{
            background-color: tomato;
            color:white;
            border:1px solid white;
            flex-grow: 1
        }
        .item:nth-child(2){
            /* flex-basis: 200px; */
            flex-grow:2;
        }
    </style>
</head>
```



- shrink
  - 아이템들이 `flex-basis`값을 가지고 있을때 원래의 컨테이너 크기보다 작아졌을 때의 아이템의 크기는 자동으로 줄어들게 됩니다.
  - 기본적으로 `flex-basis`로 설정한 아이템이 혼자 부담하게 됩니다.
  - `flex-shrink: 1` 컨테이너의 크기가 작아질 때 적용된 아이템들은 공통분담하게 됩니다.
    - flex-shrink: 0 : 공통분담을 못하게 막습니다.

```css
// 아이템-1은 3/1만큼 공통분담, 아이템-2는 3/2만큼 공통분담(더 많이 줄어든다!)
.item:nth-child(1){
    flex-basis: 200px;
    flex-shrink: 1;
}
.item:nth-child(2){
    flex-basis: 200px;
    flex-shrink: 2;
}
```



### Flex 기타 속성

- container 속성

  - display
    - `display: flex;`
  - flex-direction
    - `flex-direction: row` (기본 값)
    - `flex-direction: row-reverse` 
    - `flex-direction: column` 
    - `flex-direction: column-reverse`
  - flex-wrap : 컨테이너가 더 이상 아이템들을 한 줄에 담을 여유 공간이 없을 때 줄바꿈 속성
    - `flex-wrap: nowrap;` (기본 값), 줄바꿈 되지 않습니다.
    - `flex-wrap: wrap;` 아이템 크키가 크다면 줄바꿈되어서 내려갑니다.
    - `flex-wrap: wrap-reverse;`
  - flex-flow : `flex-direction`과 `flex-wrap`을 한꺼번에 지정할 수 있습니다.
    - `flex-flow: row wrap;`
  - justify-content : **메인 축**(기준) 방향으로 정렬
    - `justify-content: flex-start;` 아이템들을 시작점으로 정렬합니다. (왼쪽, 위)
    - `justify-content: flex-end;` 아이템들을 끝점으로 정렬합니다. ( 오른쪽, 아래)
    - `justify-content: center; ` 아이템들을 가운데로 정렬합니다.
    - `justify-content: space-around;` 아이템들의 둘레에 균일한 간격이 생성됩니다.
    - `justify-content: space-between;` 아이템의 사이에 균일한 간격이 생성됩니다.
      - 양 끝은 여백이 없습니다.
    - `justify-content: space-evenly;  `양 끝까지 균일한 간격으로 만들어 줍니다.
      - 브라우저 IE와 Edge에서는 지원되지 않습니다.
  - align-items : 메인 축의 수직축 방향으로 정렬하는 속성입니다.
    - `align-items: stretch;` 수직축 방향으로 아이템들이 끝까지 쭈욱 늘어납니다.
    - `align-items: flex-start;`  시작점으로 정렬합니다. (수직 기준)
    - `align-items: flex-end;` : 끝으로 정렬합니다. (수직 기준)
    - `align-items: center;` :   수직축 기준으로 중간으로 정렬합니다.
    - `align-items: baseline;` : 텍스트 베이스라인 기준으로 정렬합니다.
  - 한 가운데 놓기
    - `justify-content: center; align-item: center;`

  - align-content :`flex-wrap: wrap;` 이 설정된 상태에서 아이템의 행이 2줄 이상 되었을 때 수직축 방향 정렬을 결정하는 속성입니다.
    - `justify-content`와 속성값 동일

- item 속성

  - order : 아이템들의 배치 순서 변경
    - 기본값 0, 음수는 왼쪽, 양수는 오른쪽으로감
    - order:0, order:1; oder;2
    - order:-1
    - html 자체의 구조를 변경하는 것이 아니기 때문에 스크린 리더로 화면을 읽을때에는 무시됩니다.
  - flex-grow : item들의 차지하는 비율 조정
    - `flex-grow: 0;` 기본값, 원래크기 유지
    - `flex-grow:1 ;` 여백없이 꽉채움, 모든 아이템이(다 넣으면), 부모가 커지면 자식도 같이 커진다.
  - flex-shrink
    - `flext-shrink: 0` 브라우저가 작아지더라도 크기가 자동으로 줄지 않습니다.
      - 부모가 작아저도 자식은 그대로 유지
    - `flex-shrink: 1` 공통 분담한다. (기본값)
    - `flex-shrink: 2` 공통분담의 크기가 더 커지는것, 3개면 3/2를 분담
  - flex-basis : Flex 아이템의 기본 크기를 설정합니다. (flex-direction이 row일 때는 너비, column일 때는 높이).
    - `flex-basis: 200px` 기본크기 설정, flex-direction의 방향에 따라 크기를 지정
    - 만약 설정한 값보다 콘텐츠 크기가 더크면 콘텐츠 크기를 따릅니다.
  - flex : `{flex: flex-grow flex-shrink flext-basis}` 축약
    - `flex: auto;`( 1 1 auto ) , 부모가 커지만 나도 커지고, 작아지면 나도 축소
    - `flex: 0 1 auto;`(기본값), 축소만 자동으로 되는 스타일
    - `flex: 1;` = flex: 1 1 0
    - `flex: 2;` = flex: 2 1 0
    - flex: none( 0 0 auto) : 확장되지도 않고, 축소되지도 않는다. 원래의 크기를 유지한다.
      - `margin-left: auto;` 특정 아이템을 가장 오른쪽에 위치시켜준다.
      - `margin-right: auto;`특정 아이템을 가장 왼쪽에 위치시켜준다.
      - `margin: 0 auto;`  특정 아이템을 가운데로 위치시켜줍니다.
      - `margin-top: auto;` 특정 아이템을 맨아래로 밀어줌 ( footer고정할때 사용 )
      - `margin-bottom:auto;`: 특정 아이템을 맨위 올려줌
  - align-self : 해당 아이템의 수직축 방향 정렬입니다.
    - 기본적으로 `align-items` 설정을 상속
  - z-index도 설정 가능합니다.

  

### 참고

- https://studiomeal.com/archives/197