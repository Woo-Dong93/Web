# RequestAnimationFrame (raf)

- 자바스크립트에서 애니메이션을 구현할 때 효율적으로 개발할 수있도록 도와주는 API
- 애니메이션 등 타이머 함수를 사용할때 사용합니다. => 보통 1초에 60프레임 애니메이션 구현
  - 1개의 단일 프레임은 16ms(1,000ms/60frame)안에 수행해야 합니다. 
- 방법 1 : setInterval

```js
setInterval(function() { 
	// 로직
}, 1000/60);
```

- 방법 2 :`requestAnimationFrame(반복할 함수)`
  - 이 함수는 기본적으로는 1초에 60번, 보통은 모니터에 주사율에 맞추어 함수를 실행하게 되어있습니다. 
  - 스스로 계속 호출하지 않기 때문에 재귀로 구현해야 합니다. (영원히 움직인다 => 분기로 멈춰줘야 함)

```js
(function repeatOften() { 
    // 애니메이션 실행 코드 
    requestAnimationFrame(repeatOften); 
})();

```

- 취소하기

```js
myReq = requestAnimationFrame(callback);
cancelAnimationFrame(myReq);
```



### setInterval보다 requestAnimationFrame이 더 좋은 이유

- 브라우저가 **프레임 생성 초기 단계에** 맞춰 애니메이션 코드를 실행시킴으로써 애니메이션이 더 부드럽게 동작한다.  (FPS 보장)
- 지연을 방지하고 가장 최적화된 타이밍에 콜백 함수를 실행하는 **비동기 함수**이다.
  - setInterval이나 setTimeout은 프레임을 신경쓰지 않고 동작한다. ( 리페인트, 리플로우 과정 등)
- 만약에 애니메이션 코드가 엄청 복잡해서 실행하는데 **50ms**가 걸린다고 해보자. 그럼 **16.6ms**동안 프레임을 찍어내지 못했기 때문에 화면이 뚝뚝 끊기는듯한 현상이 발생한다.





# CSS 애니메이션 VS JS(JavaScript) 애니메이션

- 웹사이트에서 애니메이션 효과를 부여할 때 CSS의 `transition`/`animation` 속성을 사용할 수 있고 JS(JavaScript)의 `setInterval()`/`requestAnimationFrame()` 을 사용할 수 있습니다, 



### 1. CSS 애니메이션

- 일반적으로, 마우스를 올렸을 때 혹은 메뉴 버튼의 전환과 같은 간단하게 처리하는 애니메이션의 경우 CSS로 처리할 수 있습니다. 
- 이를 JS(JavaScript)로 구현하기 위해선 `setInterval`을 통해서 계속해서 `style.top`과 `style.left` 속성을 변화시켜줘야 합니다.
  - 이 속성은 브라우저의 렌더링 과정 reflow(layout) 단계를 발생시키기 때문에 애니메이션 부자연스럽게 끊기는 듯한 느낌을 받게 됩니다. 
- 반응형으로 애니메이션을 구현하기에 유용한데, 미디어 쿼리로 애니메이션을 적용하면 됩니다.
- 메인 쓰레드가 아닌 별도의 컴포지터 쓰레드(Compositor Thread)에서 그려지기 때문에 메인 쓰레드에서 작업하는 JS보다 효율적입니다.



### 2. JS(JavaScript) 애니메이션

- CSS로 처리하기에는 훨씬 복잡하고 무거운 애니메이션 작업들을 효율적이고, 세밀하게 다루기 위해서 사용하고 있습니다. 
- 바닐라 자바스크립트로 구현할 경우 위에서 살펴본 바와 같이 계속해서 요소의 위치를 재계산하기 때문에 비효율적이며 사용자 눈에 가장 부드러운 60fps가 유지되지 않습니다. 
- 이 때문에 RAF(RequestAnimationFrame) API가 등장했고 구현방식은 동일하지만 60fps를 보장할 수 있게 되었습니다.
- 최근에 Web Animations API가 나오기도 했는데 현재(2020년 4월 28일) 기준으로 지원하는 브라우저가 현저히 적기 때문에 아직까진 기존의 방법들이 더 높은 생산성을 가진다고 할 수 있습니다. 
- 요소의 스타일이 변하는 순간마다 제어할 수 있기 때문에 애니메이션의 세밀한 구성이 가능해집니다.
- 브라우저 호환성 측면에서 `transition`/`animation` 속성보다 뛰어납니다.
- GPU를 통한 하드웨어 가속을 제어할 수 있습니다. 이는 CSS의 특정 속성으로 인한 가속을 막아주는데, 하드웨어 가속이 모바일에서 성능저하를 발생시킬 수 있기 때문에 이런 면에선 좋습니다.





### 참고

- https://velog.io/@hyun_sang/CSS-%EC%95%A0%EB%8B%88%EB%A9%94%EC%9D%B4%EC%85%98-VS-JSJavaScript-%EC%95%A0%EB%8B%88%EB%A9%94%EC%9D%B4%EC%85%98