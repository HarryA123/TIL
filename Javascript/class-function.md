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
  constructor(name, age){
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

위에서는 speak() 라는 메소드를 이용해서 콘솔에 'hello ${this.name}'를 설정해 놓고 harry.speak() 로 출력했더니 hello harry가 나왔다.<br/><br/><br/><br/>


# 클래스 상속

클래스에는 상속이라는 개념이 있다. 즉, 부모와 자식-자식 관계가 존재한다.
예제에는 Person이라는 클래스가 존재한다. 근데 만약에 내가 Person 클래스에 있는 속성이나 메소드를 조금 추가하거나 수정을 하고 싶다고 가정해보자. 그러면 내가 원하는 새로운 클래스를 만들어 부모인 Person 클래스에서 상속을 받아오면 된다.

자, SpecialPerson클래스를 만들어서 Person에게서 상속을 받아오자.<br/><br/><br/>

## 상속 받아오는 SYNTAX

```js
class 새로운클래스(자식 클래스) extends 부모 클래스{

}
```
이 SYNTAX는 부모 클래스의 속성이나 메소드를 새로운 클래스로 연장해서 가져온다.<br/><br/><br/><br/>


```js
class Person{
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
    speak(){
     return `hello ${this.name}`
  }
}
const harry = new Person('harry', 22)

class SpecialPerson extends Person{
}

const special = new SpecialPerson('hanson', 33);
special.name;
special.speak();
// hanson
// hello hanson
```
위의 코드를 보면 Person이라는 부모의 클래스가 있고 그 아래에 SpecialPerson이라는 자식 클래스(상속받은 클래스)가 생성되었다.
그리고 그 아래에 SpecialPerson 이라는 클래스에 인수를 넣어주고 그 값을 special 이라는 변수로 설정했다.

이제 위의 코드에서 메소드를 더 추가하거나 수정해보자.
1.  속성에 favorite을 **추가**해보자.
2.  speak() 메소드의 반환값에 'and ~ years old'를 덧붙여 **수정**해보자.
3.  fullInfo() 라는 메소드를 추가해서 "'~name~'은 ~살. who likes ~." 라는 문구가 나오도록 **추가**해보자.<br/><br/><br/><br/>

<h2>결과</h2>

```js
class Person{
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
    speak(){
     return `hello I'm ${this.name}`
    }
}
const harry = new Person('harry', 22)

class SpecialPerson extends Person{
  constructor(name, age, fav){
    super(name, age);
    this.fav = fav;
  }
    nowSpeak(){
      return super.speak() + ` and ${this.age} years old!`
      }
    
    fullInfo(){
      return `${this.name} is ${this.age} years old man who likes ${this.fav}`
    }
}

const special = new SpecialPerson('hanson', 33,'dogs');
```
<br/><br/>

<h2>1.  속성에 favorite을 <strong>추가</strong>해보자.</h2><br/>

- this.fav 로 속성을 지정해줬고 parameter에 fav를 넣어 fav가 this.fav에 오도록 추가했다. (이 때는 단순히 새로운 걸 '추가'하는 작업이기 때문에 super 키워드가 필요하지 않다.)

- # super
  this.fav 윗줄인 'super(name, age);'를 보면 처음 보는 super 키워드를 이용한 게 보인다.<br/>
super() 는 부모클래스의 생성자를 호출하는 역할을 한다.<br/>그래서 super(name)이라고 쓰는 것 만으로도 부모클래스인 Person의 'this.name = name' 을 가져와주는 친절한 키워드다.<br/><br/>
근데, 왜 괄호 안에 name과 age가 같이 들어있냐!? 궁금할 텐데 super 키워드는 한 번만 호출할 수 있기 때문에 한 개를 초과하면 저렇게 괄호 안에 넣어주면 된다.<br/>
그리고 super는 this 키워드가 사용되기 전에 먼저 사용되어야 한다. this를 먼저 쓰게 되면 아래 이미지와 같은 오류가 발생한다.

  ```js
  this.fav = fav;
  super(name, age);
  ```
  <img style="width:600px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwK7fS%2FbtrHmdJHsRs%2FEc6j1k53cTyF4jKVRnTKUK%2Fimg.png"><br/>
  super를 먼저 쓰고 this 키워드를 쓰자.
  <br/><br/>

  <h3>정리!</h3>
  
  1. 부모 클래스의 생성자를 호출한다.
  2. super 키워드는 한 번만 쓸 수 있다.
  3. 항상 super 키워드가 this 키워드보다 앞에 있어야 한다.
  <br/><br/><br/><br/><br/>



<h2>2.  speak() 메소드의 반환값에 'and ~ years old'를 덧붙여 <strong>수정</strong>해보자.</h2><br/>

 - 여기서도 super 키워드를 이용해서 기존에 부모클래스의 speak() 메소드를 그대로 가져왔고 메소드의 이름을 nowSpeak 로 바꾸었다.
 - nowSpeak의 코드로는 부모클래스에서 speak를 가져와(super를 사용해서) ' and ${this.age} years old!'(백틱) 문구를 + 연산자로 이어주면 special.nowspeak() 를 호출했을 때 아래처럼 정상적으로 출력 된다.<br/>

    ```js
    // "hello I'm hanson and 33 year old!"
    ```
    <br/>
 - 🚨 처음에는 return 값으로 + console.log(' and ${this.age} years old!'(백틱)) 이렇게 했더니 오류는 안 나는데 내가 원하는 것처럼 자연스러운 문장이 안 되고 줄 바꿈을 해서 이상해졌고 + 가 아니라 && 을 사용했더니 뒷부분 and ~ years old 부분이 undefined 가 떠버렸다. 이유는 뭔지 모르겠지만 좀 더 공부해보고 commit 업데이트 해야겠다.(책에서는 잘 되던데?)<br/><br/><br/><br/><br/>


<h2>3.  fullInfo() 라는 메소드를 추가해서 "'~name~'은 ~살. who likes ~." 라는 문구가 나오도록 <strong>추가</strong>해보자.</h2><br/>

  - 새로운 메소드를 추가하는 건 부모클래스를 끌고 올 필요도 없어서 super 키워드는 사용하지 않고 그냥 일반적으로 써주면 된다.(1번에서 this.fav 라는 속성을 새롭게 추가했을 때의 방식과 유사하게 super 키워드 필요 없음.)
  - 1번에서 this 키워드로 만들었던 this.fav를 가져와서 넣어봤다.<br/><br/><br/>


<h3>상속 정리!</h3>

- super() 는 자식 클래스에서 부모 클래스를 호출 할 때 사용한다. 즉 클래스 상속과 super는 빼놓을 수 없는 관계.
- super() 는 부모클래스의 생성자를 호출한다!!!!!!
- 부모 클래스를 가져와 '수정or응용' 할 때는 super()를 쓰지만, '추가'할 때는 필요 없다.
- super는 한 번만 쓴다.
- super는 this 키워드보다 먼저 쓴다.

<br/><br/><br/><br/>

# Get! Set!

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

2022.07.13<br/>
2022.07.14
