# Class function

ES5 까지는 생성자 함수를 사용해왔다. 하지만 ES6에서 class 함수라는 것이 새롭게 탄생하면서 생성자 함수는 예전의 것이 되었다.

둘이 비슷한 기능을 하기 때문에 ES5의 생성자 함수를 알고 있었다면 ES6의 클래스 함수를 이해하기 쉬울 것이다. 클래스 함수 문법이 생성자 함수 문법보다 더 깔끔하다.
<br/><br/><br/><br/>



## Class 선언
```js
class 클래스명 {
  constructor(매개변수){
    this.~~
    this.~~
  }
}
```
<br/><br/>

## Class 표현식 - 1 (기명)
```js
let 변수명 = class 클래스명 {
  constructor(매개변수){
    this.~~
    this.~~
  }
}
```
<br/><br/>

## Class 표현식 - 2 (익명)
```js
let 변수명 = class {
  constructor(매개변수){
    this.~~
    this.~~
  }
}
```
<br/><br/>
- 클래스 표현식은 호이스팅 되지 않는다.
  
  하지만 아래처럼 위치를 바꿔주면 호이스팅이 된다.
  
  <img style="width: 400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcO12H%2FbtrHdwiWqxT%2FmFtwXw84KUKNZsWoUSlUQK%2Fimg.png">
  

   <br/>
- class는 constructor(생성자) 매소드와 함께 쓰인다. 이는 **객체를 생성하고 초기회 하는 역할**을 한다. 
  
  constructor 매소드는 클래스 안에서 하나여야 한다. constructor 매소드를 2개로 설정하면 오류가 발생한다. <br/><br/><br/><br/>


## Object 생성

```js
class Person{
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
}

const harry = new Person('harry', 22)
console.log(harry)
console.log(harry.name)
console.log(harry.age)

// Person {name: 'harry', age: 22}
// harry
// 22
```
harry라는 이름의 변수에 new 키워드를 붙여 새로운 Person을 만든다. 그리고 소괄호 안에 관련한 인수를 넣으면 된다.<br/><br/><br/><br/>



## fields and method 

클래스는 fields 영역과 methods 영역으로 나누어져 있다.

```js
class Person{
  constructor(){
    // fields
    this.name = name;
    this.age = age;
  }
    // methods
    speak(){
    console.log(`hello ${this.name}`)
  }
}
const harry = new Person('harry', 22)
console.log(harry.name)
console.log(harry.age)
harry.speak()

//  harry
//  22
//  hello harry
```
methods 영역에는 메소드를 얼마든지 추가해서 넣을 수 있다.

위에서는 speak() 라는 메소드를 이용해서 콘솔에 `hello ${this.name}`를 설정해 놓고 harry.speak() 로 출력했더니 hello harry가 나왔다.<br/><br/><br/><br/>

## Get! Set!

```js
class Person{
  constructor(name, age, height){
    // fields
    this.name = name;
    this.age = age;
    this.height = height;
  }
    get height(){
      return this._height;
    }
    set height(value){
      this._height = value < 10 ? "you're not a human" : value;
    }

}
const harry = new Person('harry', 22, -1);
console.log(harry.height);

// you're not a human
```

get이라는 키워드를 이용해서 값을 return하고 set이란느 키워드를 이용해서 값을 설정한다. set에서는 값을 받아와야 하기 때문에 매개변수를 입력한다.

삼항연산자를 사용해서 harry가 입력한 height 값이 10보다 작으면(true) you're not a human 이 나오고 크면(false) harry가 입력한 값 그대로 출력하게 해주었다.

getter 와 setter가 사용하는 변수 이름 height 앞에 '_' 가 붙은 이유는 그냥 get, set에서 height를 썼을 경우 무한재귀 call stack 이 넘쳐서 오류가 생기기 때문이다.
<br/><br/>

<h5> 🚨 getter 와 setter에 대해서는 더 깊이 공부해서 TIL로 올려야겠다. 무한재귀가 왜 일어나는 지 알아보자.</h5><br/>

2022.07.13
