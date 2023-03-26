# 2023-1-BE-Web-Study
2023 1학기 기초 백엔드 스터디 커리큘럼 과제입니다
1. mvc 패턴이란??
우선, mvc란 model, view, Controller의 약자입니다. 하나의 프로젝트를 구성할 때 그 구성요소를 세가지의 역할로 구분한 패턴입니다.
<img src="https://mblogthumb-phinf.pstatic.net/MjAxNzAzMjVfMjIg/MDAxNDkwNDM4ODMzNjI2.nzDNB5K0LuyP4joE2C4rIbL5Ue2F3at7wiI6ZpuTJN0g.WZ6V-WHZygLYW2WSdzcs7uAiAWgAJe3_H0XdkYKkutkg.PNG.jhc9639/1262.png?type=w800">
위의 그림처럼 사용자가 컨트롤러를 조작하면 컨트롤러는 모델을 통해서 데이터를 가져오고 그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달하는 구조이다. 

2. api와 서버 
간단하게 api 란 application programming interface로  한 프로그램에서 다른 프로그램으로 데이터를 주고받기 위한 방법 
예시- 식당 가면 있는 메뉴판과 같은 느낌 
웹툰 프로그램이 있으면
-1.외모지상주의 2.헬퍼 이런식으로 메뉴판 같이 만들어 놓은 것이 api이다. 

api 서버는 '필요한 데이터만 제공하는 서버'를 의미한다. 
-> 화면을 제공하는 것이 아니라 필요한 데이터를 호출하고 결과를 반환 받는 방식으로 동작합니다 .

api가 가져야할 내용:
 요청방식, 무슨 자료를 요청할지, 파라미터( 추가정보)- 웹과 같은경우 REST API 방법을 따라서 작성하면 된다.

3. restful이란??
rest-> 클라이언트 - 서버 통신 방식 ->특정한 uri와 http메소드를 결합해서 특정한 자원에 특정한 작업을 지정하는 방식입니다.

representational
state
transfer
-> 어떠한 상태를 주고 받는 것이 rest이다.

http : 주고받는 프로토콜(규약)이http이다. 
http의 간단한 구성 -url(주소)/하위 리소스(특정한 자원) 지정/
하위 리소스에 대해 
C  -> POST
R  -> GET
U  -> PUT
D  -> DELETE  http프로토콜을 가지고 자원을 핸들링 하는 것
이러한 방식으로 만들어진 서비스를 'RESTful'하다고 표현합니다  

간단한 비유를 통한 예시 
->api를 open을 해서 CRUD롤 맵핑을 해서 오픈을 해주면
  그게 바로 RESTFUL한 서비스가 되는 것이다. 

도서 대출/반납   -> 도서 대출 C (책이 대출되었다는 정보)  
             조회 R(대출을 정보를 읽어온다)    < -  도서관
                 U(대출을 연장하거나 그러한 업데이느)    
                 D(그냥 정보 삭제 해버리기)
도서에 대해 CRUD를 한다.
