# template literal (문자열)



### 1. 소개

```javascript
//1. 작은 따옴표
var a = 'abc';

//2. 큰 따옴표
var b = "abc";
// => 이런 선언 방식을 String literal(글자 그대로의) 선언 방식

//3. 백틱
var c = `abc`;
a === b
a === c
b === c
//=> 이런 선언 방식을 template literal 선언 방식
```

```javascript
//기존의 문자열의 줄바꿈 : '\n 활용'
var a = 'abc\n' +
    'ddf'

//백틱을 활용하면 엔터로 대체 가능
console.log(`a
bb
ccc`)

//공백도 문자로 취급한다.
console.log(`a
 bb 
 ccc`)
```

```javascript
const a = 10
const b = 20
const strBefore = a + "+" + b + "=" + (a+b);
//백틱 사이에 ${} 값이나 식이 올 수 있음
const str = `${a} + ${b} = ${ a + b }` 
console.log(str)// 10 + 20 = 30

//$를 표시하고 싶다면 하나 더쓰면 된다.
const a = `$${a+b}`
concole.log(a) // $30
```

#### - 특징 -

#### 1. backtick (`)

#### 2. multi-line = 알아서 스페이스써도 된다.

#### 3. string interpolation = ${} = 보간법



### 2. Details

- multi-line의 경우 들여쓰기에 주의

```js
const f = function () {
  const a = `abc
  def
  ghij`
  console.log(a)
}
f()
// 결과가 이쁘지 않다.
/* abc   
     def 
     ghij */

const f = function () {
  const a = `abc\n`+
  `def\n`+
  `ghij`
  console.log(a)
}
//abc 
//def 
//ghij
```

- ${ } 내에는 `값` 또는 `식`이 올 수 있다.

```js
const counter = {
  current: 0,
  step: 1,
  count: function() { return this.current += this.step },
  reset: function() { return this.current = 0 }
}
console.log(`${counter.count()} ${counter.count()}
${counter.reset()} $${counter.count()}
${counter.count()}$`)
```

- 결국 문자열이므로, 자동으로 toString 처리가 된다.

```js
//자동으로 배열의 tostring()이 호출됩니다.
console.log(`${[0, 1, 2]}`) // 0,1,2
console.log(`${{a:1, b:2}}`) // [object Object]
console.log(`${function(){ return 1 }}`) // 함수 그 자체 
/* function () {
    return 1;
  } */

//문자열 암묵적형변환
console.log(`${(() => 1 )()}` + 1) == (function(){return 1;})() //11 
```

- 중첩된 backtick 처리

```js
// console.log(`Foo `Bar``) => 문법 오류
console.log(`Foo ${`Bar`}`) // Foo Bar
console.log(`Foo ${`Bar ${`Baz`}`}`) // Foo Bar Baz
```

- 가독성을 위해 trim 처리

```js
function a () {
  return `
<div>
    <h1>Lorem ipsum.</h1>
</div>
  `.trim() // 앞과 뒤의 줄바꿈과 공백없앰
}
console.log(a())
console.log(a().replace(/\n/g, '')) // <div>    <h1>Lorem ipsum.</h1></div>
```

```js
//jsp, php, asp 등... => template language or template engine or template library
//var a = 'name'
//<div class="%a%"></div>

//자바스크립트에서도 템플릿 엔진을 흉내낼 수 있다.
const linesToHTML = function (characters) {
  return characters.reduce(function (charactersResult, character) {
    let {name, lines} = character
    return `${charactersResult || ''}
<article>
  <h1>${name}</h1>
  <ul>
    ${lines.reduce(function (linesResult, line) {
      return `${linesResult || ''}
    <li>${line}</li>
      `.trim()}, 0)}
  </ul>
</article>
  `.trim()}, 0)
}
const characters = [{
  name: 'Aria Stark',
  lines: ['A girl has no name.']
}, {
  name: 'John Snow',
  lines: [
    'You know nothing, John Snow.',
    'Winter is coming.'
  ]
}]
document.body.innerHTML = linesToHTML(characters)
```



### 3. 번외 - forEach, map, reduce(es5에서 등장)

- 배열의 모든 메소드의 인자는 **중요한 순서**로 나열되어 있습니다.
- 앞에 있을 수록 중요도가 높다는 뜻입니다.

#### 1) forEach : for문 편하게 돌리기

[MDN - Array.prototype.forEach](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

`Array.prototype.forEach(callback[, thisArg])` (메타표기법 : []생락가능)

- `callback`: `function (currentValue[, index[, originalArray]])` // 콜백은 반드시 함수여야하고..
  - `currentValue`: 현재값
  - `index`: 현재 인덱스
  - `originalArray`: 원본 배열
- `thisArg`: this에 할당할 대상. 생략시 global객체 or window 객체

```js
const a = [ 1, 2, 3 ]
a.forEach(function (v, i, arr) {
    console.log(v, i, arr, this)
}, [ 10, 11, 12 ])
// 1, 0 [1, 2, 3] [10, 11, 12]
// 2, 1 [1, 2, 3] [10, 11, 12]
// 3, 2 [1, 2, 3] [10, 11, 12]
```



#### 2) map : for문을 돌려서 배열을 새로운 배열을 만드는게 목적, return 필수

[MDN - Array.prototype.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

`Array.prototype.map(callback[, thisArg])`

- `callback`: `function (currentValue[, index[, originalArray]])`
  - `currentValue`: 현재값
  - `index`: 현재 인덱스
  - `originalArray`: 원본 배열
- `thisArg`: this에 할당할 대상. 생략시 global객체

```js
const a = [ 1, 2, 3 ]
const b = a.map(function (v, i, arr) {
    console.log(v, i, arr, this)
    return this[0] + v
}, [ 10 ])

// 콜백함수가 3번 실행되면서 새로운 배열을 만듭니다.
// [11, 12, 13]
```



#### 3) reduce : for문을 돌려서 최종적으로 다른 무언가를 만드는 목적, return 필수

[MDN - Array.prototype.reduce](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

`Array.prototype.reduce(callback[, initialValue])`

- `initialValue`: 초기값. 생략시 첫번째 인자가 자동 지정되며,  
  이 경우 currentValue는 두번째 인자부터 배정된다.
- `callback`: `function (accumulator, currentValue[, currentIndex[, originalArray]])`
  - `accumulator`: 누적된 계산값
  - `currentValue`: 현재값
  - `currentIndex`: 현재 인덱스
  - `originalArray`: 원본 배열

```js
const arr = [ 1, 2, 3 ]
const res = arr.reduce(function (p, c, i, arr) {
  console.log(p, c, i, arr, this)
  return p + c
}, 10)
// 10 1 0
// 11 2 1
// 13 3 2
// res = 16 ( 10+1+2+3 )

// 처음에는 p에 10이 들어온다. ( c에는 1, 인덱스는 0 )
// 10 1 0 => p+c(11)이 두번째 accumulator의 p로 들어갑니다.
// 11 2 1
// 13 3 2
// 최종 결과 : 16

const arr = [ 1, 2, 3 ]
const res = arr.reduce(function (p, c, i, arr) {
  console.log(p, c, i, arr, this)
  return p + c
})
// initialValue가 없으면 p에 자동으로 첫번째 인덱스의 값1이들어가거 순회를 2번째부터 합니다.
// 1 2 1
// 3 3 2
//  최종 결과 : 6
```

```js
const arr = [ 1, 2, 3, 4 ]
const str = arr.reduce(function (res, item, index, array) {
  return res + item
}, '')
console.log(str)
```

|  step  |  res   | item | index |   array   |
| :----: | :----: | :--: | :---: | :-------: |
|   1    |   ''   |  1   |   0   | [1,2,3,4] |
|   2    |  '1'   |  2   |   1   | [1,2,3,4] |
|   3    |  '12'  |  3   |   2   | [1,2,3,4] |
|   4    | '123'  |  4   |   3   | [1,2,3,4] |
| result | '1234' |      |       |           |

```js
//문자열도 만들 수 있다.
const arr = [ 'a', 'b', 'c', 'd' ]
const str = arr.reduce(function (res, item, index, array) {
  return res + item
})
console.log(str) //abcd

//객체도 만들 수 있다.
const arr = [ 'a', 'b', 'c', 'd' ]
const str = arr.reduce(function (res, item, index, array) {
  res[item] = item //a.x = 'a' 이랑 같은 것
  return res;
}, {})
console.log(str) //{ a: 'a', b: 'b', c: 'c', d: 'd' }
```

|  step  |  res   | item | index |       array       |
| :----: | :----: | :--: | :---: | :---------------: |
|   1    |  'a'   | 'b'  |   1   | ['a','b','c','d'] |
|   2    |  'ab'  | 'c'  |   2   | ['a','b','c','d'] |
|   3    | 'abc'  | 'd'  |   3   | ['a','b','c','d'] |
| result | 'abcd' |      |       |                   |

```js
const arr = [ 10, 20, 30, 40, 50 ]
const r = arr.reduce(function (p, c) {
  return p + c
})
console.log(r) //150
```

```js
// 화살표 함수로 더 최적화
const arr = [ 10, 20, 30, 40, 50 ]
const r = arr.reduce((p, c) => p + c)
console.log(r)//150
```



### 4. template tag function

- 문자열 앞에서 그냥 그 함수이름을 적어주고 **템플릿 리터럴**을 넘겨주면 첫번째 인자에는 순수한 문자열만 들어있는 배열, 그 뒤에는 보간된 값들을 하나하나 넘겨줍니다.
- 무조건 문자열이 interpolation(보간법)보다 한개 더 많습니다.

```js
//일반적인 함수
const tag = function (strs, arg1, arg2) {
  return {strs: strs, args: [arg1, arg2]} 
}

const res = tag `순서가 ${1}이렇게 ${2}` 
console.log(res) // 출력 : { strs: [ '순서가 ', '이렇게 ', '' ], args: [ 1, 2 ] }

//...args는 나머지연산자 => 나머지 인자를 전부 배열로만들어줌
const tag2 = function (strs, ...args) {
  return {strs: strs, args}
}
const res = tag2 `순서가 ${1}이렇게 ${2}` 
const res2 = tag2 `${1}이렇게 ${2}` 
console.log(res) // 출력 : { strs: [ '순서가 ', '이렇게 ', '' ], args: [ 1, 2 ] }
console.log(res2) // 출력 : { strs: [ '', '이렇게 ', '' ], args: [ 1, 2 ] }
```

```js
const tags = function (strings, ...expressions) {
  console.log(strings, expressions)
}
const a = 'iu', b = 'Friday'
const str = tags `Hello, ${a}! Today is ${b}!!`
// ["Hello, ", "! Today is ", "!!"]
// ["iu", "Friday"]
```



#### 1) expression의 수는 언제나 string의 수보다 하나 적다!

```js
const tags = function (strs, ...exps) {
  return { strs, exps }
}
console.log(tags `${10}${20}`) //{ strs: [ '', '', '' ], exps: [ 10, 20 ] }
console.log(tags `a${30}`) //{ strs: [ 'a', '' ], exps: [ 30 ] }
console.log(tags `${40}b`) //{ strs: [ '', 'b' ], exps: [ 40 ] }
```



#### 2) 이를 이용하면 strings 또는 expressions 중 하나를 순회하여 별도의 처리가 가능하다.

```js
// 문자얼만 가지고 순회, 문자열만 특수한 문자열(_suffix )을 더해준다. => 문자열 변형 가능
const addSuffix = function (strs, ...exps) {
  return strs.reduce(function (acc, curr, i) {
    let res = acc + curr + '_suffix '
    if(exps[i]) res += exps[i]
    return res
  }, '')
}

console.log(addSuffix `이 함수는${'각 문자열'}마다${'|_suffix|'}라는 글자를 추가합니다.`)
// 출력 : 이 함수는_suffix 각 문자열마다_suffix |_suffix|라는 글자를 추가합니다._suffix
```



#### 3) examples ( 실무 적용 )

```js
const setDecimalSeperators = function (strs, ...args) {
  return args.reduce(function (p, c, i) {
    return p + strs[i] + (c + '').replace(/\d{1,3}(?=(\d{3})+(?!\d))/g, '$&,')
  }, '') + strs[strs.length - 1]
}
// 보간법만 변형
const res = setDecimalSeperators `이 사과는 하나에 ${2000}원이고, 총 ${1234567}개를 구입하시면 총 ${2000 * 1234567}원 이에요.`
console.log(res) 
// 출력 : 이 사과는 하나에 2,000원이고, 총 1,234,567개를 구입하시면 총 2,469,134,000원 이에요.
```

```js
// 객체는 a.b=1로 그냥 프로퍼티만들 수 있는데 map객체는 set이라는 메소드를 써서 정해진 규칙으로 추가해야 한다. 
// 이것을 편하게 하고자 직접 구현해볼 수 있다.
const createCollection = {
  Map(keys, ...vals){
    const m = new Map()
    vals.forEach(function (val, i) {
      m.set(keys[i].trim(), val)
    })
    return m
  },
  WMap(keys, ...vals){
    const wm = new WeakMap()
    for (let i = 0 ; i < vals.length ; i+=2) {
      wm.set(vals[i], vals[i+1])
    }
    return wm
  },
}

const wkeys = [ {a : 100}, {b : 200} ]
const map = createCollection.Map `
  a ${10}
  b ${'what'}
  fn ${v => v + 10}`
let wmap = createCollection.WMap `
  ${wkeys[0]} ${10}
  ${wkeys[1]} ${20}`
console.log(map) // Map { 'a' => 10, 'b' => 'what', 'fn' => [Function] }
console.log(wmap)
```



### 5. `String.raw`

- `tag` 함수를 돌린 결과를 열어보면  문자열만 담은 배열에 `raw`라는 프로퍼티가 존재합니다.
  - **이스케이프 문자**( 엔터 등 )를 그대로 표시해줍니다.
- `String.raw`는 String 함수의 static 메소드(내장 메소드) 입니다.

```js
//이스케이프 문자를 원본그대로..=>raw라는 프로퍼티에 들어간다.(tag 쓰면)
console.log(`Hello\nWorld!`)
//Hello
//World!

console.log(String.raw `Hello\nWorld!`) // Hello\nWorld!

console.log(String.raw `Hello
World!`)
//Hello
//World!
```

```js
const tags = function (strs, ...exps) {
  return { strs, exps } 
}
const a = 'iu', b = 'Friday'
const str = tags `Hello, ${a}\n Today is ${b}\n`
```

