# 얕은 복사 (Shallow Copy)


<img style="width:350px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcqjG7R%2FbtrHCZsNBjw%2FjkBJ2KoTeskknzPpqeuG2k%2Fimg.png"><br/>

food라는 변수에다가 fruits 라는 변수를 복사했다.

그랬더니 food와 fruits가 완전히 같은 메모리를 바라보게 되어 food === fruits 의 값으로 true가 나왔다.

이렇게 되면 food 프로퍼티에 어떤 걸 추가해도 food와 fruits는 같아져서 의미가 없어진다.

그래서 얕은 복사로 food와 fruits를 완전히 별개의 것으로 만들고 싶을 때 그 방법으로 두가지를 쓸 수 있다.

하나는 위에서 사용한 것처럼

```js
object.assign({}, 소스)
```
object.assign()을 적용하는 방법이고 다른 하나는 아래처럼 전개 연산자{...}를 사용하는 방법이 있다.

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkMtTH%2FbtrHIdXKE0l%2FDmdg2YKQtCpEMiYYLltRz1%2Fimg.png"><br/><br/><br/><br/><br/>


# 깊은 복사 (Deep Copy)

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F97yEe%2FbtrHIHdfJZi%2FP0cN1dRQijzOVB1k5hrdI1%2Fimg.png"><br/>

- npm i lodash
terminal을 열어서 lodash를 설치한다.
그렇게 생긴 lodash 에서 깊은 복사를 해주는 cloneDeep()메소드를 가져오는 방법이 있다. 

```js
import _ from lodash
```
위에서 lodash를 _로 가져올 수 있는 것은 lodash의 export가 default로 되어있기 때문이다.

default export를 import 해서 가져오기를 할 때는 이름을 사용자 편의에 맞게 바꿀 수 있으며 {}중괄호로 감싸지 않아도 된다.

반면, default export가 아닌 그냥 export로 가져오기를 하면 {}중괄호 안에 해당 변수명을 명시하여 가져와야 한다.

통상적으로 lodash는 _ 로 가져온다. <br/>

2022.07.19

