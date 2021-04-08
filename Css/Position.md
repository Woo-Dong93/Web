# Position

- 엘리먼트의 위치를 지정하는 4가지 방법이 있습니다.

- static
- relative
- absolute
- fixed
- 또한 `top`, `bottom`, `left`, `right` 를 통해 해당 엘리먼트의 위치를 조정할 수 있다.



### 1. static vs relative

- static : position의 디폴트 값입니다. 차례대로 왼쪽에서 오른쪽, 위에서 아래로 쌓입니다.
  - 오프셋이 작동하지 않습니다.
- relative : `top`, `bottom`, `left`, `right` 을 사용해서 위치 조절이 가능해집니다.



### 2. absolute

- absolute는 **position: static 속성을 가지고 있지 않은 부모를 기준**으로 움직입니다. 만약 부모 중에 포지션이 relative, absolute, fixed인 태그가 없다면 가장 위의 태그(body)가 기준이 됩니다.
- 부모와 링크가 끊기면 크기도 content크기로 바뀌게 됩니다. **( wideth 100% 해제 )**



### 3. fixed

- 스크롤에서 독립적으로 위치를 지정합니다.
- 스크롤을 내려도 그 자리를 계속 유지합니다. 바로 포지션이 fixed로 설정되어 있기 때문입니다.
- 크기도 content크기로 바뀜 ( width와 height를 따로 정해야 합니다. )