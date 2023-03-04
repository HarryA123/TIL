# Typescript

타입스크립트는 마이크로소프트에서 개발한 오픈소스 프로그래밍 언어이며, 자바스크립트의 단점을 보완하기 위해 만들어졌다.

</br></br>

## Typescript의 기본 타입

Boolean(진위 값), Number(숫자), String(문자열), Object(객체), Array(배열), Tuple(지정된 배열 형식), Enum(특정 값들의 집합), Any(모든 타입 허용), Void(undefined 와 null 만 할당, 함수에는 반환 값을 설정할 수 없는 타입), Undefined, Never(함수의 끝에 절대 도달하지 않는다는 의미를 지닌 타입)

</br></br>

## Typescript 도입 시 장점, 단점

</br>

장점

1. Static Type-Checking : 정적 타이핑 언어이고 런타임 타임이 아니라, 컴파일 타임에 타입 체킹이 가능하기 때문에 관련된 오류를 예방할 수 있다.
2. Optional Static Typing : 자바스크립트 코드를 포함할 수 있다.

</br></br>

단점

1. 라이브러리 호환 문제 : 자바스크립트 라이브러리를 타입스크립트에서 사용하려면 일반적으로 추가적인 작업이 요구된다.
2. 추가적인 컴파일 시간 : 컴파일하는 데, 추가적인 시간이 요구된다.

</br></br>

## Typescript 사용 예

```js
const user = {
  name: "Hayes",
  id: 0,
};
```

위와 같은 객체의 모습을 interface 선언으로 분명히 설명할 수 있다.

```js
interface User {
  name: string;
  id: number;
}
```

그런 다음 ':' 콜론을 사용하여 타입의 이름을 상수 이름 오른쪽에 선언한다.

```js
const user: User = {
  name: "Hayes",
  id: 0,
};
```

만일, 객체의 자료형과 타입(interface)이 매치되지 않다면 경고문자가 뜬다.
```js
interface User {
  name: string;
  id: number;
}
 
const user: User = {
  username: "Hayes",
Type '{ username: string; id: number; }' is not assignable to type 'User'.
  Object literal may only specify known properties, and 'username' does not exist in type 'User'.
  id: 0,
};
```
위 경우에, interface에는 name으로 정해진 것이 user 객체 안에 username으로 정해졌기 때문에 매치가 안 되어 오류가 생긴 것이다. 그래서 User타입 안에 username이 존재하지 않다는 경고문이 뜬다.


