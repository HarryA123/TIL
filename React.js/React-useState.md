## 리액트 엘리먼트

리액트 엘리먼트는 일반 객체이며 컴포넌트의 '구성요소'다. 

개념적으로 컴포넌트는 js 함수와 유사하다. props라는 임의의 입력을 받고 화면에 어떻게 표시되는지를 기술하는 React엘리먼트를 반환한다.

이제 버튼을 누르면 콘솔로그로 'world' 가 출력되도록 코드를 만들어보자.

<br/><br/>

## 1단계 : 컴포넌트를 만들어 JSX 식으로 리액트 엘리먼트를 먼저 구성한다.

```js
const App = ()=>{
  return <div>
    <h2>hello</h2>
    <button>Click!</button>
    </div>
}
```

App 이라는 이름의 컴포넌트를 만들어주었다. 컴포넌트는 알다시피 함수이고 첫 글자가 대문자로 시작한다. 컴포넌트는 리액트 엘리먼트를 반환한다. 이처럼 리액트 엘리먼트는 컴포넌트의 '구성요소'다.

<br/><br/>

## 2단계 : 버튼을 클릭하면 콘솔로 'worLd' 가 출력되도록 event를 추가한다.

```js
const App = ()=>{

  const onClick = ()=>{
    console.log('world!');
  }

  return <div>
    <h2>hello</h2>
    <button onClick={onClick}>Click!</button>
    </div>
}
```
리액트 엘리먼트에서 event를 실행할 수 있다. onClick은 onClick이라는 함수를 받는다.  자바스크립트에서는  addEventListener('click', function(){}) 처럼 중괄호 안에 클릭 이벤트가 실행되면 작동할 함수를 넣어주면 된다.

클릭되면 world가 출력되어야 하므로 console.log('world') 라고 입력해주었다.

<br/><br/>

## 3단계 : click을 눌렀을 때, 콘솔이 아니라 화면에 있던 Hello 가 world로 바뀌도록 한다.

생각: 버튼을 클릭하면 기존에 있던 태그로 텍스트를 띄우는 작업은 js에서 어떻게 했지? innerText를 사용했다. 하지만 React에서는 useState를 사용한다.
React useState Hook을 사용하면 우리가 함수 안에서 state를 추적할 수 있게 한다.
```js
const App = ()=>{
  const [title , setTitle] = React.useState('hello?')
  
  const onClick = ()=>{
    setTitle('world!');
  }

  return <div>
    <h2>{title}</h2>
    <button onClick={onClick}>Click!</button>
    </div>
}
```
위의 코드를 하나씩 살펴보자, 일단 useState를 사용할 때 구조 분해 할당을 사용한다.

<br/><br/>

```js
const a = React.useState()
const [title , setTitle] = React.useState('hello?')
```
<img style="width:250px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Foh3v8%2FbtrIwG6nhiM%2FcQbwTapfgLOmx03P84RbE1%2Fimg.png">

저 React.useState() 만 따로 콘솔로 출력해보면, 위처럼 undefined와 함수가 나온다. 즉 React.useState()는 state와 함수로 나뉜다.

onClick이라는 함수가 실행됐을 때 setTitle이 작동하는데, setTitle 함수 안에는 'world'를 호출한다. 즉, 버튼을 누르면 world가 뜬다. 근데 그게 useState를 이용했으므로 화면에 뜬다. innerText의 역할을 하는 것.

리액트 엘리먼트를 보자 h2태그 안에 {title}이 되어 있다. 그리고 그 title의 기본 값을 보면, hello? 로 되어 있다. 그래서 콘솔로 title을 찍어보면 'hello?' 가 나온다. 왜냐면 useState 함수 안에다가 hello? 라고 작성해뒀기 때문이다. 그래서 지금 현재 title의 값은 hello? 이며, h2 태그 안의 텍스트 또한 {title} 이기 때문에 hello? 가 나오는 것이다.

이벤트를 생성할 때는 리액트 엘리먼트에 속성으로 넣어줄 수 있다. 이벤트는 함수를 값으로 가진다. 이벤트가 실행되면 함수가 실행된다. 만약에 실행된 '액션'을 브라우저 상으로 보여지게 하고 싶다면 useState를 사용해야한다. useState 에 값을 지정해두면 그 값이 undefined를 채운다. 그리고 그 값이 default가 된다. 그 state에 대한 직접적인 액션은 state 함수에서 이뤄진다. 이벤트 함수 안에 state함수에 값을 넣어 액선을 설정할 수 있다.

<br/>

2022.07.29

아 리액트 너무 헷갈린다. 뭐 알고 넘어가면 나중에 또 까먹고 새롭게 느껴진다. 많이 보고 많이 써봐야하는데 자바스크립트도 해야하고 토이프로젝트도 해야하고 할 게 산더미. 일단 useState라는 게 어떻게 작동하는 지 잘 익혀야겠다. 자주 쓸 것 같다. 그리고 리액트에서 반복문 사용하는 방법, 구조 분해 할당도 잘 알아야할 것 같다. 일단 초반이니까 너무 낙담하지 말고 천천히나마 따라가보자. 이해하면 재밌고 쉬우니까 걱정말자!
