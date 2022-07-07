## git log

내가 위치한 디렉토리의 커밋들 히스토리를 보여준다. 그동안 어느 날짜 어느 시간에 누가 어떤 제목의 commit을 했는 지 볼 수 있다.
<img style="width: 400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7DZ9C%2FbtrGLAlCWw2%2F72nkPzLdENQ0PDTNKPWrr1%2Fimg.png"><br/><br/><br/>

## git log -p
내가 했던 커밋들 사이사이에 어떤 점이 바뀌었는 지 모두 알려준다.

<img style="width: 400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSotwA%2FbtrGM3Vbc8u%2FBri8xqKQKVApQwmzkuEI31%2Fimg.png"><br/>

커밋들은 각자의 고유 주소를 가지고 있다. 위 사진에 보면 노란색으로 표시된 부분이 그 주소에 해당한다.

가장 위에 있는 내용만 보면, feat: 6 으로 커밋된 것은 내용에서 yellow lemon!!!!! 에서 yellow peer로 바뀌었음을 읽을 수 있다.<br/><br/><br/>


## git diff 커밋주소..커밋주소

특정 커밋 사이에 달라진 점을 확인할 수 있다.

위에서 git log 했을 때 나왔던 노란색 부분의 커밋 주소 두개(커밋 사이에 변화를 알고싶은 것 두개)를 가져와서 ..의 양 옆에 배치하면 된다.<br/><br/><br/>


## git reset 코드주소 --hard
최근에 했던 커밋들을 리셋하고 현재 커밋된 부분에서 (예를들어)3번째 뒤에 있는 커밋으로 돌아가고 싶다고 했을 때 이 코드를 실행시킨다. 하지만 코드를 리셋하는 것은 현업에서 안 하는 게 좋다. 더해서 이미 저장소에 공유가 됐다면 reset은 더더욱 안 하는 게 좋다.

가장 최신의, 커밋이 되었으면 하는 코드주소(노란색)를 복사해서 저 위의 문법에 넣으면 내가 고른 그 코드 시점이 가장 최신의 커밋이 되고 원래! 진짜 최신의 커밋들은 모두 리셋된다.

나는 yellow peer, yellow lemon 이전에 커밋했던 원래의 상태인 yellow banana가 가장 최신의 커밋이었으면 해서 해당하는 코드 주소를 넣고 reset을 했다.<br/><br/>

<img style="width: 400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQEAvX%2FbtrGKce0pUM%2FnypgMbVh7ixiuL5pONUbK1%2Fimg.png"><br/>
그럼 HEAD is now at 0fed79a feat: 3 이라고 뜬다. 여기서 중간에 있는 0fed79a는 내가 선택한 코드주소의 앞머리다.

정말 feat:3 이라는 커밋까지 리셋이 됐을까? git log -p 를 쳐서 다시 보자.<br/><br/>

<img style="width: 400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEZu1m%2FbtrGLfPA5Pj%2FNHQ66d0Ie7yEU8KHJqR8w0%2Fimg.png"><br/>
정말 feat: 3이라는 커밋이 최신의 커밋이 된 걸 볼 수 있고 그 앞에 했던 yellow lemon이나 yellow peer는 리셋되어 없다.<br/><br/>


<img style="width: 400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXKyvT%2FbtrGJNTUPvd%2FF4I02frcLuID877A2RfnMk%2Fimg.png"><br/>
정말 내용도 yellow banana 상태로 돌아갔나 확인해보니 내용이 정말 yellow banana로 바뀌어 있다.

reset 말고 revert 를  쓸 수 있다. revert는 reset과 좀 다르다. reset은 그냥 없애는 건데 revert는 어떤 이유로 다시 어떤 상태로 돌아갔음을 명시하는 커밋을 만들 수 있도록 한다. 그래서 굳이 쓰자면 reset 보다는 revert를 사용하는 게 좋다.

2022.07.07