
콜백함수로 어떤 객체의 메서드를 전달하면 그 메서드는 메서드가 아니라 함수로서 호출된다.

```js
var obj = {
    vals : [1, 2, 3],
    logValues : function (v, i){
        console.log(this, v, i);
    }
};

▼
obj.logValues(1, 2); 
// {vals: [1, 2,3] , logvalues : f } 1 2

▼
[4, 5, 6].forEach(obj.logValues); 
//currnetValue, index가 들어간다
//Window 4 0
//Window 5 1
//Window 6 2
```

첫번째 화살표를 보면 this가 전역객체가 아닌 obj를 가리켜 인자로 넘어온 1,2가 출력되었다.

메소드로서 호출된 것이다.

두번째 화살표에서는 obj.logValues 메소드가 콜백함수로 전달했다. 어떤 객체의 메소드가 콜백함수로 전달되면 함수로서 호출되기 때문에 this는 obj가 아니라 window 전역객체를 가리키게된다.

즉, obj.logValues는 메소드로서 호출하면 obj와 직접적 연관이 생기지만, 메소드로서 호출한 것이 아니라 콜백함수로 호출한다면 obj와 직접적 연관이 없어져 this는 전역객체를 가리키게 된다.

<br/><br/>

콜백함수 내부에서도 this가 객체를 바라보게 하고 싶다면 어떻게 할까?
전통적인 방법 : 메소드 내부에서 self변수를 선언해 this를 할당한다.

```js
var obj1 = {
    name : 'obj1',
    func : function(){
        var self = this;
        return function(){ 
            console.log(self.name); 
        }
    }
};

var callback = obj1.func();
setTimeout(callback, 1000);
```
위의 방식대로 하면 self는 obj1객체를 가리키기 때문에 1초 뒤에 obj1이 출력된다.

<br/><br/>

이 방법은 this를 직접적으로 사용하지 않기 때문에 차라리 this를 없앤다면 아래와 같은 코드를 작성할 수 있는데,

```js
var obj1 = {
    name : 'obj1',
    func : function(){
        console.log(obj1.name);
    }
};

setTimeout(obj.func, 1000);
```
1초 뒤에 obj1이 실행된다는 목적은 전통적인 방식과 똑같이 달성하지만 this를 사용하지 않았기 때문에 다양한 상황에 재활용이 불가능해진다.

<br/><br/>

그래서 위의 코드를 재활용 가능하게 만든다면 아래와 같은 코드를 덧붙일 수 있다.

```js
...
var obj2 = {
	name: 'obj2',
    func: obj1.func
};
var callback2 = obj2.func();
setTimeout(callback2, 1500);

var obj3 = { name: 'obj3' };
var callback3 =   obj1.func.call(obj3);
setTimeout(callback3, 2000);
```
1.5초 뒤에는 obj2

2초 뒤에는 obj3이 출력된다.

전통적인 방법은 this를 우회적으로 활용하여 다양한 상황에서 원하는 객체를 바라보는 콜백함수를 만들 수 있고,

위의 방법은 애초에 객체를 obj1로 지정했기 때문에 다른 객체를 바라보게 만들 수가 없다는 단점이 있다. + 메모리 낭비

<br/><br/>

해결사! bind
```js
var obj1 = {
	name: 'obj1',
    func: function() {
    	console.log(this.name);
    }
};
setTimeout(obj1.func.bind(obj1), 1000);

var obj2 = { name: 'obj2' };
setTimeout(obj.func.bind(obj2), 1500);
```
bind는 객체obj 를 받아 1초 뒤에 obj1을 출력하고 2초 뒤에 obj2을 출력한다.

