영화 정보 페이지를 만들다가 오류가 생겼다.

input에다가 영화 이름을 검색하면, 내가 검색한 text가 포함된 영화 정보 리스트들이 다시 fetch 되어서 text와 연관된 리스트들을 보여줘야 하는데, 자꾸 아래와 같은 에러가 반복해서 나타났다.


내가 사용한 코드는 아래와 같다.

<br/><br/>

```js
import { useEffect, useRef, useState } from "react";
import Movie from "../components/Movie";

function Home(){
  const [loading, setLoading] = useState(true);
  const [movies, setMovies] = useState([]);
  const [movieSearch, setMovieSearch] = useState('');
  const [movieName, setMovieName] = useState('');

  const getMovies = async () => {
    const json = await (
      await fetch(
        `https://yts.mx/api/v2/list_movies.json?minimum_rating=8&page=${Math.round(Math.random()*100)}&query_term=${movieName}&sort_by=year`
      )
    ).json();
    setMovies(json.data.movies);
    setLoading(false);
  };

  const onChange = (event) =>{
    setMovieSearch(event.target.value)
  }

  const onSubmit = (event)=>{
    event.preventDefault();
    setMovieName(movieSearch)
  }

  useEffect(() => {
    getMovies();
  }, [movieName]);

  return (
    <>
    <h4>Search</h4>
    <form onSubmit={onSubmit}>
      <input
      onChange={onChange}
      type="text"
      value={movieSearch}
      placeholder="..."
      ></input>
    </form>
      {loading ? (
        <h3>Loading</h3>
      ) : (
        <div>
          {movies.map((item) => (
            <Movie
              key={item.id}
              id={item.id}
              title={item.title}
              year={item.year}
              medium_cover_image={item.medium_cover_image}
              rating={item.rating}
              runtime={item.runtime}
              genres={item.genres}
              summary={item.summary}
            />
          ))}
        </div>
      )}
    </>
  );
}
```


export default Home
템플릿 리터럴을 사용해서 query_term={movieName} 이 변경할 때마다 useEffect가 실행되어 fetch를 rerender해주고 싶었다.

<br/><br/>

그러기 위해서 input을 submit 하면 발생하는 onSubmit 이벤트를 아래와 같은 코드로 작성했다.
```js
  const onSubmit = (event)=>{
    event.preventDefault();
    setMovieName(movieSearch)
  }
  ```
일단 새로고침 되는 submit 이벤트 리스너의 기본설정을 preventDefault로 막아주고 input 에 입력된 값 movieSearch를 setMovieName이 가져갈 수 있도록 만들었다.
위 상황은 movieName이 이제 내가 방금 input에 입력한 값이 된다.

그런 뒤 useEffect에는 movieName 이 바뀔 때마다 fetch API 를 해와야 함으로 dependency array 안에 movieName을 넣어줬다.

그런데도 ! 같은 오류가 발생했다.

stackOverflow에 물어보고 답변을 기다리는 동안 나 혼자 뭐가 문제일까 풀어보다가 해결했다!!

<br/><br/>

```js
const getMovies = async () => {
    const json = await (
      await fetch(
        `https://yts.mx/api/v2/list_movies.json?minimum_rating=8&page=${Math.round(Math.random()*100)}&query_term=${movieName}&sort_by=year`
      )
    ).json();
    setMovies(json.data.movies);
    setLoading(false);
  };
```

문제는 page 옆에 있는 템플릿 리터럴이었다. 이걸 지우니까 모든 게 에러 없이 잘 작동했다.

이걸 혹시나 해서 지워본 이유는 내가 만약 검색창에 lady라고 쓰면 query_term=lady 라고 적용이 될텐데, 그럼 page에는 뭐가 나올까? 생각을 해보니, 이 api가 lady를 포함하는 영화를 그렇게 많이 갖고 있지 않을 수도 있겠다는 생각이 들었다.

그래서 만약 api가 paage=44&query_term=lady 를 했다면...? 당연히 오류가 나온다. 실제로 이렇게 쳐보니까 lady를 포함하는 영화가 별로 없어서 랜덤 숫자로 운 좋아서 1페이지 걸리면 lady가 출력되는 거다.

이것만 지웠더니 정상적으로 잘 작동했다!!!

<br/><br/>

## 해결
```js
  const getMovies = async () => {
    const json = await (
      await fetch(
        `https://yts.mx/api/v2/list_movies.json?minimum_rating=8&page=&query_term=${movieName}&sort_by=year`
      )
    ).json();
    setMovies(json.data.movies);
    setLoading(false);
  };
```

이제 검색한 영화 결과가 없으면 에러가 아니라 영화가 없다는 text가 뜨도록 예외처리를 해줘야겠다.

