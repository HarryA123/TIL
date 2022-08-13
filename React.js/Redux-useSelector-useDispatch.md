# Redux 이해하기 (1)

## createStore, combineReducers

<br/>
createStore 와 combineReducers 함수들은 store를 만들면 getState와 dispatch 함수를 가질 수 있다.

store.dispatch() 메소드는 액션 객체를 파라미터로 받는 함수다  갖고 있는 모든!! 리듀서를 실행시킨다.

실행 시킬 때 state라는 파라미터에 현재값을 넣어주고 두 번째 인자로 새로운 액션객체를 넣는다.

이전 값이 1이었다면 새로운 액션객체를 받아 1+ 새로운 액션객체 가 된다.

<br/><br/>

```js
import { Provider } from 'react-redux' 
import store from './store'; 
 ~~~ 
root.render( 
  <Provider store={store}> 
    <App /> 
  </Provider>
)
```


Provider를 임포트해서 스토어를 자식컴포넌트들에 Prop으로 넘겨주고 있다. context랑 같은 것은 아니다. store는 하나의 거대한 객체다. 레퍼런스는 영원히 바뀌지 않는. 
컨텍스트는 참조값이 바뀌어야 사용하고 있는 컴포넌트들을 업데이트하는데, 스토어는 참조값이 절대 안 바뀌기 때문에 리렌더링 이슈로부터 자유로울 수 있다. 

리덕스에서는 useSelector, useDispatch를 제공하고 있다.useSelector 함수로 현재 스테이트 값을 가져오고, useDispatch로는 액션 디스패치가 가능하다. 즉 dispatch는 액션객체를 reducer로 전달하는 역할을 한다.

<br/><br/>

```js
// App.js

import { useSelector, useDispatch } from "react-redux";

const App = () =>{ 
  const state = useSelector(state=>state)
  console.log(state)
  return <>App</>;
}
export default App;

-> {counter:0}
```
react-redux에서 useSelector와 useDispatch 함수를 import하여 가져왔다.

그리고 App 컴포넌트에 state 변수를 선언하는데 그 할당값으로는 useSelector함수가 들어있다.

useSelector는 store에 있는 state를  통째로 가져오는 역할을 한다.

그래서 콘솔로 state를 찍었을 때, {counter:0} 이러한 객체가 나오게 된다.



{counter:0} 이러한 객체가 나오는 이유는 무엇인지 store.js 로 가서 확인해보자.

<br/><br/>

```js
// store.js
import { createStore, combineReducers } from "redux";

const INITIAL_STATE = 0;
const counterReducer = (state = INITIAL_STATE, action) => {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    default:
      return state;
  }
};

const store = createStore(combineReducers({
    counter: counterReducer,
  })
);

export default store;
```
store에는 redux로부터 createStore와 combineReducers 를 import하여 가져왔다.

createStore는 앱의 상태 트리 전체를 보관하는 redux 스토어를 만드는 역할을 한다. 이때 스토어는 앱 내에서 단 하나만 존재할 수 있다. createStore는 인수로 reducer를 받는다. 주어진 현재 상태 트리와 액션에서 다음 상태 트리를 반환하는 리듀싱 함수인 reducer를 의미한다. createStore가 반환하는 것은 앱 전체 상태를 갖고 있는 객체다. 이 객체의 상태를 바꾸는 방법은 유일한데, 바로 액션을 바꾸는 것이다.

위에서는 createStore로  combineReducers()를 사용하였는데, 그 안에 객체가 counter : counterReducer 로 구성되어 있다. counterReducer를 따라가면 state를 초기값인 0으로 하고 action을 받고 있다.

방금 전 counter: 0 에서 볼 수 있듯 할당값으로 0이 나온 이유는 counterReducer의 반환값이 0이기 때문이다.


<br/><br/>


```js
// App.js 
import { useSelector, useDispatch } from "react-redux";

const App = () =>{ 
  const state = useSelector(state=>state)
  console.log(state)
  const dispatch = useDispatch();
  return (
  <>
    App{state.counter}
    <button onClick={()=>dispatch({type:'Hello'})}>+</button>
  </>
  )
}
export default App;
```
```js
// Store.js
import { createStore, combineReducers } from "redux";

const INITIAL_STATE = 0;
const counterReducer = (state = INITIAL_STATE, action) => {
  console.log(state, action)
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    default:
      return state;
  }
};

const store = createStore(combineReducers({
    counter: counterReducer,
  })
);

export default store;
```
만약 이렇게 코드를 변경시켰다면 버튼을 클릭할 때마다 콘솔에 어떤 결과가 찍힐까?

일단 App.js를 살펴보면 버튼에 클릭 이벤트를 걸어 그 이벤트 함수로 dispatch함수를 넣어주었다. dispatch는 useDispatch함수를 실행시키는데, 이는 액션객체를 리듀서로 보내는 역할을 한다. 리듀서의 위치는 store에 있다.

그래서, useDispatch 함수를 사용하면 우리는 리듀서에 어떤 명령(?) 을 보내고 싶은 거고 그 명령이라 함은 액션 객체를 의미한다. 그래서 App.js 에서 disptach({type:'Hello'}) 가 되는 것이다. 액션 객체가 위의 상황처럼 만약에 { type: 'Hell'} 라고 한다면 이 액션객체를 받은 dispatch가 리듀서로 보내진다. store에 위치한 리듀서 createReducer 는 이 액션 객체를 받는다. 이 액션객체를 매개변수로 받은 리듀서는 state 초기값이 0이며, 다음 action이라는 매개변수로 넘어온 {type:'Hello'} 를 읽는다. 하지만 counterReducer 내에는 type이 'Hello' 일때의 특정 케이스가 존재하지 않는다. 오직 INCREMENT와 DECREMENT 뿐이기 때문에 default로 가서 반환값인 state 0 을 그대로를 갖게 되는 것이다.



그래서, + 버튼을 누를 때마다 우리는 화면에 있는 state.counter가 카운트 되는 것을 볼 수 없고 콘솔로 0 {type:'Hello'} 가 찍히는 것만 확인할 수 있다.


<br/>
2022.08.13