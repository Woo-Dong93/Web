# for ..in 과 for ..of

- 둘 다 반복이 가능한 객체의 모든 원소를 하나씩 추출하여 변수에 담아 반복문을 수행하는 문법입니다.



### 1. for ..in

- Iterable하지 않은 객체까지 속성을 모두 열거할 수 있게 도와주는 페이크형태로 만들어진 문법입니다.
- 프로토타입체인에 있는 것까지 나오기 때문에 최상위 객체에 프로토타입을 추가하면 의도하지 않게 for ..in문에 의해 출력됩니다.

```javascript
let a = { a: 1, b: 2 };
for (let b in a) {
  console.log(b); //a, b
}
```





### 2. for ..of

- Iterable object만 사용할 수 있으며 프로토타입 체인에 의한 Iterable은 반복 대상이 제외됩니다.
  - `[Symbol.iterator]` 필수

```javascript
let arr = [1,2,3,4,5]

console.log("[  for of  ]")
for(let value of arr){
    console.log(value)
}
```

- Iterable하지 않은 객체를 사용하고 싶으면 `Object.keys()`를 통해 key값을 배열에 담고 돌립니다.

