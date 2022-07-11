# 화살표 함수(Arrow function)

여기 일반적으로 우리가 사용하는 기명함수(이름이 있는 함수를 의미함)가 있다.
```js
const apple = function (x) {
  return x * 2
}
console.log('apple:', apple(10))

// apple: 20
```

apple 이라는 함수를 arrow function을 사용해서 더 간결하게 표현해보자.<br/><br/><br/><br/>

```js
const apple = (x) => {
  return x * 2
}
console.log('apple:', apple(10))

// apple: 20
```
바뀐 거라곤 function을 지우고 매개함수 자리 옆에다가 '=>' 라는 화살표 표시만 해주었을뿐.

여기서 더 간략하게 줄일 수 있다.<br/><br/><br/><br/>

 
```js
const apple = (x) => x * 2
console.log('apple:', apple(10))

// apple: 20
```
화살표 옆 {} 중괄호를 지워도 console은 제대로 작동한다.<br/><br/><br/><br/>

```js
const apple = (x) => x * 2
console.log('apple:', apple(10))

// apple: 20

const apple2 = (x) => true
console.log('apple2:', apple2())

// apple2: true

const apple3 = (x) => null
console.log('apple3:', apple3())

// apple2: null

const apple4 = (x) => [1,2,3]
console.log('apple4:', apple4())

// apple2: [1,2,3]

const apple5 = (x) => {'name':'harry'}
console.log('apple5:', apple5())

// error!!!!!!!
```
연산, boolean, null, array 를 넣어도 잘 나오는데, 마지막을 보면 똑같은 방식으로 object를 넣었더니 error가 뜬다!

error 가 뜨는 이유는 화살표 함수를 만들 때의 중괄호 기호와 중복되기 때문이다.

object를 화살표 함수로 표현할 때는 ()소괄호를 사용해서 object를 감싸줘야 한다.<br/><br/><br/><br/>
 
```js
const apple5 = (x) => ({'name':'harry'})
console.log('apple5:', apple5())

// {name : 'harry'}
```
object를 괄호 안에 묶었더니 오류 없이 제대로 작동한다.<br/><br/><br/><br/>

```js
const apple = x => x * 2
console.log('apple:', apple(10))

// apple: 20
```
매개 변수가 2개 이상이 아니고 하나의 매개변수만 존재할 경우, ()소괄호도 생략할 수 있다.

이렇게 화살표 함수를 사용하면 일부 내용을 축약해서 사용할 수 있기 때문에 코드가 복잡해지지 않고 간결해진다.<br/><br/>

익숙하지 않으면 자주 써서 익숙해지자!

2022.07.11