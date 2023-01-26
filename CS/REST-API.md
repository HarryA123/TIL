# REST API

REST 는 http를 기반으로 클라이언트가 서버 리소스에 접근하는 방식을 규정한 아키텍쳐다.

REST API는 REST를 기반으로 서비스 API를 구현한 것을 의미한다.

</br>

## API란?
API는 Application Programing Interface 라는 용어로, 어떤 응용프로그램에서 데이터를 주고받기(요청하고 응답하기) 위한 방법이다.

API유형에는 모두에게 공개되는 Public API, 개발자 외 제3자에게 노출되지 않는 Private API, 특정 파트너와 사용하는 Partner API가 있다.

</br>

REST API는 <strong>표현, 자원, 행위</strong>로 구성되어 있다.

</br>

## REST API의 설계 원칙
1. URI는 리소스를 표현해야 한다.
2. 리소스에 대한 행위는 HTTP요청 메서드로 표현한다.

</br></br>

HTTP요청 메서드에는 GET, PUT, POST, PATCH, DELETE 총 5가지가 있다.


|HTTP요청 메서드|종류|목적|
|----|---|----|
|<strong>GET|index/retrieve|모든/특정 리소스 <strong>취득|
|<strong>POST|create|리소스 <strong>생성|
|<strong>PUT|replace|리소스 전체 <strong>교체|
|<strong>PATCH|modify|리소스 일부 <strong>수정|
|<strong>DELETE|delete|모든/특정 리소스 <strong>삭제|

```
GET/todos/1
```

</br></br>




-----

REST 란 HTTP 기반으로 클라이언트가 서버의 자원에 접근하는 방식을 규정한 아키텍쳐다. REST의 기본 원칙을 잘 지킨 서비스를 RESTful하다고 표현한다.

REST API란 이런 아키텍쳐를 기반으로 서비스 API를 구현한 것을 의미한다.

REST API는 자원, 행위, 표현으로 구성되어 있다.

자원은 자원, 행위는 자원에 대한 행위, 표현은 자원에 대한 행위의 구체적 내용을 의미한다. 

REST API의 설계 원칙은 첫 번째로 URI는 리소스를 표현해야 한다. 두 번째로는 리소스에 대한 행위는 HTTP 요청 메소드로 표현한다.

HTTP 요청 메서드로는 5가지가 있다.
모든/ 특정 리소스를 취득하는 목적의 GET, 리소스를 생성하는 목적의 POST, 리소스를 교체하는 목적의 PUT, 리소스를 수정하는 목적의 PATCH, 리소스를 제거하는 목적의 DELETE.
