# 문자형 변환(To String)

## String()
```js
a = 1234
String(a)

// '1234'
```
string(), 소괄호 안에 감쌌더니 1234라는 Number가 Sting으로 형변환 된다.<br/><br/>

## ''+ Number
```js
a = 123
""+ a

// '123'
```
<br/><br/>

##  b = `${}`
```js
a = 123
b = `${a}`
// '123'
```
<br/><br/><br/><br/>


# 숫자형 변환(To Number)

## b = +a (+ 단항 연산자 unary Operator)
```js
a = '123'
b = +a
// 123

a = 'apple'
b = +a
// NaN
```
피연산자를 숫자형으로 반환.

## b = -a (- 단항 연산자 unary Operator)
```js
a = '123'
b = -a
// -123

a = 'apple'
b = -a
// NaN
```
피연산자를 숫자형(음수)로 반환.

<br/><br/>

## b = Number(a)
```js
a = '123'
b = Number(a)
123
```
<br/><br/>

🍑그 외 숫자형 변환
|전달받은 값|Number형 변환 후|
|-----|----|
|undefined| NaN (not a number)|
|null|0|
|true / false|1 / 0|
|string '　'|0|
<br/><br/><br/><br/>

# 불리언형 변환(To Boolean)

## b = !!a
```js
a = 123
b = !!a
// true

a = 0
b = !!a
// false

a = null
b = !!a
// false
```
<br/><br/>

## b = !!a
```js
a = 123
b = Boolean(a)
// true
```
<br/><br/>

🍒그 외 불린형 변환
|전달받은 값|boolean형 변환 후|
|-|-|
|0, null, undefined, NaN, '　'| false|
|그 외 값| true|

<br/><br/>
[Ref](https://ko.javascript.info/type-conversions)

2022.7.11