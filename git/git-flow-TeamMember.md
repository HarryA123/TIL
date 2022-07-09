# Git flow
[🔗install git flow HERE](https://danielkummer.github.io/git-flow-cheatsheet/index.html)<br/>

- 들어가기 전에...


  팀원들과 협업할 때 우리는 branch main에서 직접 작업하지 않고 branch develop에서 간접적으로 작업해야 한다. 팀원이 develop 에서 작업이 끝나면 github에서 pull request를 하는데 이때 팀장이 git flow release를 해서 main에 merge하는 흐름으로 팀작업이  진행된다.<br/><br/><br/><br/>

## ◼ github fork

팀원은 team organization 에서 이슈를 생성한 뒤에 fork를 한다.

코드를 fork하면 내 github repository에 원작 코드가 그대로 COPY 되어 불러와진다.<br/>
<img style="width:400px" src="https://velog.velcdn.com/post-images%2Fimacoolgirlyo%2Fcbe5ca40-5f44-11e9-88b2-25d00148b532%2Fgitfork.png" alt="https://velog.velcdn.com/post-images%2Fimacoolgirlyo%2Fcbe5ca40-5f44-11e9-88b2-25d00148b532%2Fgitfork.png"><h6>출처: https://velog.io/@imacoolgirlyo</h6> fork와 clone의 차이는 분명하다. fork는 team repository를 my repository로 그대로 fork(copy되어) 해오는 것이고 clone은 어떤 repository를 my local에 불러올 때 사용한다.<br/>



만약 이렇게 해서 생성된 fork를 취소하고 싶다면 그냥 새로 생성된 repository를 삭제하면 된다.<br/><br/><br/><br/>



## ➡ git clone 주소

그럼 이제 git bash를 켜서 dev로 간 뒤 'git clone 주소'를 하자. 이때의 주소는 내가 방금 전까지 fork한 내 repository에 있는 코드를 가져와야 한다.

clone을 끝내면 dev 내에 팀 directory가 생성된다. 이 directory로 들어가서 작업하면 된다.<br/><br/><br/><br/>

## ➡ git flow init

team directory 로 들어오면! 여기서부터 이제 git flow가 시작된다.<br/>
<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnRRkH%2FbtrGQDpu9Ur%2FhYKxe1K5WAnFIP54nlW3MK%2Fimg.png"><br/>

git flow init을 하면 새로운 브랜치 develop을 생성한다는 문구와 그 외의 기본 셋팅 관련한 문구가 뜬다. $가 나올 때까지 엔터를 누르자.<br/><br/><br/><br/>

## ➡ git flow feature start 기능이름

git flow init이 끝나면 이제 작업을 시작하자.
'git flow feature start 기능이름'을 하고 git branch로 상황을 확인해보면 main, develop, feature/기능명 세 가지가 생성된 걸 볼 수 있다. 그리고 현재 내가 위치한 branch는 feature/기능명인 것도 확인 가능하다.<br/><br/>

<img style="width:200px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclSUj0%2FbtrGRiZub2K%2FS8ZLvbWAQcvy4WuFctDlc1%2Fimg.png"><br/>

- develop에 기반한 새로운 브랜치(feature) 생성
- 브랜치(feature)로 위지 전환<br/><br/><br/><br/>

## ➡➡ touch 파일생성

feature로 이동한 상태에서 본격적으로 파일을 생성해서 작업을 하면 된다.
index.html, main.css, feature.js 등등 자기가 issue 생성한 내용에 걸맞은 파일을 생성하자.<br/><br/><br/><br/>

## ➡➡ vi 파일

해당파일의 작업을 진행한다.<br/><br/><br/><br/>

## ➡➡ add git 파일

파일 작업이 완료되면 git add 해서 commit stage에 올리자.<br/><br/><br/><br/>

## ➡➡ git commit

stage에 올라온 new file  commit<br/><br/><br/><br/>


## ➡ git flow feature finish 기능이름

git commit 까지 완료가 되면 touch 파일 하기 직전에 해주었던 git flow feature start 기능이름을 다시 finish로 닫아주면 된다.<br/><br/>

<img style="width:200px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJXYra%2FbtrGQFgz92i%2FoRhTQI3hhWLPhENKeO56Zk%2Fimg.png"><br/>
- feature에서 develop으로 위치 이동
- branch feature 삭제
<br/><br/>

---
❗❗❗ 헷갈렸던 점❗❗❗<br/><br/>
 이 feature finish를 어느 시점에서 해줘야 하는지 헷갈렸다. 파일 작업을 완료하고 바로 feature finish를 해야 하는지 아니면 파일을 commit 까지 끝내고 해야 하는지. 정답은 add, commit까지 끝내고 feature finish를 해야 한다.<br/><br/> 
 안 그러면 이렇게 무시무시한 Fatal 메시지가 뜬다. <br/><img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmOEU6%2FbtrGPotEiaZ%2FB8rQskkAimGCWIEvKTvQNK%2Fimg.png"><br/><br/>
그래서 일단 파일 작업이 끝났으면 add, commit은 습관적으로 하는 게 좋을 것 같다. [작업 끝-add-commit]은 한 세트로 생각하자!

----
<br/><br/> <br/>
## ➡ merge commit

'git flow feature finish 기능이름'을 치면 곧바로 merge commit이 열린다. 그냥 변경사항 없이 저장하거나 수정 후 저장하고 나가면 된다.<br/><br/> <br/><br/> 




## ➡ git push origin develop
merge commit 까지 끝나면 이제 remote repository로 push하는 일만 남았다.
만약 팀장이 github에 branch develop을 미리 생성시켜놨다면 저대로 git push origin develop을 하면 된다. 하지만 없다면!?<br/> <br/> 

```
git push -u origin develop
```
flag '-u' 를 써서 remote repository에 develop이라는 branch를 최초 생성할 수 있다. 최초 생성할 때만 -u 를 쓰기 때문에 다음 push 때는 -u를 뺀 git push origin develop을 사용한다.<br/><br/><br/><br/> 

## ◼ pull request
github의 내 repository로 돌아오자. 이곳에서 pull request를 하면 되는데, 이것의 역할은 내가 방금까지 작업한 작업물을 team repository에 pull 해달라고 팀장한테 요청하는 것이다.

즉, 앞서 team repository에서 my repository로 fork해서 COPY본을 가져왔다. 그리고 push까지 끝난 내 작업물을 pull request를 통해서 팀장한테 team repository로 합쳐달라고 요청을 보내는 것.

이때 중요한 것은 my repo (develop) 에서 team repo (develop)으로 선택해야 한다. my repo (develop) 에서 team repo (main) 으로 가면 진실의 방으로...😱💫🔨<br/><br/>
> Create 버튼을 누르면 입력창이 뜬다. 이때 내가 처음에 생성했던 issue의 해시태그 번호를 가져와(내가 만든 issue 창을 보면 제목 옆에 #번호가 붙어 있다.) close 하면 "#번호 issue 해결(닫음)" 이라는 의미의 문법이 완성된다.<br/><br/><img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNIMMt%2FbtrGQ1cGjdx%2FBf2w54BUojc3sPq3J6U9B1%2Fimg.png"><br/> 'close' or 'resolve' 를 사용한다.

<br/><br/><br/>
# pull(fetch-merge)
끝!!!인 줄 알았지? 끝이 아니다. 지금까지 내가 최초의 작업 시작자였을 때의 과정을 다루었다.<br/><br/>

<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlZGOB%2FbtrGTx9L2lH%2FfRMBOM2zy25sv8fhg3BXrK%2Fimg.png"><h6>출처: https://velog.io/@imacoolgirlyo</h6>


내가 다른 팀원의 최신 작업물을 끌어와서 그 위에다가 충돌 없이 작업을 해야 될 때는 어떻게 해야 할까? 두 과정에서 어떤 차이가 있는지 알아보자!<br/><br/><br/><br/>

## ➡ git remote

git remote 명령으로 현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다. 이 명령은 리모트 저장소의 단축 이름을 보여준다. 저장소를 Clone 하면 origin이라는 리모트 저장소가 자동으로 등록되기 때문에 origin이라는 이름을 볼 수 있다.

사용 타이밍: git flow init을 하기 전. 그니까 git clone 주소를 친 후에 ▼아래의 작업을 하는 게 좋다.<br/><br/><br/><br/>

## ➡ git remote add upstream 팀주소

origin이 아닌 upstream이라는 이름으로 remote 팀주소를 추가한다는 의미다. team repo의 url을 등록할 수 있다.<br/><br/>
<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8K0X3%2FbtrGSxaThHC%2FkeXSrjSexmEUfi3TSgTDa0%2Fimg.png"><br/><br/><br/>

## ➡ git pull upstream develop
자, git remote add upstream 팀주소를 쳐서 upstream이라는 팀 저장소를 불러왔다. 이젠 git pull upstream develop을 하면 upstream이라는 저장소를 develop으로 당겨오게 된다. 이 상태에서 ls 해서 확인하면 최신의 작업 현황들을 볼 수 있다.<br/><br/><br/><br/>

😁나도 이제 git협업 마스터! release는 다음에 알아보자!<br/>
<img style="width:400px" src="https://www.devguide.at/wp-content/uploads/2019/06/git-basic-commands.png"><h6>출처: https://www.devguide.at/en/git/pull-push-the-remote-repository/</h6>
위 그림을 알아볼 수 있다면 어느정도 git commands를 이해하고 있다는 의미다.


2022.07.08