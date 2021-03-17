# Arrow Function

### 1. 소개

```js
// 기존 함수표현식

var a = function () {
  return new Date()
}
var b = function (a) {
  return a * a
}
var c = function (a, b) {
  return a + b
}
var d = function (a, b) {
  console.log( a * b )
}
```

```js
// Arrow Function 변환

let a = () => new Date()

//인자가 1개면 괄호도 생략 가능, return 값만 존재할 경우는 {}생략 가능
let b = a => a * a 

let c = (a, b) => a + b

let d = (a, b) => {
  console.log( a * b )
}

```

```javascript
var e = function (x) {
    return {
        x: x
    }
}

// 객체를 반환해야하는 경우는 중괄호가 에로우 함수의 스코프로 인식을 하게 됩니다.
// => 괄호로 감싸줘야 한다!
var e = (x) => {x: x}; // 에러

var e = (x) => ({x: x}); //x를 KEY와 VALUE로 하는 객체 반환

// 더 생략 가능
var e = x => ({x});
```

```javascript
// 클로저 축약

var f = function(a) {
    return function(b){
        a+b;
    }
}

var f = a => b => a+b; // var z = f(1)(2);
```



### 2. 상세

#### 1) (매개변수) => { 본문 }

#### 2) 매개변수가 하나뿐인 경우 괄호 생략 가능

#### 3) 매개변수가 없을 경우엔 괄호 필수

- `_`와 `$`은 변수명 앞글자로 사용 가능하다. ( 인자 안받을 때 관행적으로 사용 )
- `var b = _ => 10;` 

#### 4) 본문이 `return [식 or 값]` 뿐인 경우 `{ }`와 `return` 키워드 생략 가능

#### 5) 위 4) 에서 return할 값이 `객체`인 경우엔 괄호 필수

```js
// 에러 발생
const f = () => {
  a: 1,
  b: 2
}

// 정상 작동
const f = () => ({
  a: 1,
  b: 2
})
```

#### 6) 실행컨텍스트 생성시 this 바인딩을 하지 않음

- **에로우 함수**는 기존 함수의 기능을 보기 편하게 직관적으로 보여주기 위해 만든 것 보다는 함수를 라이트하게 가져가기 위해 만든 것이라고 볼 수 있습니다.
  - 함수를 실행할 때 다양한 것들이 많이 수행 됩니다. ( 실행 컨텍스트 등 )

```javascript
const obj = {
  a: function () {
    console.log(this) //this는 obj

    const b = function() {
      // 함수가 실행되는 순간 this를 바인딩, 없으니 전역객체를 바인딩
      console.log(this) //this는 window 
    }
    b();
    // 같은 this를 보게하려면 b.call(this)
  }
}

obj.a()
```

```js
const obj = {
  a: function () {
    console.log(this) //this는 obj

    const b = () => { 
      // 에로우 함수는 함수가 실행될 때 this를 바인딩하는 작업을 하지 않습니다.
      // 현재 자기는 this를 들고 있지 않기 때문에 외부스코프에서 찾게 됩니다.
      console.log(this) //this는 obj 
    }

    b()
  }
}

obj.a();
```

```js
// 블록스코프 : 함수스코프와 다르게 this 바인딩을 하지 않습니다. (상위를 그대로 사용합니다.)
// 그럼 에로우 함수도 블록스코프일까? => 아닙니다. (중요)

const a = () => {
    var x = 10;
}
a();
console.log(x); // Error 발생
// var는 블록스코프의 영향을 받지 않기 때문에 x가 출력되어야 합니다.
// 블록스코프면 x가 나오지만 함수스코프면 x가 안나온다. => 에러가 나온다. 
// 즉 에로우 함수는 기존 함수처럼 함수 스코프를 생성한다. 다만 실행 컨텍스트 생성시 this를 바인딩 하지 않는 것이 포인트!

/////
for(var i =0; i<10; i++){
}
console.log(i) 10;
////블록스코프는 살아잇다.


const obj = {
  grades: [80, 90, 100],
  getTotal: function () { // 이 함수안에서의 this : obj
    this.total = 0 
    this.grades.forEach(function(v) { 
// 이 함수는 콜백함수, 콜백함수는 제어권을 가진 함수가 정해주지 않으면 일반적으로 함수의 this와 동일 // 콜백함수안에서 this는 그냥 함수실행 => window
      this.total += v
    })
  }
}
obj.getTotal() //언디파인드
console.log(obj.total) // 출력 : 0'
// Window에 추가됩니다.
console.log(total) // NaN (undefind+80+90+100)
```

```javascript
var total = 0;
const obj = {
  grades: [80, 90, 100],
  getTotal: function () { 
    this.total = 0 
    this.grades.forEach(function(v) { 
      this.total += v  
    })
  }
}
obj.getTotal()
console.log(total) // 270
console.log(obj.total) // 0
```

```javascript
const obj = {
  grades: [80, 90, 100],
  getTotal: function () {}
    this.total = 0 
    this.grades.forEach(function(v) { //v =>
      this.total += v
    }, this)// 이런식으로 this넘길수 있다. 하지만 에로우함수를 활용하면 더 간편하게 할 수 있다.
  }
}
console.log(obj.total) // 270

// 에로우 함수 활용
const obj = {
  grades: [80, 90, 100],
  getTotal: function () {}
    this.total = 0 
    this.grades.forEach( v => { //v =>
      this.total += v
    })
  }
}
console.log(obj.total) // 270
```



#### 7) 명시적 this 바인딩 ?

- this가 바인딩되지 않기 때문에 this를 변경 불가능합니다.

```js
const a = () => {
  console.log(this)
}
a(); // window

a.call({a: 1}) // this : window

const c = function() {
  console.log(this)
}
c();

c.call({a: 1}) // this : {a:1}
```

```js
// 그러면 call or apply가 동작하지 않는 것인가?
// 동작은 제대로 하고 있는 것이다. 하지만 this만 바인딩하지 않는 것일 뿐...

const a = (...rest) => {
  console.log(this, rest)
}
a.call({a: 1}, 1, 2, 3) // window + [1,2,3]
a.apply([], [4, 5, 6]) // window + [4,5,6]

// 그래서 애초에 this를 넘겨줘도 바인딩을 못하니 null or undefind를 넘겨주자!
const b = a.bind(null, 7, 8, 9, 10)
b() // window + [7,8,9,10]
```

```js
const obj = {
  f() {
    const a = (...rest) => {
      console.log(this, rest)
    }
    a.call({a: 1}, 1, 2, 3)
    a.apply([], [4, 5, 6])
    const b = a.bind(null, 7, 8, 9, 10)
    b()
  }
}
obj.f()
// obj, [1, 2, 3]
// obj, [4, 5, 6]
// obj, [7, 8, 9 ,10]
```

#### 8) 생성자함수로 ?

- 두 함수의 구조를 보시면 차이점이 있습니다.
  - 에로우 함수 : arguments와 caller는 숨겨져 있고 invoke해야만 값을 얻을 수 있다. 또한 직접 실행하면 실행시점이 아니기 때문에 에러 발생, **프로토타입**도 존재하지 않습니다.

```javascript
function sum = (...arg) {
    console.log(this);
    return arg.reduce((p,c) => p+c);
}

const sum2 = (...arg) => {
    console.log(this);
    return arg.reduce((p,c) => p+c);
}

const b = new sum() // 가능 => sum {} 빈객체 만들어짐
const c = new sum2() // 오류
```

- concise method와 arrow function의 공통점
  - **prototype** 프로프티가 없다 => 생성자함수로 사용할 수 없다.
  - arguments, caller가 숨겨져 있고 invoke해야만 값을 얻을 수 있다.
  - 차이점은 **method**는 메소드로만 사용 가능, 함수로 사용 x
  - **arrow**는 함수로서의 기능(this가 객체를 바라볼 수 없음)에 충실 =  (그냥 객체에서 함수선언)
    - 물론 **arrow 함수**를 메소드로 사용할 수 있지만 this를 바인딩 하지 않으니 활용할 수 없는 부분이 많으니 **arrow 함수**를 사용할 이유가 없다.

```javascript
const b = {
    name = '하하',
    bb(){
        return this.name;
    },
    a: x=>{
        return this.name;
    }
}
b.bb() => 하하
b.a(); => '' // window.name 실제로 존재
```

- 꼭 에로우 함수를 메소드로 사용하고 싶으면 ...

```javascript
const b = {
    name = '하하',
    bb(){
        // 메소드 안의 내부함수로 활용할 때...
         const b = x =>{
        	return this.name;
    	}
        b();
    },
   
}
b.bb(); // '하하'
```




#### 9) 그밖에

this 외에도 super, arguments, new.target 등을 바인딩하지 않는다.