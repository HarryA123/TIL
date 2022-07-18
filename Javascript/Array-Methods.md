# Array Methods

## Array.concat()

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fboy82F%2FbtrHvnnbGGG%2FD5gSEggWXvKZ4Dld8u1Kok%2Fimg.png"><br/>

concatenate 는 사슬같이 잇다라는 의미로, concat() 메소드는 array의 아이템들을 한 줄의 사슬처럼 이어주는 역할을 한다.

위의 예제에서 number.concat(color)를 콘솔로그 했더니 (7) [1, 2, 3, 44, 'red', 'yellow', 'blue'] 라는 배열이 출력됐다. 보면 하나의 사슬처럼 이어졌다.<br/><br/><br/><br/>

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTQvWB%2FbtrHCXAiNKZ%2FDjvm4ajco9tzTavXV6IH7k%2Fimg.png"><br/>

그 외에도 이렇게 배열 안에 배열을 만들어서 concat으로 엮을 수 있는데, 이렇게 하면 배열 안의 배열을 하나의 아이템으로 보기 때문에 출력 결과는 (7)개의 아이템이 나오는 것이 아니라 위 사진처럼 (5) or (4) 개의 아이템이 나올 수 있다.<br/><br/><br/><br/>

<img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdwxriJ%2FbtrHCnMOXcV%2FmX2Pa5GfdJ6Hlz8kYyCgkk%2Fimg.png"><br/><br/>

그리고 위 사진처럼 concat 안에 orange, purple을 직접 넣어도 출력 결과에는 순서에 맞게 배열되어 나온다.<br/><br/><br/><br/>


## forEach()

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcW7edi%2FbtrHDbSGB0b%2FyFOL7h2YwpxfWHjWTfuGkK%2Fimg.png"><br/>
배열 데이터(위에서는 color)의 아이템 개수만큼 콜백함수를 반복적으로 실행하는 용도로 쓰인다.

위에서 forEach 메소드 안 인수 자리에 함수를 넣은 것을 '콜백(callback)'이라고 한다.

color 에는 3개의 아이템이 있기때문에 red, yellow, blue 각 3개씩 출력되었다.<br/><br/><br/><br/>

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F56nuE%2FbtrHCWVNetA%2FS71aC0gPNMlnNkDlxMnJXK%2Fimg.png"><br/>

만약 위처럼 color에 아이템을 두 개 더 추가했다면 forEach 메소드를 돌렸을 때 각 컬러가 5개씩 출력되고 그 옆에 매개변수에 넣은 index도 차례대로 출력된다.<br/><br/><br/><br/>

 

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmAtG6%2FbtrHBBq2JaD%2FOJJHPU7zm7KNbthc4sBGCK%2Fimg.png"><br/>

color라는 변수에 orange와 purple을 또 하나의 배열로 넣어주면,

forEach 메소드는 이 배열을 하나의 아이템으로 인식하고 그 배열 아이템을 세 번째 인덱스로 배치한다.

그리고 콜백함수는 저것보다 더 간단한 화살표 함수로, 아래와 같이 바꿔줄 수 있다.
```js
color.forEach((item, i) => console.log(item, i))
```
<br/><br/><br/><br/>
## map()

<img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFO94N%2FbtrHCWuM7mx%2FjST8VjutjvEXiTtIOD7sMk%2Fimg.png"><br/>

map() 메소드는 배열 데이터의 아이템을 토대로 콜백함수를 반복적으로 실행하여 새로운 배열을 만들어주는 역할을 한다.

어떤 점에서 보면 forEach() 메소드와 비슷하다고 볼 수 있지만 map()메소드는 콜백이 반환하는 데이터를 가지고 모아 놓은 데이터를 새로운 배열로 만든다. return으로 데이터를 반환해야 한다.<br/><br/><br/><br/>

<img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCla7g%2FbtrHrvyGkch%2FSimZ2hJPQKEPIMn2gWaff1%2Fimg.png"><br/>

처음에는 return이 아니라 console.log로 출력하고 newArray 변수를 썼더니 배열 안에는 undefined가 뜬다. 그래서 아래처럼 꼭 return으로 데이터를 반환해야 한다.

위에 사용된 콜백함수도 화살표 함수로 간단하게 바꿀 수 있다.

```js
const newArray = color.map((item, i) => `${item} : ${i} 번 입니다`)
```
<br/><br/><br/><br/>

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fckc2dF%2FbtrHCXN0qM1%2FmGa1PQVNr2OLm8mzFKxju0%2Fimg.png"><br/>
return을 객체로 할 경우 () 소괄호 안에 중괄호 속 내용을 넣어 화살표 함수로 표현할 수 있다.<br/><br/><br/><br/>


## filter()

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcrWE6E%2FbtrHCoyk1xz%2FXslf5X5TNqY7uhCrA63bUk%2Fimg.png"><br/>
filter() 메소드는 배열데이터 안에 있는 각각의 아이템들을 특정한 기준에 의해 필터링 한다.

새로운 변수를 만들어서 filter된 아이템들에 한해서 배열을 만들 수 있지만, 굳이 배열을 새로 만들 필요가 없다면 console.log로만 배열을 출력할 수도 있다. filter를 통한 새로운 배열이 필요하다면 변수를 선언하고 filter메소드를 사용하면 된다.

filter() 메소드와 map() 메소드는 둘 다 return으로 데이터를 반환한다. filter는 연산자를 사용해서 참에 해당하는 것만 return 한다.

<details>
<summary>그럼 의문이 드는 게 map으로는 filter의 기능을 수행할 수 없나?</summary>
<div markdown="1">

<img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJBNLq%2FbtrHCpxjsbm%2F7oK3di6yFz7WYg0EJiku9K%2Fimg.png"><br/>
위 사진을 보면 알 수 있듯이 map에다가 연산자로 5보다 큰 수를 return하면 boolean으로 형성된 새로운 배열을 만든다.

map() 은 filter() 의 기능을 수행하지 못한다. filter()를 쓰자.

</div>
</details>
<br/><br/><br/><br/>


## find()

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEr0qw%2FbtrHwliC4p0%2FzkGL3gvZgnZQ43kChgQ9Zk%2Fimg.png"><br/>

find() 메소드는 콜백함수에 해당하는 아이템들을 찾고, 그 중에서 첫번째 아이템만을 반환한다.

처음에는 find()가 filter()랑 다를 게 뭐야? 했는데 둘은 다르다. find는 첫번째 아이템만 반환하기 때문이다.

그래서 find0 메소드를 쓰면 그건 새로운 배열로 만들어 주는 것도 아니고 그냥 콜백함수에 해당하는 그 첫번째 아이템만 반환하기 때문에 확실히 filter랑 다르다.<br/><br/><br/><br/>


<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9eBfI%2FbtrHAw4qi9e%2FNiWVsgtsJsgbXyqY2UMHck%2Fimg.png"><br/>

b는 find() 메소드고 c는 filter() 메소드다.

변수 b는 하나의 아이템 8만 갖고 있는 반면, 변수 c는 반환 조건에 해당하는 모든 아이템들을 묶어 배열로 만들어 갖고 있다.<br/><br/><br/><br/>

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcdKD5N%2FbtrHzpdMmm3%2FjCK5UMBcVgx8XRkufKKSZK%2Fimg.png"><br/>

만약 어떤 아이템도 콜백함수 조건에 해당하지 않으면 undefined가 뜬다.
<br/><br/><br/><br/>

## findlast()

<img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdhyCYJ%2FbtrHzpdQwkw%2F5LHEssfMaaVjHMg7E4OEjk%2Fimg.png"><br/>

findlast() 메소드는 find()와 비슷한 결이지만 배열데이터를 돌 때 0부터 도는 게 아니라 last인 배열의 끝에서부터 돈다.

위에서 b의 값이 5가 나오는 이유는 배열의 뒤쪽부터 3보다 크고 40보다 작은 아이템을 찾았기 때문이다.

만약 위에서  findlast() 가 아니라 find() 를 했다면 4가 나온다.<br/><br/><br/><br/>

## findIndex()

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbskx1g%2FbtrHCnM6OJU%2FJhmfUmaCUnTVNLKFArYDf1%2Fimg.png"><br/>

findIndex() 는 말 그대로 콜백함수 조건에 해당하는 아이템을 찾아, 그 아이템의 index 번호를 반환해주는 메소드다.

findIndex() 메소드 역시 find() 메소드처럼 조건에 해당하는 첫번째 아이템만 찾는다.<br/><br/><br/><br/>

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbHWaTU%2FbtrHxVD1DMB%2FGheb63lTBWxYFPCtX0u31k%2Fimg.png"><br/>

3보다 큰 숫자의 index를 찾으라고 했더니 3이 나왔다.

3보다 큰 숫자는 number 배열에서 4에 해당하고, 4 의 index는 3이기 때문에 console.log(b) 를 했을 때 값이 3이 나온다.
<br/><br/><br/><br/>

## includes()
 
<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbuw6bp%2FbtrHwkD6TXp%2Ftq0ponOjH1OLGmkvpkJJlK%2Fimg.png"><br/>

includes() 메소드는 인수에 들어온 데이터 타입이 배열 데이터에 포함되어 있는 지 확인하고, 만약에 포함되어 있으면 true를, 포함되어 있지 않으면 false를 반환한다.
<br/><br/><br/><br/>

## push()

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcx1b3L%2FbtrHCZd2QEH%2FxvPTKhkPeBER0k6uHtiHE1%2Fimg.png"><br/>

push() 메소드는 배열데이터에 하나 이상의 아이템을 배열 끝에 추가해준다. 그리고 새롭게 추가된 배열 데이터의 새로운 length 값을 반환한다.

number는 1부터 6까지 원래의 number.length는 6이었는데, push() 로 77을 배열 끝에 추가했더니 length가 7이 되었다.

number를 확인해보니 push() 할 때 넣어줬던 77이 배열의 맨 끝에 추가되어 있다.

push() 는 추가한 대로 새로운 배열을 만들지 않고 완전히 기존의 배열을 바꿔버린다.(참조형 데이터의 복사 후 재할당으로 같은 주소 영역을 지나게 되므로.)
<br/><br/><br/><br/>

문제!<br/>
<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbt7qJA%2FbtrHDji4yeq%2F3kwVWUcuPeK5u18pp3EEf1%2Fimg.png"><br/><br/>

Q 1 :  number2                       값은?<br/>
Q 2 :  number === number2            true? false?

<details>
<summary>해답</summary>
<div markdown="1">

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZXtb3%2FbtrHCx9WIo6%2FkVz6SX0kq8wjVNP9ZEvzkK%2Fimg.png"><br/><br/>
Q 1 의 답은 8.<br/>
push() 는 88과 99가 추가된 새로운 배열을 반환하는 게 아니라 새로워진 number의 length를 반환하기 때문이다.<br/><br/>

Q 2 의 답은 false.<br/>
[1,2,3,4,5,6,88,99] 는 8과 다르다.

</div>
</details>
<br/><br/>

메소드를 사용하고 배열 또는 객체 데이터가 바뀌냐 안 바뀌냐 다르니까

그런 점을 유의해서 사용해야 한다.


<br/>
2022.07.18<br/>
메소드는 쉬워 보여도 깊게 공부하면 좀 더 복잡하고 어려운 것 같다. 어렵다. 어려워
많이 보고 익히는 수밖에 없다.
