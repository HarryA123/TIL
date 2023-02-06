# MVC

MVC패턴은 웹 애플리케이션 개발 방법론 중 하나이다. 

<img width="300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2452883B57F0B3C02B">

- Model: 데이터를 가진 객체, 파라미터로 자주 쓰인다. DB의 테이블과 대응하는 경우가 많다.

- View: UI를 담당한다. 클라이언트 측 기술인 Html, Css, Javascript등으로 만들어진 컨테이너이다.

- Controller: UI를 통한 사용자의 입력 명령에 응답하고, 및 데이터 흐름 제어를 담당한다.

사용자는 컨트롤러를 사용해서 웹 애플리케이션을 다룰 수 있다. 컨트롤러는 사용자의 요청에 맞는 데이터를 모델에 요청한다. 그러면 뷰는 모델이 리턴한 결과를 반영하여 유저가 볼 수 있게 한다.

이처럼 MVC패턴의 장점은 사용자에게 보여지는 프레젠테이션 영역과 비즈니스 로직, 데이터 구조가 완전히 분리되어 있다는 점이다. 

</br></br>

## MVC model-1, model-2

<img width="300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F270EFE4C57F0C7A61C">

- 모델1은 비즈니스 로직 영역(controller)에 프레젠테이션 영역(view)를 같이 구현하는 방식이다. 이 방식은 빠르고 쉽게 개발할 수 있다는 장점이 있지만 controller와 view가 혼재하므로 향후 유지보수에 어려움이 있을 수 있다.
</br>

- 모델2는 비즈니스 로직영역과 프레젠테이션 영역이 분리되어 있는 구현 방식이다. 이 방식은 view와 controller가 분리되어 있기 때문에 디자이너와 개발자의 분업이 가능하며 유지보수에 유리하다. 하지만 설계에서 어려움을 겪을 수 있고, 개발 난이도가 높다는 단점이 있다.

대부분 MVC 모델2 방식으로 개발한다.


