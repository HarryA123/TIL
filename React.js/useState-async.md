# useState는 비동기다.
set 함수를 연달아 사용했을 때 왜 의도대로 작동이 안 되는지, 근데 왜 이걸 함수 형태로 쓰면 의도대로 작동되는 지 모르겠어서 useState 비동기에 대해 알아봤다.

<br/><br/>

```js
function App(){
  const [value, setValue] = useState(0)
  const onclick = function(){
    setValue(value+1);
    setValue(value+1.5);
    setValue(value+2.5);
  }
  return(
    <div>
      <h1>{value}</h1>
      <button onClick={onclick}>click</button>
    </div>
  )
}
```
위 코드를 실행시키고 click 버튼을 한 번 클릭하면 어떤 결과가 나올까? 분명 setValue를 연달아 세 번 실행했으니까 5?

<br/><br/>

위의 결과는 5가 아니라 2가 나온다.
```js
2 [click] - O              // 5 [click] - X
```
가장 맨 뒤의 setValue(value+2) 만 실행시킨 결과다. 이런 결과가 나오는 이유는 useState가 비동기로 작동하기 때문이다. 한꺼번에 여러 요청을 처리하기 때문에 첫 번째 setValue(value+1), setValue(value+1.5), setValue(value+2.5); 가 동시에 진행된다. 그러다 결국 제일 마지막의 setValue(value+2.5)만 실행이 된 것.

이렇게 비동기적으로 동작하는 이유는 useState를 연속 호출하면 batch(react가 더 나은 성능을 위해 여러개의 state 업데이트를 하나의 리렌더링으로 **묶는 것**을 의미한다.) 처리하여 한 번에 렌더링하도록 되어있기 때문이다.

<h4 style='color: yellow'>아무리 setValue가 연속적으로 여러번 사용되어도 batch에 의해 하나로 묶여 렌더링되는 것이다.<h3>

<br/><br/>

# 비동기 해결 방법 - setState의 함수 인자

```js
function App(){
  const [value, setValue] = useState(0)
  const onclick = function(){

/* 비동기 실행의 예
    setValue(value+1);
    setValue(value+1.5);
    setValue(value+2.5);
*/
    setValue((prev)=> prev + 1 );
    setValue((prev)=> prev + 1.5 );
    setValue((prev)=> prev + 2.5 );
  }
  return(
    <div>
      <h1>{value}</h1>
      <button onClick={onclick}>click</button>
    </div>
  )
}
```
setState가 인자로 함수를 받도록 만들면 useState를 동기로 사용할 수 있다. setState의 함수의 반환값으로 설정해야 한다. 위처럼 setState가 인자로 함수를 받아 return을 하는 식으로 setState를 설정하면 내가 의도한 대로 버튼을 누를 때마다 5씩 커진다.

```js
5 [click]
```

<br/><br/>
## ⁉ 매개변수 prev는 뭐지⁉

그럼, setState는 어떤 인자를 받는 걸까? 위의 코드를 아래와 같이 바꿔봤다. (useState 초기값에 있었던 0을 'so'라는 string으로 바꿨다.)

```js
function App(){
  const [value, setValue] = useState('so')
  const onclick = function(){
    setValue((prev)=> prev + 1 );
    setValue((prev)=> prev + 1.5 );
    setValue((prev)=> prev + 2.5 );
  }
  return(
    <div>
      <h1>{value}</h1>
      <button onClick={onclick}>click</button>
    </div>
  )
}
```
위 코드의 결과, 버튼을 누르면 어떤 값이 브라우저에 출력될까?

<br/>

```js
so11.52.5
```
위와 같은 결과가 나온다. 이 결과를 보니까 이제 useState가 어떤 인자를 매개변수로 받는 지 알겠다. 바로, useState에서 설정해두었던 초기값'so' 를 인자로 받는 것이다. setValue는 so에 string 결합 방식으로 계속 덧붙여진다.

-> 최초값(이전값)인 so,   
-> 그 값에 더해진 1 (암묵적 형변환으로 string으로 계산됨),   
-> 그 값에 더해진 1.5   
-> 그 값에 더해진 2.5

<br/><br/>
## useState의 초기값에 더해지는 것만은 아니다.

```js
function App(){
  const [value, setValue] = useState(9)
  const onchange = function(e){
    setValue(e.target.value)
    setValue((prev)=>+prev+1)
    setValue((prev)=>+prev+2)
  }
  return(
    <div>
      <input
      value={value}
      onChange={onchange}>
      </input>
    </div>
  )
}
```
근데 꼭 useState 초기값에 더해지는 것은 아니다. 예제를 좀 바꿔서 클릭할 때마다 결과가 보여지는 게 아닌, input에 숫자를 입력할 때마다 결과가 어떻게 바뀌는 지 코드를 바꿔봤다.

위의 코드에서 내가 input 창에 1을 누르면 어떤 결과가 나올까? prev 매개변수가 useState의 초기값인 9를 받아 9에다가 1을 더해 10이 되었다가 그 값에 2를 더한 12가 될까?
그리고 순차적으로 12345를 눌렀을 때는 어떤 결과가 나올까?

<br/>

```js
94   /*1만 눌렀을 때*/         945678   /*12345 눌렀을 때*/
```
초기값인 9에 1과 2가 더해지는 것이 아니라 내가 1을 눌렀을 때 그 1이 9를 대체하고 최신의 값이 된다. 그래서 밑의 setValue는 내가 방금 전에 누른 1에 1을 더하고 그 값에 2를 더해서 4가 나온 것이다.
(내가 제대로 이해한 게 맞는 지 모르겠지만 일단 지금 이해하기로는 이렇다.)

<h4 style='color:yellowgreen'>setState는 함수를 인자로 받을 때 동기로 작동하는 구나!
매개변수가 받아온 인자는 방금전(current)의 값이구나!?</h4>

<br/><br/>


Ref: [velog](https://velog.io/@alstnsrl98/useState는-동기-비동기-동기적-처리)

<br/>
2022.08.04
