# Part7 - 연산자

## (7) 연산자

피연산자가 값이라는 명사의 역할을 한다면, 연산자는 피연산자를 연산하여 새로운 값을 만든다는 동사의 역할을 한다.
<br/><br/><br/>

**산술연산자**

수학적 계산을 수행해 새로운 숫자 값을 만든다. 연산이 불가능하면 NaN(not a number) 를 반환한다. 피연산자의 개수가 2개면 이항 산술 연산자, 1개면 단항 산술 연산자라고 부른다. 이항 산술 연산자는 피연산자 값이 바뀌는 경우는 없고 언제나 새로운 값을 만들 뿐이다.


단항 산술 연산자는 한 개의 피연산자를 산술 연산하여 숫자 값을 만든다. 단항 산술 연산자는 증가++/감소-- 연산자는 피연산자의 값을 변경하는 암묵적 할당이 이뤄진다.

```js
let x = 5, result;
// 선할당 후증가
result= x++;
console.log(result, x) // 5 6
// result에 x라는 값을 먼저 할당한 뒤 후증가연산(x++)을 함 

// 선증가 후할당
result = ++x;
console.log(result, x) // 7 7
// x를 먼저 선증감연산(++x)한 뒤 result에 그 결과값을 할당함
```
++/--는 증가 또는 증감 연산이 가능하지만 +/-는 부수효과가 없다.(-는 음수를 양수로, 양수를 음수로 반전하지만 +는 그런 반환을 하지 않는다.)

<br/><br/>

```js
console.log(+'1') // 1

console.log(+true) // 1
console.log(-true) // -1

console.log(+false) // 0

console.log(+'hello') // NaN
```
+/- 단항 연산자는 숫자타입으로 변환하여 반환한다. - 단항 연산자를 사용하면 숫자타입으로 변환하여 음수로 반환한다. 숫자타입으로 변환되지 않는 string의 경우 NaN를 반환한다.

<br/><br/>

**문자열 연결 연산자**

피연산자들 중 하나 이상이 문자열이면 +연산자는 문자열 연결 연산자로 동작한다.
```js
'1' + 1 = 11
1 + true = 2
1 + false = 1
1 + null = 1 // null 은 0으로 타입 변환된다.
+undefined = NaN
1 + undefined = NaN
```
**암묵적 타입 변환**

이렇듯 기존의 타입을 다른 타입으로 강제 변환하는 것을 **암묵적 타입 변환**, **타입 강제 변환**이라고 한다.

<br/><br/>

**할당 연산자**

할당연산자는 좌항의 변수에 값을 할당하므로 변수 값이 변하는 부수 효과가 있다.
```js
let x = 10;

console.log(x += 5) // x = x + 5,   15
console.log(x -= 5) // x = x - 5,   10
console.log(x *= 5) // x = x * 5,   50
console.log(x /= 5) // x = x / 5,   10
console.log(x %= 5) // x = x % 5,   0

let str = 'hello'
console.log(str += 'world') // str = str + 'world', 'hello world'
```

할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가된다.

<br/><br/>

**비교 연산자**

비교연산자는 주로 if문이나 for문과 같은 제어문의 조건식에서 주로 사용한다.
<br/><br/>

**동등 비교 연산자(==)**

좌항과 우항의 피연산자를 비교할 때 먼저 암묵적 타입 변환을 통해 타입을 일치시킨 후 같은 값인지 비교한다. 타입이 달라도 암묵적 타입변환 후 같은 값일 수 있다면 true를 반환한다. 하지만 동등 비교 연산자는 예측하기 어려운 결과를 만들기 때문에 되도록이면 일치 비교 연산자(===)를 사용한다.

<br/><br/>

**일치 비교 연산자(===)**

```js
5 === 5 // true (5와 5는 타입까지 일치한다.)
5 === '5' // false (5와 '5'는 타입까지 일치하지 않다.)
5 !== 1 // true (5와 1은 타입까지 일치하지 않다.)
NaN === NaN // false (NaN는 자신과 일치하지 않다.)
```
좌항과 우항의 피연산자가 타입도 같고 값도 같은 경우에 한해 true를 반환한다.

<br/>


```js
Number.isNaN('5') // true('5'는 넘버가 아니다-> 맞음(true))
Number.isNaN(5) // false(5는 넘버가 아니다-> 틀림(false))
Number.isNaN(1+undefined) // true(1+undefined는 NaN를 반환한다. Number.isNaN(NaN) -> 맞음(true)) 
```
NaN는 자신과 일치하지 않는 유일한 값이다. 따라서 숫자가 NaN 인지 조사하려면 빌트인 함수 Number.isNaN() 함수를 사용한다. 이 함수는 지정 값이 NaN 인지 확인하고 그 결과를 Boolean으로 반환한다.

<br/>

```js
0 === -0 // true
0 == -0 // true
```
양의 0, 음의 0은 같다.

<br/><br/>

**삼항 연산자**

```js
// Syntax
🟠조건식 ? 🟡조건식이 true일 때 반환할 값 : 🔵조건식이 false일 때 반환할 값

-> 🟠 ? 🟡 : 🔵
```
```js
let x = 2;
let result = x % 2 ? '홀수' : '짝수';
console.log(result) // '짝수'
```
위 처럼 조건식의 평과 결과가 boolean이 아니라면 boolean으로 암묵적 타입 변환된다. x % 2는 0이 남기 때문에 (0 = false) ':' 뒤에 있는 '짝수' 가 반환된다.

첫번째 피연산자는 조건식이므로 삼항 연산자 표현식은 조건문이다. 이는 If...else문과 유사하게 처리할 수 있다.
<br/><br/>

**삼항 연산자와 If...else문의 차이**

삼항 연산자 표현식은 값으로 평가할 수 있는 표현식인 문이다. 따라서 삼항 연산자 표현식은 값처럼 다른 표현식의 일부가 될 수 있어 매우 유용하다.

삼항 연산자 표현식은 값처럼 사용할 수 있어 유용하고, if...else문은 조건에 따라 수행해야 할 문이 여러 개일 때 가독성 면에서 좋다.

<삼항 연산자는 값처럼 사용 가능, if...else 불가능>

<br/><br/>

**논리 연산자**

우항과 좌항의 피연산자를 논리 연산한다.

```js
// 논리합(||) 연산자
true || true // true
true || false // true
false || true // true
false || false // false

// 논리곱(&&) 연산자
true && true // true
true && false // false
false && true // false
false && false // false

// 논리 부정(!) 연산자
!true // false
!false //true
!0 // true
!'hello' // false
```
위의 논리합, 논리곱 연산 평과 결과가 true 또는 false가 나오는 지 그 원리를 잘 알아두자. 논리합 연산자는 끝까지 평가를 안 하고 첫 평가에서 true가 나오면 곧바로 그 피연산자 값을 반환한다. 하지만 논리곱 연산자는 앞에서 계속 true가 나와도 끝까지 평과를 거치며, false가 나오면 곧바로 거기서 멈추고 피연산자 값을 반환한다. 아래를 보면 더 이해하기 쉽다.

<br/>

```js
'cat' || 'dog' // 'cat'
'cat' && 'dog' // 'dog'
'cat' && 'dog' && 32 && 'undefine' && 0 && null
// 0 (0과 null은 false다 논리곱 연산자는 cat부터 true인지 평가를 하다가 false로 평가되는 피연산자를 만나면 그 순간부터 평가를 멈추고 그 피연산자의 값을 반환한다. null 또한 false지만 0이 먼저 평가됐기 때문에 0을 반환한다.)
```
논리합, 논리곱 연산자의 평가결과는 불리언 값이 아닐 수도 있다. 논리합 또는 논리곱 연산자 표현식은 언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.

<br/><br/><br/>

## 문제를 풀어봅시다.

**[문제1]** 
```js
let x = 10, result;

// 1번
result = ++x;
console.log(result, x)

// 2번
result= x++;
console.log(result, x)
result = x = x + 1
```
<details>
<summary></summary>
<div markdown="1">       
1번: 11 11 , 2번: 11 12
<br/>
</div>
</details>
<br/><br/>

**[문제2]** 
```
+/- 단항 연산자는 [  a  ]타입으로 변환하여 반환한다.
- 단항 연산자를 사용하면 [  a  ]타입으로 변환하여 [  b  ]로 반환한다. 
[  a  ]타입으로 변환되지 않는 string의 경우 [  c  ]를 반환한다.
```
<details>
<summary></summary>
<div markdown="1">       
a : 숫자, b : 음수, c : NaN
<br/>
</div>
</details>
<br/><br/>

**[문제3]**
```
기존의 타입을 다른 타입으로 강제 변환하는 것을 [  ?  ]이라고 한다.
```
<details>
<summary></summary>
<div markdown="1">       
암묵적 타입 변환
<br/>
</div>
</details>
<br/><br/>

**[문제4]**
```
NaN === NaN 의 평가 결과는 [  a  ] 다.

숫자가 NaN 인지 조사하려면 빌트인 함수 [  b  ] 함수를 사용한다. 이 함수는 지정 값이 NaN 인지 확인하고 그 결과를 Boolean으로 반환한다.
```
<details>
<summary></summary>
<div markdown="1">       
a: false, b: Number.isNaN()
<br/>
</div>
</details>
<br/><br/>

**[문제5]**
```
삼항 연산자 표현식은 ____a____이다. 따라서 삼항 연산자 표현식은 값처럼 다른 표현식의 일부가 될 수 있어 매우 유용하다.
그리고 If...else문은 조건에 따라 수행해야 할 문이 여러 개일 때 가독성 면에서 좋다.

<삼항 연산자는 값처럼 사용 [ b  가능/ 불가능  ], if...else는 [ c  가능/ 불가능  ]>
```
<details>
<summary></summary>
<div markdown="1">       
a : 값으로 평가할 수 있는 표현식인 문, b :가능, c : 불가능
<br/>
</div>
</details>
<br/><br/>

**[문제6]**

아래의 평가 결과는?
```js
// 1번
0 || null && 1

// 2번
'hello world' && 12321.1 && 10+'1'
```
<details>
<summary></summary>
<div markdown="1">       
1번 : null, 2번 : 101
<br/>
</div>
</details>
<br/><br/>


<br/>
2022.07.28

