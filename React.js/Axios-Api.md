# Axios

가장 많이 사용되고 있는 자바스크립트 http 클라이언트다. http 요청을 promise 기반으로 처리한다. axios를 react에서 어떻게 사용하는 지 알아보자

```js
npm install axios
```
<br/><br/>

```js
import React, { useState } from "react";
import axios from "axios";

const App = () => {
  const [data, setData] = useState(null);
  const onClick = () => {
    axios
      .get("https://jsonplaceholder.typicode.com/todos/1")
      .then((response) => {
        setData(response.data);
      });
  };
  return (
    <div>
      <div>
        <button onClick={onClick}>불러오기</button>
      </div>
      {data && (
        <textarea
          rows={7}
          value={JSON.stringify(data, null, 2)}
          readOnly={true}
        />
      )}
    </div>
  );
};

export default App;
```

불러오기 버튼을 누르면 onClick 함수가 실행되고 함수 안에 있는 axios가 실행되어 api를 가져오게 된다. 상단에 useState로 data와 setData 변수를 만들어서 api로 불러와지는 데이터를 setData 변수를 사용하여 data 안에 넣어주게 되면 data값은 더이상 초기값인 null이 아니라 api로 불러와지는 data를 갖게 된다.

JSX를 보면 data의 값이 true 일때 textarea가 나타난다. 즉, api 를 정상적으로 잘 불러오며 data는 null(false) 에서 true가 되기 때문에 textarea가 나타나고 그 안의 값을 볼 수 있게 된다.

axios.get 함수를 사용해서 파라미터로 전달된 주소에 get요청을 하고 그에 대한 결과를 .then을 통해 비동기적으로 확인할 수 있다.

<br/><br/>

## 동기와 비동기?

서버의 api를 사용해야 할 때는 네트워크 송수신 과정에서 시간이 걸리기 때문에 작업이 즉시 처리되는 것이 아니라. 응답을 받을 때까지 기다렸다가 전달받은 응답데이터를 처리한다. 이런 과정에서 해당 작업을 비동기적으로 처리한다.

<img style="width:500px" src="https://miro.medium.com/proxy/1*V5syja2casc0gCuu9zKV5g.png">

<br/><br/>

다시 돌아와서 위의 코드를 async를 적용해보자.

```js
import React, { useState } from "react";
import axios from "axios";

const App = () => {
  const [data, setData] = useState(null);
  const onClick = async () => {
    try {
      const response = await axios.get(
        "https://jsonplaceholder.typicodecom/todos/1"
      );
      setData(response.data);
    } catch (e) {
      console.log(e);
    }
  };
  return (
    <div>
      <div>
        <button onClick={onClick}>불러오기</button>
      </div>
      {data && (
        <textarea
          rows={7}
          value={JSON.stringify(data, null, 2)}
          readOnly={true}
        />
      )}
    </div>
  );
};

export default App;
```

```
 async () => {}
```
위와 같은 형식으로, 코드 블록 안에서 try와 catch 구문을 사용하여 api를 불러옵니다.

<br/><br/>

만약에 useEffect를 사용해 api를 요청할 때는 useEffect에 등록하는 함수에 async를 붙이면 안 된다. useEffect에서 반환하는 값은 뒷정리 함수이기 때문이다. 그래서 async를 사용한다면 함수 내부에 async 키워드가 붙은 또다른 함수를 만들어서 사용해야 한다.

추가로 loading 이라는 상태도 관리하여 api 요청을 불러오는 중이면 loading값이 true, 요청이 끝나면 false가 되도록 한다.

```js
import React, { useState, useEffect } from 'react';
import styled from 'styled-components';
import NewsItem from './NewsItem';
import axios from 'axios';

const NewsListBlock = styled.div`
  box-sizing: border-box;
  padding-bottom: 3rem;
  width: 768px;
  margin: 0 auto;
  margin-top: 2rem;

  @media screen and (max-width: 768px) {
    width: 100%;
    padding-left: 1rem;
    padding-right: 1rem;
  }
`;

const NewsList = () => {
  const [articles, setArticles] = useState(null);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    // async를 사용하는 함수 따로 선언
    const fetchData = async () => {
      setLoading(true);
      try {
        const response = await axios.get(
          'https://newsapi.org/v2/top-headlines?country=kr&apiKey=bae68fcaf1e24a9a980327c4e6ccd384',
        );
        setArticles(response.data.articles);
      } catch (e) {
        console.log(e);
      }

      setLoading(false);
    };
    fetchData();
  }, []);

  // 대기 중일 때
  if (loading) {
    return <NewsListBlock>대기 중...</NewsListBlock>;
  }

  // 아직 articles 값이 설정되지 않았을 때
  if (!articles) {
    return null;
  }

  // articles 값이 유효할 때
  return (
    <NewsListBlock>
      {articles.map((article) => (
        <NewsItem key={article.url} article={article} />
      ))}
    </NewsListBlock>
  );
};

export default NewsList;
```
뉴스 데이터 배열을 map 함수를 사용해 컴포넌트 배열로 변환할 때는 꼭 !article 를 조회하여 해당 값이 현재 null인지 아닌지 검사해야 한다. 이 과정을 거치지 않으면 데이터가 없을 때는 map 함수가 없기 때문에 렌더링 과정에서 오류가 발생해 흰 페이지만 보이게 된다.

<br/><br/>
2022.08.30