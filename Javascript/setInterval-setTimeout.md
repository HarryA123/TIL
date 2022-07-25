# setTimeout과 setInterval 메소드

setTimeout 은 일정 시간 후 함수를 실행하고

setInterval 은 일정 시간 간격으로 함수 반복을 실행한다.

이때의 시간은 밀리세컨드를 사용한다.<br/><br/><br/>

## setTimeout()
타이머가 만료되면 실행될 함수와, 그 함수를 실행하기까지 기다려야하는 시간이 필요하다.

setTimeout 를 취소하고 싶다면 clearTimeout() 메소드를 사용한다.

```html
<input type='number' /> 
<button id='button'>Click ME!</button> 
```
```js
const input = document.querySelector('input')
const button = document.querySelector('#button')

function consoleLog(){
  console.log(input.value)
}

button.addEventListener('click', function(){
  setTimeout(consoleLog, 3000)
})
```
button을 클릭하면 setTimeout메소드가 실행된다. 메소드가 받고 있는 함수는 consoleLog 이고, 3초 후에 consoleLog 함수가 실행된다.
consoleLog 함수는 input.value 값을 콘솔로그한다.
<br/><br/><br/><br/>

## setInterval()
```js
const input = document.querySelector('input')
const button = document.querySelector('#button')

function consoleLog(){
  console.log(input.value)
}

button.addEventListener('click', function(){
  setInterval(consoleLog, 1000)
})
```
같은 방법으로 setInterval을 하면 input에 입력한 값이 1초 간격마다 실행된다.
<br/><br/><br/><br/>

## clearInterval() 메소드

clearInterval() 메소드는 setInterval 작업을 취소한다. 만약에 제공된 '매개변수'가 setInterval에 설정된 작업을 식별하지 않는 경우엔 아무런 작업도 수행하지 않는다.

```
clearInterval(intervalID)
```


```html
  <input type='number' /> 
  <button>Start</button> 
  <button>Stop</button> 
```
```js
const input = document.querySelector('input')
const startBtn = document.querySelector('button')
const stopBtn = document.querySelector('button:nth-child(3)')

let timerId;
function consoleLog(){
  console.log(input.value)
}

startBtn.addEventListener('click', function(){
  timerId = setInterval(consoleLog, 1000)
})

stopBtn.addEventListener('click', function(){
  clearInterval(timerId)
})
```
timerId 식별자를 만들어 setInterval 메소드를 timerId로 할당한다. clearInterval은 timerId를 인자로 받아 setInterval 메소드를 취소한다.

<br/><br/><br/>

<img style = "width:400px" alt = "w3s출처" src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRcg61%2FbtrIdazy9AZ%2FLTWNLZhKQtsaGk5g0hkOd1%2Fimg.png">
<h6>출처 : W3S</h6>
clearInterval()을 하면서 좀 이해가 안 됐던 부분이다. 위 Note에 나온 것처럼 interval을 클리어하려면 setInterval에서 리턴된 id를 사용해야한다.


<br/>
2022.07.25