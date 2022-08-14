# React-Redux 컴포넌트 rerender 막기

```js
//App.js
import { useSelector, useDispatch } from "react-redux";

const App = () =>{ 
  const state = useSelector(state=>state)
  console.log('3. redux state 변경으로 인한 rerender!')
  const dispatch = useDispatch();
  return (
  <>
    App{state.name}
    <button onClick={()=>dispatch({type:'INCREMENT'})}>+</button>
    <button onClick={()=>dispatch({type:'DECREMENT'})}>-</button>
  </>
  )
}
export default App;
```

```js
// store.js
import { createStore, combineReducers } from "redux";

const INITIAL_STATE = 0;
const counterReducer = (state = INITIAL_STATE, action) => {
  console.log('1. counterReducer가 실행되었습니다.')
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    default:
      return state;
  }
};

const nameReducer =(state = '#Lisa', action)=>{
  console.log('2. nameReducer가 실행되었습니다.')
  switch(action.type){
    case 'INCREMENT':
      return state + '$';
    default:
      return state;
  }
};

const store = createStore(combineReducers({
    counter: counterReducer,
    name: nameReducer,
  })
);

export default store;
```

위의 코드 상황에서 '-'버튼을 눌렀을 때 콘솔에는 아래와 같은 결과가 출력된다.

```
1. counterReducer가 실행되었습니다.
2. nameReducer가 실행되었습니다.
3. redux state 변경으로 인한 rerender!
```

1,2,3 세가지 모두 출력되는 이유를 살펴보자.

'-'버튼을 눌렀을 때, Dispatch가 {type:'DECREMENT'} 라는 액션객체를 store의 Reducer로 전달한다. store를 보면 reducer가 2개 존재한다. 하나는 counterReducer 다른 하나는 nameReducer. 둘 중에 하나가 실행될까? 아님 모두 실행될까? 정답은 reducer모두가 실행된다. 

counterReducer는 action 매개변수로{type:'DECREMENT'}를 전달받아 state를 반환한다. state 값은 최초값 0에서 -1을 한 '-1'이 되었기 때문에 변경되었다.

nameReducer는 action 매개 변수로 {type:'DECREMENT'}를 전달받았지만 해당하는 type case가 없기 때문에 default의 반환값인 state 값을 그대로 갖게 된다. state의 초기값은 '#Lisa' 이기 때문에 그대로 '#Lisa' 이며 변경되지 않았다.

'3. redux state 변경으로 인한 rerender!' 가 출력되는 이유는 App 컴포넌트가 rerender되기 때문이다. useSelector로 state를 가져올 때 위의 예제에서는 state를 통째로 가져왔기 때문에 reducer 중 하나만 바뀌어도 rerender가 되는 것이다.

바뀌지 않은 것에 대한 rerender를 막기 위해서 우리는 useSelector 함수를 정확하게 작성해야할 필요가 있다. 위에서는 state를 통으로 가져왔으니 그 반대로 state를 쪼개서 필요한 것만 가져오면 된다. 위 예제의 경우, '-'버튼을 눌러서 액션객체의 name 키의 값에 변경이 없다면 3번 콘솔이 출력되지 않기를 원하기 때문에 이를 위해서는 nameReducer만 잡아서 select하면 된다. 수정된 코드는 아래와 같다.

<br/><br/>

```js
//App.js
import { useSelector, useDispatch } from "react-redux";

const App = () =>{ 
  const nameState = useSelector(state=>state.name)
  console.log('3. redux state 변경으로 인한 rerender!')
  const dispatch = useDispatch();
  return (
  <>
    App{nameState}
    <button onClick={()=>dispatch({type:'INCREMENT'})}>+</button>
    <button onClick={()=>dispatch({type:'DECREMENT'})}>-</button>
  </>
  )
}
export default App;
```
state를 더이상 통으로 가져오지 않고 쪼개서 필요한 것만 가져올 것이기 때문에 기존에 state라는 변수 이름을 nameState로 바꾸었다. 그리고 useSelector를 이용하여 그 안의 함수를 state를 받아와 state의 name 키를 가져오도록 하였다.

위 코드를 실행시키면 '-' 버튼을 눌렀을 때 App 컴포넌트는 rerender 되지 않는다. 콘솔 출력 결과도 의도한 것처럼 3번은 출력되지 않는 아래와 같은 결과가 나온다.
```
1. counterReducer가 실행되었습니다.
2. nameReducer가 실행되었습니다.
```

참고로 a번을 b번처럼 표기해도 같은 의미라는 것을 알아두자.
```js
a : const nameState = useSelector(state=>state.name);
b : const nameState = useSelector(({name})=>name);
```

<br/><br/>

```js
//App.js
import { useSelector, useDispatch } from "react-redux";

const App = () =>{ 
  const counterState = useSelector(({counter})=>counter);
  const nameState = useSelector(({name})=>name);
  console.log('3. redux state 변경으로 인한 rerender!')
  const dispatch = useDispatch();
  return (
  <>
    App{nameState}
    <button onClick={()=>dispatch({type:'INCREMENT'})}>+</button>
    <button onClick={()=>dispatch({type:'DECREMENT'})}>-</button>
  </>
  )
}
export default App;
```
만약 state를 쪼개서 위처럼 모든 reducer를 counterState와 nameState로 각각 가져온 상태에서 '-'버튼을 누르면 콘솔 출력 결과가 어떻게 나올까? App 컴포넌트가 rerender 될까? 정답은 rerender 되어 처음과 같은 콘솔결과(1,2,3번 출력)를 얻게된다.

그 이유는 counterState의 값은 0에서 -1로 바뀌었기 때문에 위처럼 state에서 counter 키만 가져왔을 때 rerender가 된다. 만약 counterState와 nameState를 사용하면서 App 컴포넌트가 rerender되기를 원하지 않는다면 '-' 버튼의 액션 객체 type의 값을 INCREMENT도 DECREMENT도 아닌 것으로 바꾸면 된다.

<br/>
2022.08.14