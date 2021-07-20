# Call by value vs Call by reference



### Call by value

- 매개변수를 주어진 값을 복사하여 전달하는 방식으로 메소드 내에서 변경한 값은 메소드 밖의 변수에 영향을 주지 않습니다.
- a와 b를 바꾸는 함수를 실행했어도 출력을 하면 a와 b가 그대로 출력됩니다.

```c
void swap(int a, int b)
{
    int t = a;
    a = b;
    b = t;
}

int main()
{
    int a = 1;
    int b = 2;
    swap(a, b); 
    cout << a << " , "<< b << endl; //1, 2
    return 0;
}
```



### Call by reference

- 매개변수에 변수의 주소를 전달하여 메소드 내에서 수정한 내용이 메소드 밖에서도 적용되게 하는 기법입니다.	
- 포인터를 활용해 주소를 매개변수로 넘기게 되면 출력값이 바뀐채로 출력됩니다.

```c
void swap(int *a, int *b)
{
	int t = *a;
	*a = *b;
	*b = t;
}

int main()
{
    int a = 1;
    int b = 2;
    swap(&a, &b);
    cout << a << " , "<< b << endl; //2, 1
    return 0;
}
```



### 자바스크립트

- 기본적으로 자바스크립트는 원시값을 **arguments**로 넘겨주면 **Call by value**의 형태로 작동합니다.

```js
var a = 1;
var func = function(b) {
  b = b + 1;
}
func(a);
console.log(a); // 1
```

- 또한 참조값을 넘기면 **Call by reference**의 형태로 작동합니다.
  - 하지만 이게 진실일까??

```js
var a = {};
var func = function(b) { 
  b.a = 1;
}
func(a); 
console.log(a.a); // 1
```

- **Call by reference**의 예외 상황 => 다른말로 **Call by sharing**
  - 참조 값을 넘겼음에도 변하지 않았습니다.

```js
var a = {};
var func = function(b) {
  b = 1;
}
func(a); 
console.log(a); // {}
```

- 즉 자바스크립트는 무조건 **Call by value**로 작동하게 됩니다.
  - 처음에 참조 주소값이 들어있는 `a`의 값을 복사하고 이것을 `b`에 담습니다.
    - 이 때 b도 같은 `{}`를 가르키고 있습니다.
  - 자바스크립트는 `=` 연산자로 참조값을 재할당하기 때문에 기존에 참조하던 `{}`에서 `1`로 참조 대상이 변경되었다.
    - 참조 대상이 변경되었기 때문에 참조주소가 변경됩니다.
- 정리하자면 참조 타입을 인자로 넘기면 참조값에 대한 **복사본**을 만들어서 넘기게 됩니다.



### 그럼 클로저는 어떤 방식일까?

- 일단 매개변수로 넘기면 동일하게 **Call by value**로 작동합니다.
- 클로저는 실행 컨텍스트의 관점에서 정리하면, 외부함수의 실행이 끝났음에도 내부 함수에서 렉시컬 스코핑으로 인해 상위 컨텍스트 내의 활성 객체(변수 객체)를 스코프 체인으로 참조할 수 있는 상황입니다.
- 즉 내부에서 선언된 변수를 참조하고 있기 때문에 클로저는 **Call by reference**이지 않을까 생각합니다.

```js
function test(){
    const object = {};
    
    return {
      a: function(sum){ 
        sum=3
        return sum 
      }, 
      b: object}
}

const a = test();
a.a() // 3
a.b // {}
```

