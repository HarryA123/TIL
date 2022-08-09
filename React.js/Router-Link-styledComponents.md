# Router의 Link에는 어떻게 styled-components를 적용할까?

개인 프로젝트를 하면서 styled-components를 적용해서 css를 입히다가 Link 에다가 css를 주어야 하는 상황을 맞닥뜨렸는데, 대체 이걸 어떻게 해결해야 하는지 문제가 발생했다.

```js
const StyledTite = sytled.h3`
	color: red;
	background: black;
`
...

<StyledTite><Link to={'/'}>Title</Link></StyledTite>
```

위의 코드가 전혀 먹히질 않는 상황에서 구글링으로 해답을 찾았다!

<br/><br/><br/>

```js
const StyledLink = styled(Link)`
	color: red;
	background: black;
	}
`;

<StyledLink to={'/'}>Title</StyledLink>
```

Router Link 에 styled components를 적용하고 싶을 때는 styeld.(Link)를 해주어야 한다. 그리고 그렇게 만든 변수 StyledTitle로 Link tag를 대체하면 된다.

<br/><br/><br/>

```js
const StyledTitle = styled(Link)`
	color: red;
	background: black;

  	&:hover {
      color: red;
      background: blue;
	}
`;
```

또 해당 엘리먼트를 hover, active, focus, visited 등의 표시를 하고 싶을 때는 위처럼 작성한 뒤에 중괄호 안에다가 해당 css를 작성하면 된다.

<br/><br/><br/>

```js
&:hover{color: red;}, &:focus{color: pink;}
```

focus할 때도 css를 적용하고 싶다면 위와 같이 작성한 뒤 중괄호 안에 내용을 쓰면 된다. 

<br/><br/><br/>

```js
&:hover, &:focus, &:active{
	color: blue;
}
```
위와 같이 작성하면 hover, focus, active 가 발생했을 때의 color는 공통적으로 blue가 된다.

<br/>
2022.08.10