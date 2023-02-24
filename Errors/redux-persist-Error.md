 # 의도


프로젝트에 브라우저 창을 닫으면 유저 정보가 없어지게 하는 세션 스토리지 추가 작업을 했다.(새로고침해도 로그인이 유지됨)

로컬 스토리지를 선택하지 않은 이유

굳이 영구적으로 정보를 갖고 있을 필요가 있나? 싶어서 세션 스토리지를 선택했다.

redux persist 를 적용하려고 store.js 파일을 건드렸는데

```js
import { combineReducers, configureStore } from "@reduxjs/toolkit";
import movieSlice from "./features/movieSlice";
import userSlice from "./features/userSlice";
import storage from "redux-persist/lib/storage";
import sessionStorage from "redux-persist/es/storage/session";
import { persistStore, persistReducer } from 'redux-persist'

const rootPersistConfig = {
  key: "root",
  storage,
};

const userPersistConfig = {
  key: "user",
  storage: sessionStorage,
};

const rootReducer = combineReducers({
  movie: movieSlice.reducer,
  user: persistReducer(userPersistConfig, userSlice.reducer),
});

const persistedReducer = persistReducer(rootPersistConfig, rootReducer);

export const store = configureStore({
  reducer: persistedReducer,
});

export const persistor = persistStore(store);
```
</br></br></br>

# 에러 발생
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb9dOy6%2FbtrWbVpd34f%2Fmv8155MxElonAZPMmboomK%2Fimg.png">

```
A non-serializable value was detected in an action, in the path: `register`. Value: ƒ register(key) {
    _pStore.dispatch({
      type: _constants__WEBPACK_IMPORTED_MODULE_0__.REGISTER,
      key: key
    });
  } 
Take a look at the logic that dispatched this action:  {type: 'persist/PERSIST', register: ƒ, rehydrate: ƒ}
```

</br></br></br>

# 해결

리덕스 툴킷 공식문서에는 이렇게 쓰여 있다.

If using Redux-Persist, you should specifically ignore all the action types it dispatches:
 

디스패치하는 모든 액션타입들을 특별히 ignore 해주어야 한다고 되어 있다.

이걸 ignore 하지 않았기 때문인 것 같아 공식문서 예제를 참고해서 다음과 같은 코드로 수정했다.

 ```js
 import { combineReducers, configureStore } from "@reduxjs/toolkit";
import movieSlice from "./features/movieSlice";
import userSlice from "./features/userSlice";
import storage from "redux-persist/lib/storage";
import sessionStorage from "redux-persist/es/storage/session";
import {
  persistStore,
  persistReducer,
  FLUSH,
  REHYDRATE,
  PAUSE,
  PERSIST,
  PURGE,
  REGISTER,
} from 'redux-persist'


const rootPersistConfig = {
  key: "root",
  storage,
};

const userPersistConfig = {
  key: "user",
  storage: sessionStorage,
};

const rootReducer = combineReducers({
  movie: movieSlice.reducer,
  user: persistReducer(userPersistConfig, userSlice.reducer),
});

const persistedReducer = persistReducer(rootPersistConfig, rootReducer);

export const store = configureStore({
  reducer: persistedReducer,
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: {
        ignoredActions: [FLUSH, REHYDRATE, PAUSE, PERSIST, PURGE, REGISTER],
      },
    }),
});

export const persistor = persistStore(store);
 ```


</br></br></br>

 - 참조 링크 : https://redux-toolkit.js.org/usage/usage-guide#working-with-non-serializable-data
