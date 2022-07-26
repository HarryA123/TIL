# ReactDOM-JSX-babel


## 
클릭하면 console.log로 clicked!를 반환하는 버튼을 js로 만들어보자.
```html
<button id="clickBtn">click!</button>
```
```js
// 1번
const btn = document.querySelector('#clickBtn')
btn.addEventListener('click', ()=>console.log('clicked!'))
```
<br/><br/><br/>

위와 같은 코드를 React.js에서는 덜 번거롭게 표현할 수 있다.

```html
<div id="root"></div>
```
```js
// 2번
  const root = document.querySelector('#root')
  const btn = React.createElement('button',{ onClick: ()=>console.log('clicked!')}, 'click!')
  
  ReactDOM.render(btn, root)
```
React.js에서는 Element를 생성과 동시에 여러가지 속성,  EventListener를 달아줄 수 있다. 위의 예시에서는 button 요소를 btn 변수 선언과 동시에 onClick이라는 EventListener 를 실행시켜 console.log 하면 clicked가 뜨게끔 했다. 그리고 button의 value를 세 번째 인자로 받아 click! 으로 설정해주었다.(elements ,props , contents)

이렇게 한 줄로 코드가 끝나버리니 정말 간단하다.

<br/><br/>

(다만 주의할 점은 EventListener를 할 때 js에서 하던 것처럼 'click'만 해서는 안 되고 on을 붙이고 따옴표를 빼야하고 camelCase를 사용한다. - onClick, onMouseEnter, onScroll 등...)

나머지로는 ReactDOM을 이용해서 btn을 root에 집어넣는 render 작업만 해주면 화면에 정상적으로 작동한다.
ReactDom은 js로 따지면 appendChild 비슷한 개념이다.

근데 위에 코드를 React에서는 더 간단하게 줄인다. 위 react 코드에서는 createElement를 했는데, React 개발자들은 이것을 사용하는 일이 거의 없다.
<br/><br/><br/>
# JSX
JSX는 JS에 XML을 추가한 확장 문법이다. 공식적인 JS문법은 아니지만 대부분의 React 개발자들이 JSX문법을 사용한다. 사용하려면 Babel을 끌어와야 한다. 우리에게 익숙한 html 문법처럼 생겼기 때문에 가독성 측면에 장점이 있다.

위에 작성했던 react 코드를 JSX로 표현해보자.

```js
// 3번
  const root = document.querySelector('#root')
  
  const btn = (
    <button 
    style={{
      backgroundColor:'yellow',
    }}
    onClick={()=>console.log('clicked!')}>
    click!
    </button>
    );

  ReactDOM.render(btn, root)
```
html 문법과 거의 유사한 형태다.
button 안의 속성들을 html에서 속성을 넣어주는 방식대로 하면 그대로 완성된다. 3번에서는 추가적으로 style을 적용했다. 할당문을 시작할 때는 중괄호를 열어야 한다는 점만 다를 뿐 그 외는 다 익숙한 방법이다. React 개발자들은 위와 같은 방법을 사용한다.
<br/><br/><br/>

그럼 아래에 있는 ReactDOM의 형식도 JSX를 사용해서 바꿔보자.

```js
// 4번
  const root = document.querySelector('#root')
  
  const btn = (
    <button 
    style={{
      backgroundColor:'yellow',
    }}
    onClick={()=>console.log('clicked!')}>
    click!
    </button>
    );

  ReactDOM.render(<btn/>, root)
```
ReactDOM.render에서는 btn또한 </>태그로 묶어서 표기할 수 있다.
하지만 위처럼 하면 에러가 뜬다. 왜냐하면 컴포넌트의 첫 글자를 대문자로 쓰지 않았기 때문이다. 그럼 첫 글자를 대문자로 바꿔보자.
<br/><br/><br/><br/>

```js
// 5번
  const root = document.querySelector('#root')
  
  const Btn = (
    <button 
    style={{
      backgroundColor:'yellow',
    }}
    onClick={()=>console.log('clicked!')}>
    click!
    </button>
    );

  ReactDOM.render(<Btn/>, root)
```

btn을 Btn으로 첫 글자를 대문자로 바꾸었는데도 위의 결과는 에러가 나온다.
왜그럴까? Btn 변수를 함수로 바꿔야 render에서 Btn을 인식하기 때문이다. arrow function을 이용해서 다시 바꿔보자.
<br/><br/><br/><br/>

```js
// 6번
  const root = document.querySelector('#root')
  
  const Btn = ()=> (
    <button 
    style={{
      backgroundColor:'yellow',
    }}
    onClick={()=>console.log('clicked!')}>
    click!
    </button>
    );

  ReactDOM.render(<Btn/>, root)
```
위 6번 예제처럼 작성해야 에러없이 작동한다.

<br/><br/>




## babel

[Try babel!](https://babeljs.io/repl) 


<br/>
2022.07.26<br/>
리액트를 왜 사용하는 지 몰랐었는데, 오늘 공부하고 사용해보니까 확실히 문법이 보기 깔끔하고 복잡하지 않아 좋은 것 같다. Babel 이라는 게 뭔가 궁금했었는데, 컴파일러 중 하나라는 걸 알게 됐다.




