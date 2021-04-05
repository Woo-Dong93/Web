# Bind 구혀하기

- ES5에 추가된 문법으로 `this`값을 특정 값으로 변경한 후에 함수를 생성하는 메소드입니다.

```jade
Function.prototype.bind = function(target, ...args) {
	if(typeof this !== 'function') throw new Error('함수가 아닙니다.');
  	const that = this;
  	return function(...rest){
    	return that.call(target, ...args, ...rest);
    }
}
```

- ES6 문법을 사용하지 않으려면 `arguments` 을 활용하면 됩니다.

```js
Function.prototype.bind = function(target) {
	if(typeof this !== 'function') throw new Error('함수가 아닙니다.');
    var args = Array.prototype.slice.call(arguments, 1);
    var that = this;
  	return function(){
        var rest = Array.prototype.slice.call(arguments);
        return that.apply(target, args.concat(rest))
    } 
}
```

