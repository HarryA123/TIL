# Loop 반복문
js를 공부하면 반복문은 꼭 나온다.

반복문의 형태는 여러 가지인데 그중 for, forEach, for of, for in, do while, while을 배워보자.

들어가기 전에 알아두어야 하는 것은 for in 같은 경우 예외적으로 객체에서 쓰이는 반복문이다.  
그 외 for, forEach, for of, do while, while은 배열에서 쓰이는 반복문이라는 것을 알아두자.

```html
<body>
    <h1>for</h1>
    <ul id="for"></ul>
</body>
```

```js
const animals = ['dog','cat','camel','rabbit']
const myDog = {
    name: 'miso',
    age: 10,
    favorite: 'sweet potato',
    color: 'brown'
}
```

html의 ul element 안에 li를 만들어서 각각의 li 태그에 배열의 아이템들이 모두 들어가도록 만들어보자.  
그래서 우선 animals 라는 배열과 myDog라는 객체를 만들었다.  
<br/><br/><br/><br/>  
  
  
  

## 1\. for문

```html
<body>
    <h1>for</h1>
    <ul id="for"></ul>
</body>
```

```js
for( let i = 0 ; i < animals.length; i++){
  document.querySelector('#for').innerHTML += `<li>${animals[i]}</li>`
}
```

querySelector로 ul을 잡아준 뒤 ul이라는 html element 안에 list 태그를 걸어 그 안에 animals 배열에서 아이템을 꺼냈다.  
여기서 주의할 점은 innerHTML 오른쪽에 있는 할당 연산자다. 만약 = 만 쓰면 for문이 계속 반복되다가 마지막에 오는 아이템 rabbit만 뜨게 된다. 모든 아이템들을 하나씩 계속 추가하고 싶다면 += 덧셈 할당을 해야 한다.

<img style="width :100px" src ="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FH2z0i%2FbtrHZeOIkVJ%2FatQuSepbcWZjVqxCcklsa0%2Fimg.png" >

<br/><br/><br/><br/>
  

## 2\. forEach문

```html
<body>
    <h1>forEach</h1>
    <ul id="forEach"></ul>
</body>
```

```js
animals.forEach(function(item){
  document.querySelector('#forEach').innerHTML += `<li>${item}</li>`
})
```

forEach는 인자로 함수를 받는다. 반복될 때마다 콜백 함수가 호출된다.

<img style="width :100px" src ="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZDgWV%2FbtrHVf27UD5%2FRumGuWLeRojvryv8IwupC0%2Fimg.png" >
<br/><br/><br/><br/>

## 3\. for of문

```html
<body>
    <h1>forOf</h1>
    <ul id="forOf"></ul>
</body>
```

```js
for( item of animals){
  document.querySelector('#forOf').innerHTML += `<li>${item}</li>`
}
```

animals라는 배열의 item들을 반복한다는 의미로, 반복 가능한 대상을 animals 자리에 둔다(iterable)

forOf는 ES6에서 새롭게 생긴 반복문이다.  
Array에 대한 반복, string에 대한 반복, TypedArray에 대한 반복, map에 대한 반복, Set에 대한 반복 등을 할 수 있다.

<img style="width :100px" src ="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCKAn6%2FbtrHY7pgqdg%2FRISY9okxkKU5agmhu0wTk1%2Fimg.png" >

<br/><br/><br/><br/>

## 4\. for in문

```js
// SYNTAX;
for (variable in object) { }
```

```js
<body>
    <h1>forIn</h1>
    <ul id="forIn"></ul>
</body>
```

```js
for( item in myDog){
  document.querySelector('#forIn').innerHTML += `<li>${item} : ${myDog[item]}</li>`
}
```

for in 반복문은 객체의 속성을 반복하여 작업을 수행한다. 위의 예제의 경우 myDog라는 객체의 속성인 name, age, favorite, color를 반복하였고, 마찬가지로 myDog \[item\]으로 그 속성의 값도 가져올 수 있다

for in은 객체의 반복을 위해 만들어졌기 때문에 배열의 반복을 위해 사용하는 것은 추천하지 않는다. 그런 경우에는 위에서 알아본 forEach와 for of를 사용하면 된다.  
for in은 객체의 속성을 확인하는 것이 쉽기 때문에 실질적으로 '디버깅' 하는 데에 쓰일 수 있다. key-value를 가진 객체 데이터의 경우 특정 값을 가진 key가 있나 확인할 때 for in을 사용할 수 있다.

<img style="width :150px" src ="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbEQaNP%2FbtrHVfPy6GF%2FxPBPQ6asNfLe1KePFKhbgK%2Fimg.png" >
<br/><br/><br/><br/>  

## 5\. do while문

```js
// SYNTAX
초기문
do{행동 문장; 증감문}
while(조건문)
```

```js
<body>
    <h1>do while</h1>
    <ul id="doWhile"></ul>
</body>
```

```js
let y = 0
do{
    document.querySelector('#doWhile').innerHTML += `<li>${animals[y]}</li>`
    y++;
}
while( y < animals.length)
```

while은 for문이랑 거의 흡사하다. do를 쓰기 전에 초기문을 먼저 작성한다. 그리고 do에서 행동 문장을 쓴 뒤 그다음 줄에 증감문을 붙여야 한다.

do while은 조건문이 거짓으로 판별될 때까지 반복된다.

그리고 do while은 조건문이 시작부터 false라고 해도 적어도 한 번은 실행된다는 특성이 있다.

<img style="width :300px" src ="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBnP8n%2FbtrHZRzdiGt%2Fm5HKzL5futg3WNiqNqh8pK%2Fimg.png" >

위 예제의 조건문을 보자 y < 0인데 처음 y는 0으로 시작하기 때문에 위의 조건문은 false다.

그럼에도 불구하고 저 코드를 실행시키면 do while 반복문이 실행되면서 첫 번째 아이템인 apple을 반환한다.

이렇게 do while 반복문은 조건문이 false라도 한 번은 출력한다는 것을 알 수 있다.  
  
<br/><br/><br/><br/>
## 6\. while문

```js
// SYNTAX
초기문
while( 조건문 ){
행동 문장; 증감문
}
```

```js
let m = 0
while(m < animals.length){
  document.querySelector('#while').innerHTML += `<li>${animals[m]}</li>`;
  m++;
}
```

while은 조건문이 참이라면 거짓일 때까지 반복한다.  
do while과는 달리 처음부터 조건문이 false라면 단 하나의 코드도 출력되지 않고 그대로 종료되고 다음 코드를 실행한다.  
while의 조건문을 항상 true가 되게 설정하면 영원히 실행되기 때문에 주의해야 한다.

<img style="width :300px" src ="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQjDPv%2FbtrHWFtUyt9%2FAsSs35SiNLtqe4HKp8Czc1%2Fimg.png" >

위의 예제를 보면 처음부터 false일 때 undefined가 나오는 걸 볼 수 있다.

하지만 위 예제가 do while문이었다면 false임에도 적어도 한 번은 출력되기 때문에 apple이 한 번 출력된다.  
<br/><br/><br/><br/>

## 7\. break 문

break문은 반복문, switch, label 문을 '종료'하고 그다음 문으로 넘어가기 위해 사용된다.

```js
// 예제 1번

for (let i = 0; i < 10; i++) {
    if (i == 3) {        // i 가 3이 되면
        break;            // for 문 종료
    }
    console.log(i);        // 0,1,2
}
```

```js
// 예제 2번

for (let i = 0; i < 10; i++) {
    if (i < 3) {                // i가 3보다 작을 때까지
      console.log(i);            // 0, 1, 2
    }
}
```

예제 1번과 2번은 똑같이 0,1,2 라는 값이 나온다.

둘의 차이점이라고 하면, 예제 1번은 4번을 순회하고, 예제 2번은 10번을 순회한다.  
순회하는 횟수가 많아지면 연산도 늘어나기 때문에 순회 횟수는 성능에 큰 영향을 미친다.

break를 사용하는 이점이 있다.
<br/><br/><br/><br/>
  

## 8\. Continue 문

```js
 for (let i = 0; i < 10; i++) {
    if (i === 3) {                     // i 가 3 과 같을 경우
        continue;                     // 다시 순회표현식으로 이동
    }
    console.log(i); // 0,1,2,4,5,6,7,8,9
}
```

위 콘솔 결과를 보면 3이 없다.  
이는 if조건문에서 3일 때 continue를 실행했기 때문이다. 이처럼 continue가 실행되면 그에 해당하는 행동 문장은 실행되지 않고 바로 종료되어버리기 때문에 다음 증감문을 받아 조건문을 실행한다.

즉, continue를 만나면 코드를 실행시키지 않고 바로 종료되고, 다음 증감문을 받아 조건문을 실행한다.

break는 모든 label에서 사용할 수 있는 반면 continue는 반복label에만 사용할 수 있다.
<br/><br/><br/><br/>

## 9\. label 문

label문은 break와 continue와 함께 사용할 수 있다.  
label은 프로그램 내 특정한 영역을 식별할 수 있도록 해주는 식별자라고도 할 수 있다.  
이때, strick mode 코드에서는 let을 label의 식별자로 사용했을 때 SYNTAXERROR를 발생시키기 때문에 사용하지 않아야 한다.  
strick mode란 ES6에서 기본적으로 설정되어 있기 때문에 'use strict'를 쓰지 않아도 자동 실행된다.

```js
// SYNTAX
label:
```

break와 continue와 함께 사용할 때는 아래처럼 작성한다.

```js
break labelname1
continue labelname2
```

label은 보통 switch 문에서 쓰이고 있다.
<br/>

2022.07.22
