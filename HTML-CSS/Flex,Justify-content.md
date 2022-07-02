# Display : Flex;

- display:flex는 flex container에 적용한다. (container가 아닌 items에 적용하면 변하지 않음.)
- flex container에 적용하면 container 안에 items는 수평으로(row) 정렬된다.<br/><br/><br/>

## display:flex
block 요소와 같이 flex container에 적용된다.<br/><br/>
![](https://blog.kakaocdn.net/dn/G6AGe/btrGfUTXcrn/cJMEk5kEuRdl99LgXrevp1/img.png)<br/><br/><br/>

## display:inline-flex
inline 요소와 같이 flex container에 적용된다.
![](https://blog.kakaocdn.net/dn/b3zs48/btrGmoZR9Lc/Cd6ELPQ3FHWeeILFPL50N0/img.png)<br/><br/><br/>

### display:flex 와 display:inline-flex 차이점
display:flex는 container가 block의 형태를 유지하면서 그 안에 있는 items를 row로 정렬하지만 display:inline-flex는 inline의 형태로 items를 row로 정렬한다.<br/><br/><br/>

### 주의사항
items에 넣지 않도록 조심하자. **무조건 container에 넣을 것!**