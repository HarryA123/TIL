# This

대부분의 객체지향 언어에서 this는 클래스로 생성한 인스턴스 객체를 의미한다. 클래서에서만 사용하기에 혼란의 여지가 없지만 자바스크립트에서 this는 어디서든 사용이 가능하기 때문에 상황에 따라 혼란을 야기합니다.

 

함수와 객체(메소드)의 구분을 할 때 this를 사용합니다. this는 함수를 호출할 때 결정되는데 함수를 어떤 방식으로 호출하냐에 따라 값이 달라집니다.

 

전역 공간에서 this
전역 공간에서 this는 전역 객체를 가리킨다. 

전역 객체는 브라우저 환경에서 window, Node.js 환경에서는 global을 의미한다.

 
```js
console.log(this)		        // {process:...}
console.log(window) 		    // {process:...}
console.log(this === window) 	// true
 ```
<br/><br/>
 

자바스크립트의 모든 변수는 실행 컨텍스트의 LexicalEnvironment의 프로퍼티로서 동작합니다.
```js
var a = 1
console.log(a)			    //1
console.log(window.a)		//1
console.log(this.a)         //1
```
LexicalEnvironment를 조회해서 a와 일치하는 프로퍼티를 찾아 1이라는 값이 나왔습니다.

이렇듯 전역변수를 선언하면 자바스크립트 엔진은 이를 전역 객체(window, this)의 프로퍼티로 할당합니다.

console.log(a)를 했음에도 1이 나오는 이유는 스코프 체인에서 a를 검색하다가 전역 스코프의 LexicalEnvironment 즉 전역 객체에서 a라는 프로퍼티를 발견하고 그 값을 반환했기 때문입니다. 단순히 window. 이 생략되었다고 생각해도 무방합니다. 

<br/><br/>

## 변수 선언이 아니라 프로퍼티에 직접 할당해도 똑같이 동작할까?
 
```js
var a = 1;
window.b = 2;
console.log(a, window.a, this.a);		//1 1 1
console.log(b, window.b, this.b);		//2 2 2

window.a = 3;
b = 4;
console.log(a, window.a, this.a);		//3 3 3
console.log(b, window.b, this.b);		//4 4 4
```

위의 예시의 경우, 프로퍼티에 직접 할당은 변수 선언을 했을 때와 똑같이 동작하는 것을 알 수 있습니다.

 하지만 '삭제(delete)' 명령의 경우 전혀 다르게 동작합니다.

 <br/><br/>

```js
var a = 1;
delete window.a;				        // false(삭제X)
console.log(a, window.a, this.a);		//1 1 1

window.c = 3;
delete window.c;		        		// true(삭제O)
console.log(c, window.c, this.c);		//RefferenceError: c is not defined
```
처음부터 전역객체의 프로퍼티로 할당한 경우(c) 에는 삭제가 되었지만, 전역 변수로 선언한 경우(a) 에는 삭제가 되지 않았습니다.

 

전역 변수를 선언하면 자바스크립트 엔진이 이를 자동으로 전역 객체의 프로퍼티로 할당+ 해당 프로퍼티의 configurable(변경 및 삭제 가능성)을 false로 정의하기 때문에 a는 삭제되지 않았던 것(false 출력)입니다.

<br/>

## 함수와 메소드
프로그래밍 언어에서 함수와 메소드는 미리 정의한 동작을 수행하는 코드 뭉치입니다. 둘은 '독립성' 에서 차이가 있는데 함수는 그 자체로 **독립적인 기능**을 수행하지만, 메소드는 자신을 호출한 **대상 객체에 대한 동작**을 수행한다.

메소드는 객체의 메소드로 호출할 경우에만 메소드로 동작하고 그렇지 않으면 함수로 동작한다.

<br/><br/>

## 함수로서의 호출? 메소드로서의 호출?
함수 앞에 점(.)이 있으면 메소드, 없으면 함수라고 쉽게 구분할 수 있습니다. 

<br/>

```js
1. func(1)             // 함수
2. obj.method(1)       // 메소드
```
1번은 앞에 점이 없기 때문에 함수로서 호출한 것이고, 2번은 앞에 점이 있기 때문에 메소드로서 호출한 것이라고 구분할 수 있습니다.

<br/><br/>

## 메소드 내부에서의 this 

this 에는 호출에 대한 정보가 담기는데 어떤 함수를 메서드로서 호출하는 경우 호출 주체는 함수명 앞의 객체가 된다. 즉, 마지막 점 앞에 명시된 객체가 곧 this가 됩니다. 바로 위의 예제를 예로 들면, 2번에서의 this는 obj입니다. 호출의 주체가 obj이기 때문입니다.

반면, 함수에서의 this는 전역 객체를 가리킵니다.

this 바인딩에 관해서는 오직 해당 함수를 호출하는 구문 앞에 점 또는 대괄호 표기가 있는지 없는지가 관건입니다.

<br/>
2022.07.30


