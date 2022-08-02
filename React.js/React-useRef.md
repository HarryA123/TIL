# useRef

공부하다보니 useRef와 useState를 각자 어느 상황에 사용하는지 궁금해졌다.

useState는 state가 변하면 계속 render되어 컴포넌트 내부 변수들이 초기화된다는 특징이 있지만, useRef는 render를 하지 않고 그대로 변수들의 값이 유지된다. ref를 사용한다면 불필요한 렌더링을 막을 수 있다는 장점이 있다.

|useState|useRef|
|--|--|
|State의 변화|Ref의 변화|
|렌더링|No 렘더링|
|컴포넌트 내부 변수들 초기화|변수 값 유지됨|
|state의 변화에 렌더링 되어도 Ref값은 유지됨|-|

변화가 생길 때 값이 변경되면 안 되는 상황에 Ref가 유용하게 쓰인다.
<br/><br/><br/><br/>

```js
const App = () => {
  const [count, setCount] = React.useState(0);
  const countRef = React.useRef(0);

  const onClickState = ()=>{
    setCount(count + 1);
  }

  const onClickRef = ()=>{
    console.log(countRef.current = countRef.current + 1)
  }

  return (
    <div>
      <p>state : {count}</p>
      <p>ref : {countRef.current}</p>
      <button onClick={onClickState}>state 올려</button>
      <button onClick={onClickRef}>ref 올려</button>
    </div>
  );
};
```
이 코드를 실행했을 때, 
'state 올려' 버튼을 누를 때마다 화면의 state 숫자가 1씩 증가한다. 이것은 버튼을 누를 때마다 App 컴포넌트가 리랜더링 된다는 걸 의미하고 이때 App 안에 있는 변수들이 초기화된다. 

'ref 올려'버튼을 눌렀을 때는 화면의 ref 숫자는 아무런 변화가 없이 초기값 0을 유지한다. ref는 useState 를 사용하는 게 아니기 때문에 버튼을 누를 때마다 화면에 그 변화된 값을 출력할 수 없다. 위에서 말했듯이 useRef Hook은 렌더링되지 않기 때문이다. 

<br/><br/>

```js
state: 4      ref: 0
```
그렇다면, state 버튼을 4번 누르고 ref 버튼을 5번 누른 뒤 다시 state 버튼을 한 번 누른다면 브라우저 화면은 어떻게 바뀔까?

<br/>

```js
state: 5    ref: 5
```
바로 위와 같이 브라우저 창이 렌더링된다. ref의 값이 5가 되었다. 왜일까? ref는 브라우저에 변화된 값을 출력할 수 없던 거 아니었나? 

정확히 말하면, ref 버튼을 눌렀을 때는 변화된 값을 즉각적으로 브라우저에 띄울 수 없다. 그럼에도 불구하고 계속 ref 버튼을 눌렀을 때 브라우저는 ref의 값을 기억하고 있다. 그저 브라우저 창에 띄우지 못할 뿐이다. 왜? useRef는 렌더링을 하지 않기 때문이다.

브라우저에 ref: 5 가 뜬 이유는 마지막에 다시 한 번 state 버튼을 눌렀기 때문이다. state버튼은 렌더를 한다. 누를 때마다 App 컴포넌트의 내부 변수들은 초기화되며 re-render 된다. 그동안 ref버튼을 눌렀을 때의 결과값은 브라우저에 보이진 않지만 잘 저장되어 있다가 state버튼을 누르는 순간 render 되면서 저장되어 있던 ref 값이 브라우저에 보이게 되는 것이다.

<br/><br/>

```js
state: 5     ref: 5
```
이 상황에서 state버튼을 한 번 누르면 어떻게 될까?

<br/>

```js
state: 6    ref: 5
```
state는 6으로 렌더 된다. 하지만 ref는 5로 값이 변하지 않고 유지된다. state 버튼을 수 십번 눌러도 중간에 ref 버튼을 클릭하지 않는 이상 ref: 5 는 그대로 유지된다.

이처럼, state는 변하는 족족 렌더되지만 그 와중에 ref 값은 변하지 않고 유지된다. ref는 어디 없어진 게 아니라 어딘가에 그 값이 잘 저장되어 있다. 렌더를 하는 순간 ref의 값을 변하게 할 수 있다.
<br/><br/><br/><br/>

# UseRef Dom

useRef는 Dom요소에 접근할 수 있다. document.querySelector처럼 말이다.

```js
const aRef = React.useRef()
<div ref={aRef}>hello</div>
```
컴포넌트가 반환하는 리액트 엘리먼트에서는 **ref={ref이름}** 이렇게 한 번만 써둔다면 그에 해당하는 엘리먼트에 한해서 Dom을 자유롭게 이용할 수 있다.


<br/><br/>

```js
const App = () => {

  const inputRef = React.useRef();
  const [state, setState] =  React.useState('Hello')
  const onClick = ()=>{
    setState('Changed! Go Check it out!');
    inputRef.current.focus();
    inputRef.current.className = 'thisisinput';
    inputRef.current.disabled = true;
    console.log(inputRef);
  }

  return(
    <div>
      <h1>{state}</h1>
      <input
      ref={inputRef}
      placeholder='here'
      ></input>
      <button onClick={onClick}>login</button>
    </div>
  )
}
```
<br/>

inputRef를 useRef Hook의 변수로 선언하고 inputRef 가 어떤 값을 반환하는 지 알아보기 위해 콘솔로그 하면 아래와 같은 결과가 콘솔창에 뜬다.

<br/>

```text
{current: input.thisisinput}
```
Dom 객체를 반환했다! 우린 이 객체로 HTML 엘리먼트에 직접 접근해서 DOM API를 이용해서 제어가 가능하다.

위에서 login 버튼을 클릭하면, 어떤 변화가 일어나는 지 보자
1. h1 엘리먼트의 state가 'Changed! Go Check it out!'로 변한다.
2. input이 focus된다.
3. input의 클래스명이 'thisisinput'로 생긴다.
4. disabled가 true가 된다.

<br/>

이렇듯 useRef 로 정말 다양한 걸 할 수 있다. 렌더링이 불필요한 요소에 대해서는 useState대신 useRef 를 사용하는 게 낫고 Dom을 이용해서 여러가지 조작할 수 있어 좋다.
<br/><br/><br/>

Ref: https://youtu.be/VxqZrL4FLz8
<br/>
2022.08.03