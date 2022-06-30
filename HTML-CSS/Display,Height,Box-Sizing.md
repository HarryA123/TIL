## Display : Initial;

말 그대로 display 속성을 초기화 한다는 의미다.
-> header에서 width 크기를 줄이고 늘렸을 때 메뉴의 center or right 부분이 사라지거나 생기길 원할 때 이 값을 쓰곤 한다.
display : initial; 해서 무언가가 생기길 원한다면, 당연히 그 css 윗줄에서 display: none; 이 되어 있어야 한다.




## Height: 100% VS Height:100vh

- height:100% : 부모에 의존적으로 사용된다. 부모 크기만큼 100% 채우겠다는 의미로, 이 때 부모의 height 속성 값이 설정되어 있어야 한다. 
- height: 100vh : 만약 부모에게 의존하지 않고 독립적으로 height 값을 주고 싶다면 height : 100vh 를 사용한다.

height : 100vh 는 부모에 의존하지 않고 독립적으로 viewpoint를 100% 채우겠다는 의미다.
공통적으로는 둘 다 height 값을 100% 채우는 것은 같으나 부모 크기에 의존하냐 안 하냐는 차이가 있다.




## Box-Sizing

자주 헷갈렸던 부분이다.
박스의 크기를 content로? 또는 border까지 포함해서? 라고 묻는 속성이다.
content-box 로 지정했을 경우, width와 height 크기가 content 크기만큼 늘어나고 줄어든다.
border-box 로 지정했을 경우, width와 height 크기가 border까지를 포함(즉, content+padding+border를 포함. margin은 포함하지 않음)해서 크기가 늘어나고 줄어든다.

- box-sizing : content-box;    "content 영역까지만 계산하세세요"
- box-sizing : border-box;     "border 영역까지 계산하세세요"

