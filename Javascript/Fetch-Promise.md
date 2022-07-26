# Fetch()
```js
1. fetch(resource)
2. fetch(resource, options)
```
fetch 메소드는 네트워크에서 리소스를 가져오는 과정을 시작해 fulfilled된 Promise를 리턴한다.<br/><br/><br/><br/>



## A Promise that resolves to a Response object

**fetch함수는 resource를 받아 response object를 돌려주는 Promise를 return한다.**<br/>
|fetch ✔|Promise ✔ |response object ✔|
|-|-|-|

<br/><br/><br/><br/>
위 말대로라면, fetch가 resource를 받았을 때를 콘솔로그 하면 Promise를 반환해야 한다. 직접 찍어서 정말 Promise가 나오는 지 확인해보자.

```js
const fetched = fetch('https://jsonplaceholder.typicode.com/posts')
console.log(fetched)
```
<img style="width:250px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsjxQd%2FbtrIiFlSQNT%2FCWGvVYWRWGMyfePkP0YHX1%2Fimg.png"><br/>
resource를 받은 fetch함수가 정말 Promise를 반환했다.

1. 어떤 함수를 사용했을 때, 함수의 반환값이 promise라면 비동기 함수일 가능성이 높다.
2. 함수의 반환값은 두개의 함수(메소드)를 사용할 수 있다. (then,catch-모두 callback함수를 받는다)

<br/><br/><br/>
```js
.then(function(response){})
```
```js
const fetched = fetch('https://jsonplaceholder.typicode.com/posts')
console.log(fetched)
fetched.then(function(result){})
```
두 개의 함수가 추가된 위의 코드를 읽어보면, 
fetched가 실행되면 then이라는 함수가 실행되는데, then은 콜백함수를 받는다. fetch의 반환값은 Promise고 then이 그 Promise로 나온 결과를 result라는 매개 변수로 받아낸다.
이때의 result를 콘솔로 출력하면

<img style="width:250px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmhpnl%2FbtrIjNcKAxJ%2FKnUTpKTStwGLsLukTCfrlk%2Fimg.png">
<br/>
위처럼 Response라는 객체를 반환한 모습을 볼 수 있다.
<br/><br/><br/><br/>

## 정리!

1. fetch 에다가 resource를 넘겨줬더니 Promise 객체를 반환했다.
2. fetch가 성공했을 때, then으로 전달된 콜백함수가 호출됐다. 콜백함수가 호출되면서 결과값을 첫번째 매개변수로 받았다.
3. fetch가 실패했을 때, catch안으로 전달된 콜백함수가 호출된다. 매개변수로는 그 이유를 알려준다.
4. 위의 코드는 fetch의 then으로 전달된 함수가 실행되면서 response객체가 전달됐다는 것을 알려줬다.

fetch가 성공하면 then()이 받고, 실패하면 catch()가 받는다. fetch도 Promise를 반환하고, then도 Promise를 반환한다.

```js
fetch('https://jsonplaceholder.typicode.com/posts')
.then(function(response){
  return console.log(response)
  })
```
<br/><br/><br/>

Response는 json()과 text() 등을 함수로 갖고 있다. 웹브라우저는 데이터들을 json 데이터 타입에 맞게 해석해서 js의 데이터 타입으로 돌려준다.

그럼 json() 이 무엇을 리턴하는 지 보자.
```js
fetch('https://jsonplaceholder.typicode.com/posts')
.then(function(response){
  return console.log(response.json())
  })
```

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKQtq5%2FbtrIjLMOpNN%2Fosly4YpEaOn7JfW8Pslyuk%2Fimg.png">
<br/><br/><br/><br/>
response.json() 을 콘솔로 확인했더니, 역시나 Promise를 반환하는 걸 볼 수있다. 즉, response의 반환값 또한 Promise라는 것. promise를 반환하므로 우리는 여기서 또 then() 또는 catch() 함수를 쓸 수 있다.

<br/>

```js
fetch('https://jsonplaceholder.typicode.com/posts')
.then(function(response){
  return response.json()})
.then(function(data){
  return console.log(data)
})
```
<img style="width:250px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbeI04d%2FbtrIeM7xnJ9%2FPQR5kpPtTnuq08zj6rKI7K%2Fimg.png">
<br/>
fetch로 Promise를 반환. 그 반환값을 json()함수로 js 데이터 타입으로 돌려 받음. 그 반환값의 데이터를 출력했더니 데이터 배열이 나왔다.

<br/><br/>

### json 예제 제공 사이트
[jsonPlaceholder](https://jsonplaceholder.typicode.com/)

<br/><br/>

### Ref
- https://youtu.be/Sn0ublt7CWM
- https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then



<br/><br/>
2022.07.27
<br/>
fetch() 함수 개념과 Promise가 잘 이해되지 않았었는데, 어느정도 흐름이 이해된 것 같다. fetch 함수에 리소스를 넣으면 Promise 객체를 반환하고, 반환된 Promise 객체는 js에서 읽을 수 없어서 json() 으로 변환해주면 js에서도 데이터를 읽을 수 있게 된다. 그 상태에서 또 then() 함수로 반환되는 데이터를 인자로 받으면 data를 사용할 수 있다.

복잡하지만 자주 보고 읽자!