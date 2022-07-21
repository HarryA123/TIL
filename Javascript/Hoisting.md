# 호이스팅(Hoisting)

호이스팅은 자바스크립트 엔진이 실제로 끌어올리지는 않지만 편의상 끌어올린 것으로 간주하자는 의미에서 이름 붙여졌다.(호이스팅은 environmentRecord의 수집 과정을 추상화한 개념이다.) 호이스팅이 되면 코드가 실행되기 전, 자바스크립트 엔진이 이미 해당 환경에 속한 코드의 변수명들을 모두 알고 있게 된다. <br/><br/><br/>


## 어떤 것들이 호이스팅 될까?
현재 컨텍스트와 관련된 코드의 식별자 정보들이 저장된다.

- 함수의 매개변수의 이름
- 함수 선언문 그 자체
- 변수의 식별자

(변수는 선언부와 할당부를 나누어서 선언부만 끌어올리지만 함수선언은 함수 전체를 끌어올린다.)<br/>

environmentRecord는 위와 같은 식별자들을 가져오는 데에만 관심 있다. 그 외에 변수에 어떤 값이 할당되었는 지는 관심 없다. 그래서 변수를 호이스팅 할 때 변수에 할당된 것은 그대로 두고 변수명만 끌어올린다.<br/><br/><br/><br/>


 

# 함수 레벨 스코프
함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다.
함수 내부에서 선언한 변수는 지역변수이며 함수 외부에서 선언한 변수는 모두 전역변수다.<br/><br/>
```js
const apple = 444
const a = function(){
    const b = 123
    console.log(apple)
    console.log(b)
}

a() // 444, 123
console.log(b) // ReferenceError: b is not defined
```
함수 a를 호출했을 때 444, 123 이 나오는 이유는 스코프 체인을 통해서 a함수 내에 apple을 찾고, apple이 없으면 그 밖의 환경에서 a를 찾는다. 위의 경우 a라는 전역변수를 찾았기 때문에 값이 444가 된다.<br/><br/>
콘솔로그 b로 에러가 뜨는 이유는 함수 내부에 있는 지역변수를 찾으려고 했기 때문이다. 콘솔이 위치한 전역에서는 함수 내부의 존재하는 변수를 참조할 수 없다. 그래서 자동으로 전역에 위치한 변수 b를 찾는데, b라는 전역변수는 없기때문에 에러가 뜨는 것이다.


<br/><br/><br/>

# 블록 레벨 스코프
모든 코드 블록 내에서 선언된 변수는 코드 블록 내에서만 유효하고 코드 블록 외부에서는 참조할 수 없다.
코드블록 내부에서 선언한 변수는 지역 변수다.<br/>

여기서, 코드 블록이라 함은 간단하게 {}중괄호로 묶여진 코드를 의미한다.
<br/><br/>
```js
let a = 123;

{
  let a = 456;
  let b = 456;
}

console.log(a); // 123
console.log(b); // ReferenceError: b is not defined
```
첫번째 콘솔이 123이 나오는 이유는 4번재 줄부터 시작하는 코드블럭에 있는 a는 외부에서 참조할 수 없기 때문이다. 그래서 1번째 줄에 있는 전역변수 a의 값을 읽어서 123이 나온다.<br/><br/>
두번째 콘솔에서 에러가 뜨는 이유는 마찬가지로 코드 블럭 안에 있는 변수를 외부에서 참조할 수 없기 때문이다. 첫번째 콘솔의 경우에는 코드블록 내부의 a를 참조하지 못해도 전역변수에 a가 있었기 때문에 123이 나왔지만, b는 전역변수로 선언조차 되지 않았다. 그래서 에러가 뜬다.





<br/><br/><br/>



## 문제!
```js
let apple = 123

{
    let apple = 456
    console.log(apple)
    let banana = 777
}

console.log(apple)
console.log(banana)
```
위의 콘솔값은 어떤 것이 나올까?

<details>
<summary>
해답
</summary>
<div markdown="1">
456<br/>
123<br/>
Uncaught ReferenceError: banana is not defined<br/><br/>

코드 블록 내에서 선언된 변수 apple은 지역변수다.
let apple = 456이므로 코드 내의 console.log 값은 456이 된다.
let apple = 123 은 전역 변수이므로 같은 환경에 있는 console.log는 123이 출력된다.
banana에서 에러가 뜨는 이유는 코드 블록 내에서 선언된 banana 변수를 외부에서 출력하려고 했기 때문이다.
</div>
</details>
<br/><br/><br/><br/>

## let 키워드는 중복 선언이 불가능하다.
<img style="width:350px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdcwnLB%2FbtrHJAFrsUW%2FGu8i7FZaouMC6WSaSkdWo0%2Fimg.png"><br/><br/><br/><br/>

 

## 호이스팅 사용시 주의할 점

- 호이스팅이 가능하다 하더라도 아무데나 선언하는 것보다 상단부터 차례대로 선언하는 것이 좋다.
- ES6에서는 let과 const 를 사용한다.

<br/>
Ref : 코어 자바스크립트
<br/>
2022.07.21