# Optional Chaining

-  ES2020에서 추가된 문법인 `?.` 입니다.
- 그동안 자바스크립트에서는 주로 `.` 연산자(chaining)를 사용해서 객체의 속성값에 접근했었습니다.
- 하지만 존재하지 않은 프로퍼티를 탐색할 때 그 깊이가 깊을 때 `TypeError`가 발생한다.

```js
user = {name: {first: "John", last: "Doe"}}
user.address.street
// Uncaught TypeError: Cannot read property 'street' of undefined
```

- 이를 방지하기 위해 이렇게 구현이 가능했다.

```js
user.address && user.address.street
undefined
```



### ?. 연산자를 통한 안전한 속성갑 접근

```js
user = {name: {first: "John", last: "Doe"}}
user?.name?.first
//'John'
user?.address?.street
//undefined
```



### 배열나 함수도 접근 가능합니다.

```js
arr = null;
arr?.[0]
//undefined

func = undefined
func?.()
//undefined
```



### 장점

- 옵셔널 체이닝을 사용하면 외부 API를 활용해서 데이터를 가져올때 에러를 발생시키지 않고 `undefind`나 `null`를 통해 분기처리 및 에러처리를 쉽게 할 수 있습니다.



### 마치며

- 2020년 현재 대부분의 최신 브라우저는 optional chaining을 지원하기 때문에 `?.` 연산자를 사용할 수 있습니다. 
- Node.js의 경우 버전 14부터 지원하며, 그 이전 버전에서는 [Babel](https://www.daleseo.com/?tag=Babel)과 같은 트랜스파일러(transfiler)를 통해서 접해볼 수 있다.



### 참고

- https://www.daleseo.com/js-optional-chaining/