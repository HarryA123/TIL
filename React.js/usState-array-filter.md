# How to delete array elements using filter() in React

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbM5OJ%2FbtrI1OJktr7%2FBKSFdFgDdVyZkgLfx7tVik%2Fimg.png">
<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbLBaS4%2FbtrI4VAAuee%2FwEhoHoWGns7uF3W34xcrG1%2Fimg.png">


<br/><br/>

```js
const [list, setList] = useState([])
...

<ul>
{list.map((item,index)=>
  <li key={index}>{item}

  <button onClick={()=>{
    setList(curToDos => alert(curToDos));
  }}>✖</button>
  </li>
  )
}
</ul>
```

브라우저 리스트를 보면 A,B,C,D,E 가 있고 콘솔로 그 리스트를 찍어보면 하나의 배열 안에 각 인덱스를 달고 A,B,C,D,E로 들어가 있는 모습을 확인할 수 있다.

<br/>

이 배열에서 X버튼을 누르면 E가 사라지게 하고 싶은데, 배열에 있는 요소를 지우기 위해서 filter() 메소드를 사용해보자. 

<br/>

나는 리스트가 들어있는 배열을 바꾸고싶고, 그 배열은 useState 변수로 선언이 되었기 때문에 useList 라는 (setter) setState를 사용해서 배열에서 원하는 요소를 삭제할 것이다. 그래서 onClick 함수가 setList 먼저 반환하도록 만들었다. setList( // contents //)

<br/><br/>

1. 최근의 배열을 넘겨주자.

setState는 일단 previous, current 값을 인자로 갖고 있다. 최신의 업데이트된 값이다. 즉 set(something=> alert(something))을 하면 something 이라는 변수에 들어간 배열을 확인할 수 있다.

 
```js
setList(curToDos => curToDos.filter((_, curIndex) => curIndex !== index));
    1      2            2      3     4      5           5           6
```

<br/>

위의 한 줄 코드를 보자. 1번 setList 가 매개 변수로 2번 curToDos 를 설정하고 반환값으로 curToDos에 filter 메소드를 적용했다.  여기까지 정리하자면, 2번 curToDos 에는 배열이 들어있다. 방금전까지 우리가 map으로 넣어준 리스트들이 들어있다. 즉, A,B,C,D,E 가 들어있는 배열 인자를 curToDos 라는 매개변수로 받았다.

<br/><br/>

1. 이제 2번 배열에 필터 메소드를 적용하자.

filter는 첫 번째 인자로 각 배열의 element를 받고, 두 번째 인자로는 그 element의 index를 받는다. 세 번째 인자로는 그 배열 자체를 갖는다. 4번과 5번을 보면 element와 index를 각각 _ 와 curIndex로 설정해뒀다.

4번 _ 에는 A,B,C,D,E 가 순차적으로 들어오게 될 것이고 5번 curIndex는 그 배열의 index가 들어간다.

여기까지 정리를 해보면 4번과 5번은 이미지 2번의 배열 모습과 똑같은 형태를 갖고 있다.

```js
A : 0
B : 1
C : 2
D : 3
E : 4
```

<br/><br/>

5. filter() 메소드는 조건을 만족하는 element로 구성한 배열을 반환한다.

filter의 반환부분을 보자, 

 => curIndex !== index));

curIndex가 index 아니면 통과되어 배열을 구성한다. 6번의 index는 내가 버튼을 누른 그 위치의 index를 의미한다. 나는 E를 눌렀으니까 4번이 index 자리에 들어가게 된다.

다시 코드를 해석해보면 curIndex 가 4가 아니면 배열로 들어가고 4면 배열로 들어갈 수 없다.

```js
A : 0    ->   들어감
B : 1    ->   들어감
C : 2    ->   들어감
D : 3    ->   들어감
E : 4    ->   못 들어감✖!!!
```

그래서 네 번째 index E는 배열에서 없어진다. 삭제 기능이 완성됐다!



Ref: [techiediaries](https://www.techiediaries.com/react-usestate-hook-update-array/)
, [bobbyhadz](https://bobbyhadz.com/blog/react-remove-element-from-state-array)
<br/><br/>
2022.08.06

이거 이해하느라 진짜 노력했다!👏😁