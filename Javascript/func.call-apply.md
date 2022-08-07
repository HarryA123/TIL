# call/ apply

객체에는 배열 메소드를 직접 적용할 수 없다. 하지만 유사 배열 객체의 경우에는 call, apply 메소드를 이용할 수 있다.

<br/><br/>

## 유사 배열 객체란?

키가 0 또는 양의 정수인 프로퍼티가 존재하고 length 프로퍼티 값이 0 또는 양의 정수인 객체를 의미한다.

꼭 index 순서는 0번부터 시작해야 하며, length를 반드시 포함하고 있어야 한다. 이 조건이 만족하지 않으면 유사배열객체라고 인식하지 못하거나 에러가 발생한다.
<br/><br/>


<img style="width:150px" src="https://blog.kakaocdn.net/dn/b34pwS/btrI4U249do/PXjzFTRr3bKldzCnkhskbK/img.png">

<img style="width:350px" src="https://blog.kakaocdn.net/dn/bmXfhF/btrI2xgu5do/7TlJAEBmcb2wMpw4PhFM11/img.png">

ES5까지는 Array.prototype.slice.call(arr,0) 를 사용하였지만,

ES6부터는 Array.from(arr) 를 사용하여 유사배열객체나 반복 가능한 객체를 얕게 복사해 새로운 array를 만든다.
<br/><br/><br/>

```js
let obj ={
    0:'a',
    1:'b',
    2:'c',
    length: 3    
};

let arr = Array.prototype.slice.call(obj);
console.log(arr);

// ['a','b', 'c']
```
slice 메소드를 적용해 객체를 배열로 전환했다.

slice는 시작 인덱스 값과 마지막 인덱스값을 받아 시작 인덱스부터 마지막 인덱스 앞부분까지를 배열로 추출합니다.

하지만 매개변수를 아무것도 받지 않았을 때는 원본 배열의 얕은 복사본을 반환합니다.

<br/><br/>

<img style="width:250px" src="https://blog.kakaocdn.net/dn/bMgQsj/btrIXV3JdXE/2TDc6cKNkXMRPucikMujX1/img.png">

slice에서는 빈 배열을 만들었고(유사배열객체를 배열로 변환) call 메소드가 obj 객체 인자를 받아 유사배열객체 obj 의 얕은 복사를 수행합니다. 이때, slice 메소드가 배열 메소드이기 때문에 복사본이 배열로 반환되었다.

call , apply 를 이용한 형변환은 본래의 메소드 의도와는 동떨어진 활용법이므로 Array.from 메소드를 사용하자.

<br/><br/>

# Array.from()
유사배열객체나 반복 가능한 객체를 얕게 복사해 새로운 array를 만든다.

```js
let obj ={
    0:'a',
    1:'b',
    2:'c',
    length: 3    
};

Array.from(obj);

// ['a','b','c']
```
Array.from 메소드를 사용하면 slice.call() 할 것 없이 간단하게 배열로 만들 수 있다.

<br/><br/>

배열에서 최대/최솟값을 구해야 할 경우 apply를 사용하면 간단하게 구현할 수 있다.


```js
let numbers = [2,45,7,35,866];
let max = Math.max.apply(null, numbers);
let min = Math.min.apply(null, numbers);
console.log(max, min);

// 866 2
```
apply는 첫 번째 인자로 null을 받고 두 번째 인자를 배열로 받는다.
numbers 배열에 대해 최대값을 구했고 -> 866
numbers 배열에 대해 최솟값을 구했다. -> 2
<br/><br/><br/>

위 코드는 apply를 적용하지 않고 펼치기 연산자로 더 간단하게 쓸 수 있다.
```js
let numbers = [2,45,7,35,866];
let max = Math.max(...numbers);
let min = Math.min(...numbers);
console.log(max, min);

// 866 2
```

<br/><br/>

**[문제1]** 
```
[  a  ]가 0 또는 양의 정수인 프로퍼티가 존재하고
[   b   ] 프로퍼티 값이 0 또는 양의 정수인 객체를 의미한다.
```
<details>
<summary></summary>
<div markdown="1">       
a = 키 , b = length
<br/>
</div>
</details>
<br/><br/>

**[문제2]** 

아래 코드의 결과는 어떻게 나올까?
```
Array.from('Apple');
```
<details>
<summary></summary>
<div markdown="1">       
['a', 'p', 'p', 'l', 'e']
<br/>
</div>
</details>
<br/><br/>


**[문제3]** 

어떤 함수를 호출해야 'John Doe,seoul,korea' 가 나올까? (apply() 와 call() 을 사용해보세요.)

```
const person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}

const person1 = {
  firstName:"John",
  lastName: "Doe"
  
//'John Doe,seoul,korea'
```
<details>
<summary></summary>
<div markdown="1">       
person.fullName.apply(person1, ['seoul', 'korea'])
person.fullName.call(person1, 'seoul', 'korea')
<br/>
</div>
</details>
<br/><br/>

**[문제4]** 

각 어떤 결과를 가져올까?

```
1. Math.max.apply(null, [1,2,3]);
2. Math.max.apply(Math, [1,2,3]);
3. Math.max.apply(" ", [1,2,3]);
4. Math.max.apply(0, [1,2,3]);
```

<details>
<summary></summary>
<div markdown="1">       
3, 3, 3, 3
<br/>
</div>
</details>
<br/><br/>


