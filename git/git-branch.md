지금부터 작업하려는 현재의 branch 위치는 master(or main)라는 곳이다.<br/><br/><br/>


## git branch
<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FliaWD%2FbtrGNWimQRZ%2FQnzJy3DklZv4OOoDIdCLM0%2Fimg.png"/><br/>

git branch의 위치는 master다. master에 커밋된 히스토리는 this is 1~3까지 있다.<br/> 이 상태를 기준으로 하나의 분기점을 만들고 싶다면 다른 branch를 생성해야 한다.<br/><br/><br/>

## git branch 브랜치이름

box1이라는 브랜치 하나를 생성해보자!

<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FboBxjt%2FbtrGPnzHzVH%2FQELvkdw0xKykxQXtjxYXw0%2Fimg.png"/><br/>

master 위에 box1이라는 branch 하나가 생성됐다.<br/><br/><br/>

## git switch(or 'checkout') 브랜치이름
<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc8nEpv%2FbtrGLd6ubeJ%2Fnk56yli1oFfNCkdWxkLhek%2Fimg.png"/><br/>

지금 현재 위치는 master에 있는데, box1로 가려면 git switch 를 사용하면 된다.

위 사진을 보면 master에서 box1으로 이동해 간 것을 확인할 수 있다.
그럼 방금 만든 box1에서의 커밋 상황은 어떤가 git log를 해보자<br/><br/><br/>


<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbz1O7S%2FbtrGOaVut4S%2F9D4kGyWLHWgKPEUR5evl6k%2Fimg.png"/><br/>

git log 를 했더니 방금 만든 box1에는 master에서 커밋한 히스토리가 복사 붙여넣기 한 것처럼 똑같이 기록되어있다. 

box1에서 하나의 md파일을 생성해서 this is 4 라고 커밋해서 다시 master로 돌아가 커밋 히스토리를 보자.

box1에서의 새로운 커밋이 master에도 똑같이(싱크) 생길까?<br/><br/><br/>



<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDbqrs%2FbtrGPIXLAMO%2Fxcv4PH84lcMOy1nlGTnqGk%2Fimg.png"/><br/>

같은 방법으로 git switch master 해서 master로 진입한 뒤 git log로 커밋 히스토리를 봤더니 this is 4 라는 커밋은 업데이트 되지 않았다.

즉, 다른 브랜치 box1에서 했던 커밋 작업은 master에 싱크되지 않았다.

브랜치라는 건 master에 자동으로 영향을 끼치지 않는 개별적인 것이고, 브랜치가 하나 생성 될 때만 master의 커밋 히스토리가 그 생성 브랜치에 카피된다. <br/><br/><br/>

## git merge 브랜치이름
master에 box1에서 새로 만들어진 this is 4라는 커밋을 새로 업데이트 하려면 git merge 를 이용해서 합치면 된다.

git merge 사용시 주의사항은 꼭 master(or main) 위치에서 사용해야 한다는 것. 

master에서 box1의 '커밋을 끌고 와서 합치기' 를 해야 한다.

그럼 box1을 merge해보자.<br/><br/><br/>


<img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F81muI%2FbtrGLeRTYYU%2FVGtNRGoJULJ9mxPfhgIwJ1%2Fimg.png"/><br/>

merge했더니 master에 'this is 4'라는 새로운 커밋 히스토리가 생겼다!

box1에서 만들었던 4.md라는 파일도 merge로 끌려왔음을 확인할 수 있다. <br/><br/><br/>

#### Q : 만약 이미 새로운 브랜치(box1)가 있는 상황에서 master에 새로운 커밋이 생기면, 새로운 브랜치에도 똑같이 자동으로 업데이트 될까?
<details>
<summary>정답은?</summary>
<div markdown="1">       
 <img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqoBtM%2FbtrGO8ppg3e%2FJQ9Kh0ikbGc5pCvL9s44Y1%2Fimg.png"/><br/>
X 아니오!<br/>
master에서 5.md를 'this is 5' 로 커밋한 상황인데 브랜치 box1에서는 업데이트 되지 않는다.
</div>
</details><br/><br/><br/>


#### Q: 새로운 브랜치(box1) 에서 master의 새로운 커밋들을 merge 해서 가져올 수 있을까?
<details>
<summary>정답은?</summary>
<div markdown="1">       
 <img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNRKfi%2FbtrGMp6x9om%2FUg7yfx3Ljg0gMnlQO7i7rk%2Fimg.png"/><br/>
O 네!

box1에서 master를 merge했더니 git log에 this is 5라는 커밋이 뜬 걸 확인할 수 있다.
</div>
</details><br/><br/><br/>


## git branch -d 브랜치이름

그럼 이제 box1에 있는 커밋들을 master로 다 끌어왔으니까 더이상 box1은 필요가 없다.

box1브랜치를 삭제하고 싶으면 git branch -d 브랜치이름 을 써주면 된다.

 <img style="width:400px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvVdLi%2FbtrGPn7R3Vj%2FYKLb1KCjrjpsYTJZsV6Lf0%2Fimg.png"/><br/>

하고서 git branch 했을 때 master만 남고 box1은 없어진 걸 볼 수 있다.

2022.07.08