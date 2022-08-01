# 제어문 (control flow statement)

제어문은 조건에 따라 코드 블록을 실행하거나 반복 실행할 때 사용한다. 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다. (forEach, map, filter, reduce)

<br/><br/>

**블록문**

블록문은 코드블록 또는 블록이라고 부르기도 한다. 일반적으로 제어문이나 함수를 정의할 때 사용한다. (문의 종료르 ㄹ의미하는 자체 종결성을 갖기 때문에 세미 콜론을 붙이지 않는다.)

<br/><br/>

**조건문**

주어진 조건식의 평과 결과에 따라 코드블록의 실행을 결정한다. 조건식은 불리언 값으로 평가될 수 있는 표현이다. (if...else, switch)

<br/><br/>

## If...else 문

참, 거짓에 따라 코드블록을 결정한다. true면 if문의 코드블록이 실행되고, false면 else문의 코드 블록이 실행된다.

만약 조건식이 불리언 값이 아닌 값으로 평가되면 암묵적 타입 변환으로 불리언 값으로 강제 변환된다.

만약 조건식을 추가하여 조건에 따라 실행될 코드를 늘리고 싶으면 else if 문을 사용하면 된다. else if 문은 여러번 사용 가능하다.

if...else문은 삼항 연산자로도 표현할 수 있다. 이 둘의 큰 차이점은 if...else문은 값처럼 쓸 수 없지만 삼항 연산자는 값으로 사용할 수 있다는 것이다.

```js
//if...else문

let a = 10;
let result

if(a > 4){
  result = '크다'
} else{
    result = '작다'
}

console.log(result)   //'크다'
```

```js
//상항 연산자

let a = 10;
let result = (a > 4) ? console.log('크다') : console.log('작다')

console.log(result)   //'크다'
```


<br/><br/>

## switch

주어진 표현식을 평가하여 그 값과 '일치'하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다. switch 문의 표현식과 일치하는 문이 없다면 실행 순서는 default문으로 이동한다.

switch문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다. 즉, 논리적 참, 거짓보다는 다양한 상황(case)에 따라 실행할 코드 블록을 결정할 때 사용한다.

<br/><br/>

```js
let yourNum = 2;
let ourNum

switch(yourNum){
case 1 : ourNum = 2020;
  break;
case 2 : ourNum = 2021;
  break;
case 3 : ourNum = 2022;
  break;
case 4 : ourNum = 2023;
  break;
case 5 : ourNum = 2024;
  break;
default: ourNum = 2050;
}
console.log(ourNum)   // 2021
```

**폴스루(fall through)**

문을 실행한 후 문을 탈출하지 않고 switch문이 끝날 때까지 이후의 모든 case문과 default 문을 실행하면 맨 마지막 case가 출력된다.


**break**

폴스루를 막기 위해서는 위의 예제와 같이 break문을 사용해야 한다. break 키워드로 구성된 break문은 코드 블록에서 탈출하는 역할을 한다. 일반적으로 default문에는 break를 생략한다. default문은 switch문의 맨 마지막에 위치하기 때문에 별도의 break문이 필요가 없다.

<br/><br/>

## 반복문

조건식이 참인 경우 코드 블록을 실행한다. 조건식이 거짓일 때까지 반복된다.
<br/><br/>

**for**

- 변수 선언문은 단 한 번만 실행된다. 
- 증감문으로 실행 흐름이 이동하는 것이 아니라 코드 블록으로 실행흐름이 이동한다. 
- 증감식 실행이 종료되면 다시 조건식이 실행된다. 변수 선언문이 실행되는 것이 아니라 조건식이 실행됨에 주의.

```js
for(let i = 0; i < 5; i++>){
  console.log(i)
}
```

변수 선언문, 조건식, 증감식은 모두 옵션이므로 반드시 사용할 필요는 없지만 어떤 식도 선언하지 않으면 무한루프 된다.

for문 내에 for문을 중첩해 사용할 수 있다. 이를 중첩 for문이라고 한다.

<br/><br/>

**While문**

조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료한다.
```js
let count = 0;
while(true){
  console.log(count);
  count++;
  if(count === 4) break;    // count가 4면 코드블록 탈출
}
// 0,1,2,3
```
<br/><br/>

**Break문**

레이블문, 반복문, switch문의 코드 블록을 탈출한다. 이 외에 break문을 사용하면 syntaxError가 난다.

반복문에서는 더 이상 진행하지 않아도 될 때 불필요한 반복을 회피할 수 있어 유용하다.

<br/><br/>

**Continue문**

반복문의 증감식으로 실행 흐름을 이동시킨다. break문처럼 반복문을 탈출하지 않는다.

<br/>

2022.08.01
