# 구조 분해 할당
구조 분해 할당 구문은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식입니다. (출처-MDN)<br/><br/><br/><br/>




<img style="width:350px" src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbEmbTR%2FbtrHDiFggX3%2FZbl4bTrAlMzOtzNx63eb11%2Fimg.png"><br/>
color라는 이름으로 객체를 만들고 그냥 a 또는 console.log로 color의 프로퍼티 키를 써주었더니 오류가 발생한다.

지금의 상황은 객체의 프로퍼티를 외부에서 사용할 수가 없다. (물론 color.a 를 하면 사용할 수 있지만 구조분해할당은 프로퍼티의 키 이름 그대로를 사용 가능하게 한다.)

이때 유용한 것이 구조분해 할당이다.


```js
const {?,?,?,?...} = 객체의 변수명
```
<br/><br/><br/><br/>
<img style="width:350px" src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJzNEv%2FbtrHEX8M1KX%2F54T3rY278KkNT9GcNws4Hk%2Fimg.png"><br/>
color에 대해 구조분해 할당을 했더니 외부에서 console.log 했을 때 a의 값인 red가 나오고

마찬가지로 그냥 a를 했을 때도 값이 잘 나온다.<br/><br/><br/><br/>

<img style="width:350px" src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcg8ptr%2FbtrHCXIMe0t%2Fni1rWNcrefuDdJpSWs1LG0%2Fimg.png"><br/>
d를 콘솔로그 하면 undefined가 뜬다. color 에 d라는 프로퍼티가 없기 때문이다.<br/><br/><br/><br/>

 
<img style="width:350px" src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbyZAFP%2FbtrHHkbrqyZ%2FyxJOprhSOKZGVfFfNvsrh1%2Fimg.png"><br/>
만약 d에다가 기본값을 적용하고 싶으면 구조분해 할당한 부분에다가 원하는 기본값을 적어주면 된다.

d = 'gray' 라고 기본값을 설정해두었더니

콘솔로그로 gray가 잘 출력된 것을 확인할 수 있다.

```js
const {a: 새로운 이름} = 객체의 변수명
```
<br/><br/><br/><br/>
<img style="width:500px" src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuGE2r%2FbtrHEYtf1ko%2FTJbek5LsO4m6NWGC8QZr51%2Fimg.png"><br/>
구조분해할당에다가 기존의 프로퍼티 키의 이름을 바꿀 수도 있다. 콜론 뒤에 새로 바꿀 이름을 적으면 되는데

위에 예제에서는 a : redColor 라고, a에서 redColor 로 프로퍼티 이름을 바꿔줬더니 콘솔로그로 redColor 했을 때 제대로 작동한다.

이름을 a에서 redColor로 바꾸었으니 이제 a로 무언갈 출력했을 때 오류가 발생한다.

<br/>
2022.07.19