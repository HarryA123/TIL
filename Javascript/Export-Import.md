# Export 해서 내보내기

변수, 함수, 클래스 앞에 export를 붙이면 그 해당 변수, 함수, 클래스 <strong>내보내기</strong>가 된다.

이때 함수와 클래스 선언 끝에 ; 세미 콜론을 붙이지 않는다.<br/><br/>

 

```
SYNTAX
export 변수, 함수, 클래스
```
```js
export let fruits = ['apple', 'banana', 'mango']
```

expert문은 선언부 위에서 쓰나 아래에서 쓰나 결과는 동일하다.<br/><br/><br/>

 

## export default
이는 보통 파일 내에서 한 개만 export하거나 대표로 export 할 때 쓴다. export default는 아래처럼 import 한다.
```
import 함수명 from './함수가 속한 파일명'
```
 으로({}중괄호 없이 사용 가능) 가져올 수 있다. <br/> 

그럼에도 불구하고 default는 자주 사용하지 않는 것이 권장된다.<br/><br/><br/><br/>

# import 해서 가져오기

```
SYNTAX
import {가져올 함수명} from './함수가 속한 파일명'
```
```
import {sayHello} from './function.js'
``` 

function.js에서 sayHello라는 함수를 가져왔다.<br/><br/>

 

많은 함수를 한꺼번에 가져올 때는 import * as 를 사용하기도 하지만 이 방법보다는 아래처럼 하나씩 명시해주는 것이 좋다
```
export function putThis(){~~}
export function putCup(){~~}
export function putPaper(){~~}
```

실제 코딩 하면서 export 와 import를 자주 사용해보자~

2022.07.011