# CSS Transition

- ```
  transition: property timing-function duration delay | initial | inherit
  ```

- **property :** transition을 적용시킬 속성을 정합니다. [transition-property](https://www.codingfactory.net/10946)를 참고하세요.
- **timing-function :** transition의 진행 속도를 정합니다. [transition-timing-function](https://www.codingfactory.net/10942)를 참고하세요.
- **duration :** transition의 총 시간을 정합니다. [transition-duration](https://www.codingfactory.net/10949)을 참고하세요.
- **delay :** transition의 시작을 연기합니다. [transition-delay](https://www.codingfactory.net/10951)를 참고하세요.
- **initial :** 기본값으로 설정합니다.
- **inherit :** 부모 요소의 속성값을 상속받습니다.

```
<!doctype html>
<html lang="ko">
	<head>
		<meta charset="utf-8">
		<title>CSS</title>
		<style>
			.jb {
				box-sizing: border-box;
				width: 64px;
				height: 64px;
				margin: 10px 0px;
				background-color: orange;
				border-radius: 100%;
				transition: all ease 2s 0s;
			}
			input:checked ~ .jb {
				width: 100%;
				height: 200px;
				border-radius: 0;
				background-color: red;
			}
		</style>
	</head>
	<body>
		<input type="checkbox">
		<div class="jb"></div>
	</body>
</html>
```

