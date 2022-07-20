# 정규표현식 (RegExp)

정규식, Regular Expression
<br/><br/><br/>
## 역할

- 문자 검색(search)
- 문자 대체(replace)
- 문자 추출(extract)
<br/><br/><br/>

## 테스트 사이트
https://regexr.com/
<br/><br/><br/>

## 정규식 생성

```js
//생성자
new RegExp('표현', '옵션')
new RegExp('[a-z]', 'gi')

//리터럴
/표현/옵션
/[a-z]/gi
```

- g : '표현' 안에 있는 모든 단어를 찾아 배열 데이터를 만들고 싶다면 g를 옵션에 추가한다.

- i : 대문자, 소문자를 구분하지 않고 '표현'을 찾는다.
<br/><br/><br/>

## 예제 문자
`
010-1234-1234
google@google.com
The EventTarget interface is implemented by the objects that can receive events and may have listeners for them.
https://heropy.blog/2018/10/28/regexp/
aabbccddee
`
<br/><br/><br/>
## 메소드

메소드 |문법 |설명
--|--|--
test |`정규식.test(문자열)`| 일치 여부(Boolean) 반환)
match |`문자열.match(정규식)`|일치하는 문자의 배열(Array) 반환
replace|`문자열.replace(정규식,대체문자)`| 일치하는 문자를 대체
<br/><br/><br/>

## 플래그 (옵션)

플래그 | 설명
--|--
g|모든 문자 일치(global)
i|영어 대소문자를 구분 않고 일치(ignore case)
m|여러 줄 일치(multi line)

<br/><br/><br/>

### 이스케이프 문자

\백슬래시 기호를 통해 본래의 기능에서 벗어나 상태가 바뀌는 문자를 말한다.

그래서 예를 들면. '.' 이라는 것은 특정한 명령을 실행한다는 의미이기 때문에 온전히 .을 출력하고 싶다면 앞에 백슬래시를 사용해야한다.

.$ 는 하나의 단어로 해당하는 줄이 마침표로 끝나는 부분을 찾아서 끝나는 부분을 일치시킨다.

<br/><br/><br/>

## 패턴

패턴 | 설명
--|--
^ab| 줄(Line) 시작에 있는 ab와 일치
ab$| 줄(Line) 끝에 있는 ab와 일치
.| 임의의 한 문자와 일치
a&verbar;b | a또는 b와 일치
ab? | b가 없거나 b와 일치
{3} | 3개 연속 일치
{3,}| 3개 이상 연속 일치
{3,5}| 3개 이상 5개 이하(3~5개) 연속 일치
[abc]| a또는 b 또는 c
[a-z]| a부터 z사이의 문자 구간에 일치(영어 소문자)
[A-Z]|A부터 Z사이의 문자 구간에 일치(영어 대문자)
[0-9]|0부터 9사이의 문자 구간에 일치(숫자)
[가-힣]|가부터 힣 사이의 문자 구간에 일치(한글)
\w| 63개의 문자(word, 대소영문52개 + 숫자10개 + _)에 일치
\b| 63개 문자에 일치하지 않는 문자 경계(boundary)
\d| 숫자(digit) 에 일치
\s| 공백(space, tap) 에 일치