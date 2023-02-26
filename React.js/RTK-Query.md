# RTK Query

redux toolkit 에서 지원하는 createAsyncThunk API를 사용하면 엄청난 리듀서 로직을 작성해야 한다. 그리고 양이 방대할 수록 로직도 복잡해진다.

이를 보완하기 위해 나타난 것이 RTK Query 다.
RTK Query는 Redux에 비해 적은 양의 코드로 상태관리를 할 수 있다.(API 요청부터 store 저장 단계까지 쭉 이어서 처리하기 때문이다)
isLoading 같은 변수를 이용해 Data를 받아오기 전에 특정 UI를 보여줌으로써 UX 향상도 가능하다.


</br></br>

RTK Query 에는 다음의 API가 포함되어 있다.

- createApi() : RTK Query의 핵심. base URL당 하나의 API slice 를 사용해야 한다.  
- fetchBaseQuery() : 간단한 요청을 위한 fetch의 래퍼.
- <ApiProvider/> : Redux store가 없을 시 Provider로 사용 가능하다.
- setupListeners() : refetchOnMount와 refetchOnReconnect 기능 사용을 위한 유틸리티.

</br></br>


# RTK Query 사용
## 1 

```js
import { createApi } from '@reduxjs/toolkit/query'

/*리액트 엔트리 포인트를 명시하면 자동으로 정의된 엔드포인트의 훅을 생성합니다 -> 아직은 잘 안 와닿아서 사용해보면서 이해해야 할듯 */
import { createApi } from '@reduxjs/toolkit/query/react'
```

</br></br>

## 2 

```js
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react'
import type { Pokemon } from './types'

// Define a service using a base URL and expected endpoints
export const pokemonApi = createApi({
  reducerPath: 'pokemonApi',
  baseQuery: fetchBaseQuery({ baseUrl: 'https://pokeapi.co/api/v2/' }),
  endpoints: (builder) => ({
    getPokemonByName: builder.query<Pokemon, string>({
      query: (name) => `pokemon/${name}`,
    }),
  }),
})

// Export hooks for usage in functional components, which are
// auto-generated based on the defined endpoints
export const { useGetPokemonByNameQuery } = pokemonApi
```

위처럼 createApi 를 사용한다. 객체 0번째 reducerPath를 'pokemonApi' 로 정의한다. 만약 명시하지 않으면 api가 디폴트로 정해진다. 1번째에는 baseQuery 를 정의한다. 값으로는 fetchBaseQuery 래퍼로 baseUrl을 정의한다. 2번째로는 endpoints를 정의하는데, 각각의 query/mutation 동작을 여기서 정의한다. 위 예제에서는 Pokemon의 이름을 GET해오는 동작이다. 호출에서 name 값을 받는다.

</br></br>

## 3

```js
import { configureStore } from '@reduxjs/toolkit'
// Or from '@reduxjs/toolkit/query/react'
import { setupListeners } from '@reduxjs/toolkit/query'
import { pokemonApi } from './services/pokemon'

export const store = configureStore({
  reducer: {
    // Add the generated reducer as a specific top-level slice
    [pokemonApi.reducerPath]: pokemonApi.reducer,
  },
  // Adding the api middleware enables caching, invalidation, polling,
  // and other useful features of `rtk-query`.
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(pokemonApi.middleware),
})

// optional, but required for refetchOnFocus/refetchOnReconnect behaviors
// see `setupListeners` docs - takes an optional callback as the 2nd arg for customization
setupListeners(store.dispatch)
```

store는 위와 같은 구조로 작성하는데, 조금 다른 점이라고 하면 configureStore  리듀서 안에서 써지는 방식이다. ([pokemonApi.reducerPath]: pokemonApi.reducer)

</br></br>

## 4

```js
import * as React from 'react'
import { useGetPokemonByNameQuery } from './services/pokemon'

export default function App() {
  // 자동으로 데이터를 패치하고 query 값을 리턴하는 쿼리 hook을 사용한다.

  const { data, error, isLoading } = useGetPokemonByNameQuery('bulbasaur')
  // 각각의 훅들은 아래의 endpoints로 접근할 수 있다.
  // const { data, error, isLoading } = pokemonApi.endpoints.getPokemonByName.useQuery('bulbasaur') <- 이런식으로도 사용 가능함.
  // 데이터와 로딩 상태에 따라 UI 를 렌더한다.
}
```
RTK Query는 자동으로 컴포넌트가 마운트될때 데이터를 패치하고, 파라미터가 바뀔 때 다시 패치를 해서 {data, isFetching} 값들을 제공하고 컴포넌트를 리렌더한다.

