# 타입 변환과 단축 평가

## -암묵적 타입 변환

## 문자열 타입으로 변환
## \+ ''

```
({}) + ''                  // "[object Object]"
Math + ''                  // "[object Math]"
[] + ''                    // ""
[10,20] + ''               // "10, 20"
(function(){}) + ''        // "function(){}"
Array + ''                 // "function Array(){[native code]}"
```

<br/><br/><br/>

## 숫자 타입으로 변환

```
+true             // 1
+false            // 0
+null             // 0
+undefined        // NaN
+{}               // NaN
+[]               // 0
+[10, 20]         // NaN
+''               // 0
+(function(){})   // NaN
```
빈 문자열, 빈 배열, null, false, true는 1로 변환되지만 객체와 빈 배열이 아닌 배열, undefined는 변환되지 않고 NaN이 된다.

<br/><br/><br/>

## 불리언 타입으로 변환

```
1. false
2. undefined
3. null
4. 0, -0
5. NaN
6. ''(빈 문자열)
```
위는 모두 거짓으로 평가되는 값이다.

<br/><br/><br/>

## -명시적 타입 변환

## 문자열 타입 변환
1. String 생성자 함수를 new 연산자 없이 호출하는 방법
2. Object.prototype.toString 메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법
```
String(Infinity)     //'Infinity'
String(NaN)          //'NaN'

(true).toString()    //'true'
(1).toString()       //'1'

false + ''           //'false'
```

<br/><br/><br/>

## 숫자 타입 변환
1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
3. \+ 단항 산술 연산자를 이용하는 방법
4. \* 산술 연산자를 이용하는 방법
```
Number('10.33')       // 10.33

parseInt('10.33')     // 10

parseFloat('10.33')   // 10.33

+true                 // 1

'10.33' * 1           // 10.33

'-1' * 1              // -1
```


<br/><br/><br/>

## 불리언 타입 변환
1. Boolean 생성자 함수를 new연산자 없이 호출하는 방법
2. ! 부정 논리 연산자를 두 번 사용하는 방법
```
Boolean('x')          // true
Boolean('false')      // true
Boolean({})           // true

!!'x'                 // true
!!''                  // false
!![]                  // true
```

<br/><br/><br/>

## -단축 평가

단축평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.

(&&) 논리곱 연산자는 논리 연산의 결과를 결정하는 두 번째 피연산자를 그대로 반환한다.

(||) 논리합 연산자는 논리 연산의 결과를 결정한 첫 번째 피연산자를 그대로 반환한다.

(??)null 변합 연산자는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고 아니면 좌항의 피연산자를 반환한다. 주로 변수에 기본값을 설정할 때 유용하다.
```
'Cat' && 'Dog'          // 'Dog'
'Cat' || 'Dog'          // 'Cat'

'' && true              // ''

null ?? 'have some tea'     // 'have some tea'
1 ?? 'have some tea'        // 1
```

<br/><br/>
2022.08.16