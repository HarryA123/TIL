# Redux Thunk

thunk는 dispatch와 getState를 받는 함수를 생성하는 함수다.

Redux에 함수를 dispatch하면 reducer로 전달하지 않고 해당 함수를 실행시켜주는 redux middleware로 전달한다.
dispatch는 일단 액션객체를 reducer로 전달하는 역할을 하는데, 액션 객체에 함수를 넣어 전달하는 방법은 통하지 않는다.

주로 redux-thunk라는 미들웨어는 API 호출이 필요할 때 쓴다.

그래서 비동기 request 를 보내고, response를 액션에 담아 dispatch하는 패턴으로 작성한다.

redux-thunk는 객체가 아닌 함수 반환을 가능하게 해준다. 액션이 함수의 형태라면 그 함수를 실행하고 실행을 마치고 객체가 되었을 때는 reducer로 dispatch해준다.

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdOsH4j%2FbtrJDiXfYaT%2FYjMfu1LIrhPCRIKusGEo30%2Fimg.png">

액션이 함수를 갖고 있다면 그 함수를 실행시키고 함수가 끝난다. 함수가 끝났을 때 객체가 있다면 그 액션객체를 reducer로 dispatch한다.

그래서 thunk를 활용하여 API를 만들고자 한다면 getState와 dispatch를 받는 함수를 먼저 생성해야 한다. 

<br/><br/>

```js
//store.js

import { createStore, combineReducers, applyMiddleware } from "redux";

const INITIAL_STATE = {
  name : '',
};

const nameReducer = (state=INITIAL_STATE, action)=>{
  console.log('reducer 실행!')
  switch(action.type){
    case 'Login' :
      return {name:action.payload};
    case 'LOGIN_SUCCESS' :
      console.log('LOGIN 성공!!!')
      return {name:action.payload};
    default :
      return state;
  }
}

const firstMiddleWare = store => next => action=> {
  console.log('Middleware에 액션 도착!', action);
  if(typeof action === 'function'){
    action(store.dispatch, store.getState)
  }
}

const store = createStore(combineReducers({
  user: nameReducer,
}),applyMiddleware(firstMiddleWare))

export default store;
```

```js
//App.js

const createLoginStart = (id) => async (dispatch, getState) => { 
  const response = await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`)
  const json = await response.json();
  dispatch({type:'LOGIN_SUCCESS', payload:json.id});
};

...

const handleClick = (e) => {
  if (idInvalid) {
    setId('');
    idRef.current.focus();
    alert('유효하지 않은 id입니다');
    e.preventDefault();
  } else if (pwInvalid) {
    setPw('');
    pwRef.current.focus();
    alert('유효하지 않은 password입니다');
    e.preventDefault();
  } else if (genderInvalid){
    alert('female 또는 male로 입력해주세요.')
    e.preventDefault();
  }
  else {
    //함수를 전달하는 dispatch, 정확히는 redux-thunk.
    dispatch(createLoginStart(id))
    // 액션객체를 전달하는 dispatch : dispatch({ type: 'Login', payload: id });
  }
};
```
위의 코드를 읽어보면, handleClick 이벤트리스너 함수가 실행되고, 만약에 조건을 모두 충족한다면 else의 dispatch를 실행하게 된다. dispatch는 원래 액션 객체를 reducer로 전달하는 역할을 하지만 우리는 API를 넘겨줄 것이기 때문에 dispatch로 createLoginStart함수를 호출해주었다.

createLoginStart 함수를 보니 dispatch, getState를 받고 있다. API 함수를 받아 firstMiddleWare라는 미들웨어가 실행되었다. 그럼 console.log로 'Middleware에 액션 도착!'과 {type: 'LOGIN_SUCCESS', payload: 4(input에 4를 입력함))} 이런 액션객체가 출력된다.

store의 미들웨어에는 이미 api 함수를 넘겼고, api 함수 뒤에 dispatch로 액션객체 {type:'LOGIN_SUCCESS', payload:json.id} 를 넘겼으므로 조건문의 else로 가서 next(action) 을 실행하게 된다. 조건문의 else로 가는 이유는 dispatch로 넘겨준 것은 typeof === 'function' 이라는 조건에 부합하지 않기 때문에 else로 가서 next(action)을 실행하게 되는 것.

<br/><br/>

nameReducer가 작동하면 콘솔은 아래와 같이 출력된다.
```
-> Middleware에 액션 도착! async (dispatch, getState) => {
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`);
    const json = await response.json();
    dispatch({
      type: 'LOGIN_SUCCESS…
-> Middleware에 액션 도착! {type: 'LOGIN_SUCCESS', payload: 55}
-> reducer 실행!
-> LOGIN 성공!!!
```

<br/>
2022.08.15