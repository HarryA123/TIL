# Position
- **static** : (default) 기준 없음. position이 none인 것과 같다.
- **relative** : 자신을 기준으로 이동한다.
- **absolute** : 위치 상 부모를 기준으로 이동한다.
- **fixed** : viewport 기준으로 이동해 고정된다.  

**static**![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZmz3s%2FbtrGfmht1Fn%2FqCojDoNQW3NnsgtG7gZfD1%2Fimg.png)
기준이 없는 상태. top과 left값을 줬는데도 position: static 임으로 변함 없다.  


**relative**![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fx1rXo%2FbtrGdtBbxOq%2FvIdATzaZJBH7igkyrOKgf0%2Fimg.png)  

1. 다른 요소에 영향을 끼치지 않음.
2. 자신을 기준으로 이동한다.(자기 맘대로 움직인다.)  


me(2번box)에 position : relative; 를 줬더니, 자기 혼자 top: 100px; left:100px 만큼 이동했다.

원래 있었던 위치는 빈 공간으로 아직도 존재한다. 제 위치에서 나갔으면 밑에 있는 3번이 2번 자리를 꿰차야 하는데 2번 자리가 그대로 빈 공간으로 남아 있는 것으로 보아 다른 요소에 아직까지 영향을 끼치고 있다고 볼 수 있다.  

즉, relative 된 2번 박스는 사실 우리가 '보기에는' 움직인 것 같지만 실제로는 움직인 것이 아니라 1번과 3번 사이 그 자리에 위치하고 있다. 그래서 2번의 움직임은 허상으로 보기도 함.  

자기혼자 붕 떠서 이동하고, grandparent 밖으로도 나갈 수 있다.
자기 맘대로 움직이고 싶은 대로 움직인다.
이런 방식은 사실 자주 사용되지 않는다.  



**absolute**![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFLiK6%2FbtrGfyn334q%2FNtzULAlwqSm2igKTCVNsa0%2Fimg.png)
1. 부모를 기준으로 이동한다.  

2. 이때 부모를 설정하는 방법은 기준이 되었음 하는 부모에 position:relative; 속성값을 설정한다.  

3. 부모가 없다면 뷰포트 기준으로 이동한다.  

2번에 position : absolute를 줬더니 위에 relative와는 다른 점이 확실히 드러난다. 2의 빈자리를 3이 대체한다.

즉, absolute 되면 상대요소에 영향을 끼치지 않는다. 이 상태는 허상이 아니다. 실제로 2번 박스는 자기 위치에서 빠져나왔고 3번이 2번의 자리를 꿰찼다.  


2번에만 absolute를 줬을 때는 relative처럼 grandparent 밖으로 나갈 수 있다.(뷰포트를 기준으로 이동함) 하지만 이건 부모 기준을 설정하지 않았기 때문에 가능하다. 위에서 말했듯이 부모를 기준으로 위치할 수 있기 때문에! 부모만 지정해준다면 그 부모를 기준으로 위치할 수 있다.  


**fixed**![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJgwJy%2FbtrGaYbeiMc%2FYNhEYkNxIsATmMeZJ0Gz71%2Fimg.png)  

1. position:fixed는 무조건 viewport를 기준으로 이동한다.  


그래서 위의 사진을 보면 2번 박스를 position : fixed  했을 때 viewport를 기준으로 이동한 것을 볼 수 있다. 부모요소에 position:relative가 있어도 그걸 무시 하고 무조건 viewport에 기준으로 붙는다. (fixed값은 absolute값과 달리 부모의 영향을 안 받음)  
position:fixed 는 가끔 홈페이지 들어가보면 상담톡 같은 용도에 사용된다. 상담톡은 보통 viewport 하단 오른쪽에 붙어있다.


07.01,2022
