# CSS 기본지식



### 1. CSS Selector(선택자) 우선순위

- !important > 인라인 스타일 속성 > 아이디 선택자 > 클래스/속성/가상 선택자 > 태그 선택자 > 전체 선택자
- 선택자 우선순위가 같다면 가장 마지막에 지정된 스타일이 우선 적용됩니다.
- ID 선택자 : HTML 문서에서 특정 ID 속성값은 오직 하나만 있어야 합니다.
-  Universal Selector ( 전체 선택자 )

```css
* {
  color: green;
}
```

- CSS 선택자 성능 순위

  - ID, e.g. #header
  - Class, e.g. .promo
  - Type, e.g. div
  - Adjacent sibling, e.g. h2 + p
  - Child, e.g. li > ul
  - Descendant, e.g. ul a
  - Universal, i.e. *
  - Attribute, e.g. [type="text"]
  - Pseudo-classes/-elements, e.g. a:hover
  - **클래스 나 ID가 아닌 유형을 선택하면 리플로우가 훨씬 느려집니다.**
  -  **ID와 Class 간의 속도 차이는 거의 없다고 보면 됩니다.**
  -  **css로 직접 태그 선택자를 잡는 것보다 클래스를 부여하는 편이 훨씬 더 성능이 좋습니다.**

  

