# 생성자 함수(constructor function)

우리가 만약에 다양한 과일의 정보가 담긴 웹사이트를 만든다고 해보자.

과일의 이름, 원산지, 색, 맛, 무게 등을 예쁘게 정리해 놓은 웹사이트를 만들기 위해 일단 과일별로 정리를 해야 한다.

이때 우리는 object를 사용할 수 있다.

banana라는 object는 아래처럼 만들 수 있겠다.

```js
const banana = {
  name : 'banana',
  color: 'yellow',
  home: 'philippine',
  taste: 'sweet',
  weight: '100g',
  bugs: 'a lot',
  peel: 'yes',
}
console.log(banana);
// {name: 'banana', color: 'yellow', home: 'philippine', taste: 'sweet', weight: '100g'}

```
근데 과일의 종류가 1000개일 때, 이렇게 긴 코드를 똑같이 1000개를 카피해서 쓰면 용량 문제도 있고 해당하는 name, color, home 등 일일이 바꿔야하는 수고로움도 있다.

그래서 위의 방법을 *1000 하는 것은 비효율적이다. 다른 방법이 없을까?<br/><br/><br/><br/>



```js
function Fruits(){}

const one = new Fruits();
one.name = 'banana';
one.color = 'yellow';
one.home = 'philippine';

console.log(one)
// Fruits {name: 'banana', color: 'yellow', home: 'philippine'}
```
함수를 만들어서 그 함수 안에 각각의 항목들을 넣는 방법도 있다. 근데 이것도 첫 번째 방법과 다를 게 없다. 이 방법 또한 *1000 번을 해야 실행될 수 있어서 비효율적이다.

근데 여기서 new는 무슨 역할을 하는걸까?<br/><br/>

## new?
Fruits()라는 함수 앞에 new라는 keyword를 붙이게 되면 Fruits()는 더이상 함수가 아니라 **'객체 생성자'** 가 된다.
new로 인해서 Fruits는 비어있는 객체를 만들어낸다.
new는 그 뒤에 오는 함수를 '객체 생성자'로 만든다. 

그래서 위의 코드를 해석해보자면, 함수 Fruits라는 이미 비어있는 상태다. 그 함수를 객체 생성자로 만들기 위해 new Fruits() 를 써줬고 그것을 one이라는 변수로 선언했다.
그 아래 코드들은 비어 있는 Fruits 안에 들어갈 내용들을 선언해서 집어 넣는 것.

그 결과로 console.log(one) 을 하면 써줬던 내용들이 객체로 잘 정리되어 출력된다.

**생성자는 첫 글자를 대문자로 표기한다.**<br/><br/><br/><br/>





```js
function Fruits(name, color, home){
  this.name = name;
  this.color = color;
  this.home = home;
}

const banana = new Fruits('banana', 'red', 'philippine')

console.log(banana);
// Fruits {name: 'banana', color: 'red', home: 'philippine'}
```
이 형태가 생성자 함수 모습이다.
생성자 함수는 객체를 뽑아내는 기계라고 생각하면 이해하기 쉽다. 저 Fruits 함수는 객체를 뽑아내는 기계다. 

banana라는 변수에 객체 생성자를 만들고 그 객체 생성자 안에 차례대로 인수를 넣으면 된다.




```js
function Fruits(name, color, home){
  this.name = name;
  this.color = color;
  this.home = home;
}

const banana = new Fruits('banana', 'yellow', 'philippine')
const apple = new Fruits('apple', 'red', 'japan')

console.log(banana);
console.log(apple);
// Fruits {name: 'banana', color: 'red', home: 'philippine'}
// Fruits {name: 'apple', color: 'red', home: 'japan'}
```

그럼 간단한 생성자 함수가 간단한 코드로 완성된다!
2022.07.12