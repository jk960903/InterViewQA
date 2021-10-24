# REST API 란

- url을 통해 웹 서버로 데이터를 요청하는 방식 (REpresentational State Transfer)

## Parameters
- header
  - data를 보내기 전에 
- param
  - 주소에 포함된 parameter 
    - ex) /post/get-data/35 <--이거
- query
  - 주소에 쿼리로 달리는 parameter
    - ex) /post/get-data?id=35&user=choi
- body
  - 주소에 데이터 요청시 보낼 parameter를 담는 파트
    - ex) application/json, { "id":35,"user":"choi" } <-- 반드시 양식을 꼭 지켜서 보내야 함 (알아서 컨버팅 해주기도 하지만 안해주기도 함)

## WEB 호출 순서
1. URL 호출
2. Request 요청
    * 헤더와 함께 요청
3. 헤더를 확인 후 요청에 상응하는 로직 수행
4. 응답을 Response Body를 통해 응답
    * 헤더와 함께 응답 
5. 응답 후 추가적 리소스 재요청
6. 클라이언트 (웹 브라우져)가 랜더링

## 호출 종류
- Preflight (사전)
  - 실제 요청 전 Options method로 사전 요청을 보냄 (외부 리소스로 요청시 반드시 보냄)
  - 필수 헤더
    - Origin (요청 출처), Access-Control-Request-Method(실제 요청 메소드), Access-Control-Request-Headers(실제 요청 헤더)
    - 정상 응답시, 응답 헤더에 응답 캐시 기간동안 Preflight를 요청 하지 않아도 응답되게 처리함
- Simple (단순)
  - Method가 GET, POST, HEAD이고, <br>
Content-Type이 <b>Application/x-www-form-urlencoded, multipart/form-data, text/plain</b> 이고 <br>헤더에 Accept,Accept-Language,Content-Language,Content-Type만 있을 경우 허용됨
- Credentialed (인증)
  - 인증 관련 헤더를 포함할때 사용하는 요청
    - 클라이언트 : credentials : include, 서버 : Access-Control-Allow-Credentials : true, ""-Origin: *이면 안됨)

## API 호출시 default 값
![image](https://user-images.githubusercontent.com/35089404/137683364-07562b77-3eb7-450a-9619-bfeb3ed94aeb.png)

## 데이터 전송 방법
### Postman Body
![image](https://user-images.githubusercontent.com/35089404/137692461-af8bab21-eab8-4582-a996-f60347e1fb1c.png)

- form-data
  - Content-Type:multipart/form-data 의 형태로 <form>를 사용해 Post 요청을 할 경우 주로 사용 됨 주로 file 데이터를 binary화 하여 사용함
- x-www-form-urlencoded
  - Content-Type:multipart/form-data 의 형태로 <form>를 사용해 Post 요청을 할 경우 주로 사용 됨 value data에 file 데이터를 사용하기에는 부적절함 (용량 문제)
- raw (json, text)
  - Content-Type:application/json 등의 형태로 String 그대로 raw한 데이터를 전송할때 주로 사용 됨. 
  - 주로 사용하는 통신 방법 (~2021~)
  
## 데이터 수신 방법 (Spring boot)
  ![image](https://user-images.githubusercontent.com/35089404/137702003-9b68a1c2-d113-41d0-8361-e4a160cfda81.png)
  
    - 해당 방법은 Jackson Library가 설치되어 있어야 하는 것 같음
  
  
  ![image](https://user-images.githubusercontent.com/35089404/137702062-79a78b55-b983-49c0-9118-1a3ff6083ada.png)
  
  
  ![image](https://user-images.githubusercontent.com/35089404/137702362-ecde1e18-54db-4d9f-b030-6483ab9c1e82.png)
  
    - 암묵적으로 @ModelAttribute가 사용된다고 함



## 참고자료
- https://www.youtube.com/watch?v=-2TgkKYmJt4 (우테코 CORS)
- https://blog.naver.com/PostView.nhn?blogId=writer0713&logNo=221853596497&redirect=Dlog&widgetTypeCall=true&directAccess=false (Backend parameter 처리 방법)
