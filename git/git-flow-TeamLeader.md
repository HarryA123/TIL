# Git flow as a TeamLeader
[🔗install git flow HERE](https://danielkummer.github.io/git-flow-cheatsheet/index.html)<br/><br/><br/>

- 들어가기 전에...

  팀원이 팀 repo를 fork해서 test.md라는 작업물을 push 했다. 그 다음 자기 repo develop에서 팀 repo develop로 request 요청을 했다. 팀장인 나는 그 요청을 merge해서 팀 repo develop에는 test.md가 업데이트됐지만 main으로 merge된 상황은 아니다.

  팀장인 나는 현재 팀 organization을 fork 하지 않았고, 팀repo develop에 새로 추가된 test.md 를 main에 merge하고 싶은 상황이다.<br/><br/>
    <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZyFmp%2FbtrHtwjkUlI%2F0wuk62Zmco1K0x3NQ0CAek%2Fimg.png"><br/><br/><br/>

  따로 git remote -v 했을 때 origin 하나 뿐이며 origin의 주소는 팀 주소로 되어 있다.<br/><br/>
  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbar1kz%2FbtrHqngCmtF%2F4r8WfU9BMdb43Kaz5wOYt0%2Fimg.png"><br/><br/><br/><br/>

## 목표
github main에 test.md 파일을 올리고 이것이 올라간 버전을 v0.2로 release하자!<br/><br/><br/><br/>

## ➡ git pull origin develop

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft4i7I%2FbtrHwlVIsht%2F3xIlcTqczkO4vHDtuOBDCk%2Fimg.png"><br/><br/>

제일 첫 번째 단계는 일단 내 local에 팀 repo develop에 있는 신규 상태를 끌고 오는 것.

팀 repo의 develop을 당겨오자.

그러면 위 사진처럼 create mode ~~ test.md 라고 test.md라는 파일이 만들어졌다고 뜬다.

이제 내 로컬은 최신 상태로 구성됐다. 이렇게 모든 것이 최신 상태라는 것을 확인하고 release를 해야 한다.

주의 : main이 아니라 develop 브랜치에서 행해져야 한다.<br/><br/><br/><br/>


## ➡➡ git flow release start v0.2 

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtQODt%2FbtrHpPjk61h%2FemSqRRNmEX3CBCkT03Ov20%2Fimg.png"><br/><br/>
version 0.2를 release 하겠다고 입력하면 위와 같은 글이 뜬다.

- develop을 기반으로 release/v0.2라는 branch 를 만들었다. (develop 브랜치에 있는 내용들을 가져와서 만들어졌다는 뜻이다.)

- 위치는 develop에서 release/v0.2로 이동되었다.

- start v0.2를 실행한 순간부터는 수정할 것들을 수정하고 모든 준비가 다 끝나면 git flow release finish v0.2라는 동작을 수행해라.

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcap1Sl%2FbtrHpOknmjP%2FzfK41a960tV135M0J4PSTK%2Fimg.png"><br/><br/>

git branch 명령어로 확인해보면 실제로 나는 release/v0.2라는 곳에 위치했다.

이제 main으로 가서 이 v0.2를 당겨오자.<br/><br/><br/><br/><br/>



## ➡➡ git merge release/v0.2 

그럼 이제 main으로 이동해서 v0.2 브랜치의 내용을 끌고 온다.

merge를 했기 때문에 ls 명령어로 확인했을 때 main에 test.md라는 파일이 새롭게 생성된 걸 확인할 수 있다. 모든 걸 다 확인했으니까 finish 하면 된다.<br/><br/>


❓ 사실 이 단계에 대해서는 확신이 없다. main으로 이동해서 release/v0.2를 머지 해오는 행동을 release finish 하기 전에 해야 하는 동작인가? 의문이 든다. 왜냐하면 밑에서 git flow release finish v0.2를 하면 main 브랜치로 머지 됐다는 문구가 뜨기 때문이다. 다음에 다시 한번 release를 해서 이 동작이 확실히 필요한지 확인해야겠다.<br/><br/><br/><br/><br/>


## ➡➡ git flow release finish v0.2

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoyUmM%2FbtrHrNFTemo%2FmEEIsNQ5HxtLvr0nH2Dxr1%2Fimg.png"><br/>

그럼 이렇게 tag 를 써달라는 vi(?)가 열린다. 나의 경우 v0.2라고 저장하고 나왔다.<br/><br/><br/><br/>

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDYuAa%2FbtrHsDXocnf%2FIYpFeG23nJ3EYIPXYU6Sn1%2Fimg.png"><br/>

저러고 나오면 이제 git push 해서 로컬을 커밋 해라, main으로 머지가 됐다, tag는 0.2로 되었다. 그리고 이제 더 이상 필요 없는 브랜치 release/v0.2를 삭제했다. 그리고 내 위치는 main에 있다.라는 문구가 뜬다.<br/>

git branch로 확인해보니까 실제로 난 main에 있고 release/v0.2는 없어졌다.<br/><br/>

- release/v0.2가 main으로 머지 됐다.
- 0.2로 태그 되었다.
- release/v0.2가 삭제되었다.
- 위치가 main으로 이동되었다.
  
  (release finish의 첫 번째와 네 번째 역할을 봤을 때, 앞선 단계에서 굳이 main으로 가서 release/v0.2 를 merge하지 않아도 되는 거 아닌가? 라는 의심이 들었다.)<br/><br/><br/><br/><br/>


## ➡ git push --tags

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTkxhM%2FbtrHvoLVL90%2F3AKgQyusaHrqwZRPOVWWO0%2Fimg.png"><br/><br/>

여기서 주의해야 하는 것이. git push origin main을 하기 전에 tag를 push해야 한다. 말 그대로 tag를 remote에 push 하는 명령어다.

이 단계를 먼저 거치는 이유는 우리는 v0.2라는 tag에 새로 바뀐 버전을 넣어야 하기 때문이다.<br/><br/><br/><br/><br/>


## ➡ git push origin main
  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhiYAT%2FbtrHunfrYaT%2FTxgs6ic1eMNs3fEyhx7Mz1%2Fimg.png"><br/>

깃헙 main에다가 push 하기만 하면 release 작업 완료. 그럼 github team repo로 돌아가 제대로 test.md 가 v0.2에 잘 올라왔나 확인해보자.<br/><br/><br/>

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkQLKU%2FbtrHtvSkIo1%2FjInO5cdWXZXRj6k2VTl8Ak%2Fimg.png"><br/>

확인해보면 main에 test.md 파일이 제대로 들어온 걸 확인할 수 있다.

release 끝!<br/><br/><br/>


## 느낀 점
전에는 팀원으로 참여해서 git flow release 라는 작업을 직접 경험할 기회가 없었는데, 이번에 스터디 조원들과 함께 새로운 organization을 만들어 release를 직접 경험하게 됐다. 내가 release에 대한 경험과 이해가 부족한 상황에서 조원들과 release 하는 바람에 이해가 충분히 되지 않은 상황에서 명령어를 쓴 점이 아쉽다. 근데 TIL 쓰면서 다시 정리해 보니 왜 이런 절차를 밟았는지 이해가 됐다.

release 과정 중에 main에서 release/v0.2를 merge 하는 단계가 있는데, 이 부분이 좀 헷갈렸다. release를 먼저 해본 조원들이 전에 이 과정에서 오류가 있었는데 그걸 해결하는 방법이 main으로 가서 release/v0.2 를 merge하는 것이었다고 해서 했는데, 결과적으로 오류난 건 없었다.

근데 TIL을 쓰면서 보니까 git flow release finish v0.2라는 명령어를 쓰면 위치를 main으로 이동시켜서 release/v0.2를 merge 해오는데 굳이 앞에서 merge를 해줄 필요가 있었을까? 의문이 들었다. 다음에 release 할 때는 그 단계를 뛰어 넘고 바로 release finish를 시도해봐야겠다.<br/><br/>

2022.07.17







