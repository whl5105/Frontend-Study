# CORS
## SOP(Same-Origin Policy)동일 출처 정책이란?
말 그대로 동일한 출처, URL이 동일한 api등의 데이터 접급이 가능하도록 다른 출처의 접근을 막는 브라우저 정책입니다.

![제목 없음](https://user-images.githubusercontent.com/90454621/230934557-15564e37-1ded-451f-ade9-256aac32e0e2.png)

<br/>

## 출처(Origin)란
![image](https://user-images.githubusercontent.com/90454621/231031499-dd65db92-ee90-4cc6-a556-349bd4c0d2c1.png)

출처(Origin)란 위그림에서 `Protocal` `Host` `Port`를 합친 것을 말합니다. 

출처(Origin)가 같으면 `동일 출처(Same-Origin)`라고 합니다. 

브라우저 개발자 도구의 콘솔 창에 `location.origin`를 실행하면 출처를 확인할 수 있습니다.

![image](https://user-images.githubusercontent.com/90454621/230943777-eb56d315-e8e5-4769-982d-e7c6847a90a5.png)

<br/>

## CORS(Cross-Origin Resource Sharing)란

CORS(Cross-Origin Resource Sharing)는 `출처가 다른 자원들을 공유`한다는 뜻으로, 한 출처에 있는 자원에서 다른 출처에 있는 자원에 접근하도록 권한을부여 브라우저에게 알려주는 체제입니다.

![image](https://user-images.githubusercontent.com/90454621/230898269-471ea4e8-7308-4f6d-8877-1d54d4b1ec1e.png)

 결국 api요청시 흔히 보는 CORS 오류문구는 다른 출처에 접근 할 수 있는 권한이 없다는것입니다.

<br/>

 ### 왜 필요한가?
모든 곳에서 데이터를 요청할 수 있게 된다면, `다른 사이트에서 원래 사이트를 흉내`낼 수 있게 됩니다. 만약 기존 사이트와 완전히 동일하게 동작하도록 하여 사용자가 로그인을 하도록 하고, 로그인했던 세션 또는 토큰을 탈취하여 악의적으로 정보를 꺼내오거나 다른 사용자의 정보를 입력하는 등 헤킹을 할 수 있습니다. 하지만 이런 공격을 할 수 없도록 브라우저에서 보호하고, 필요한 경우에만 서버와 협의하여 요청할 수 있도록 하기 위해서 필요합니다.

<br/>

## 다른 출처 요청 정책
### 1.단순요청(Simple Request)
단순 요청 방법은 서버에게 바로 요청을 보내는 방법입니다. 아래 그림은 자바스크립트에서 API를 요청할 때 브라우저와 서버의 동작을 나타내는 그림입니다.

![image](https://user-images.githubusercontent.com/90454621/231039242-cb787526-ac7d-4fde-95e3-d6be4d541440.png)

단순 요청은 서버에 API를 요청하고, 서버는 `Access-Control-Allow-Origin` 헤더를 포함한 응답을 브라우저에 보냅니다. 브라우저는 `Access-Control-Allow-Origin` 헤더를 확인해서 CORS 동작을 수행할지 판단합니다.
### 단순요청(Simple Request)조건
서버로 전달하는 요청(request)이 아래의 3가지 조건을 만족해야 서버로 전달하는 요청이 단순 요청으로 동작합니다.

- 요청 메서드(method)는 GET, HEAD, POST 중 하나여야 합니다.
- Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width를 제외한 헤더를 사용하면 안 됩니다.
- Content-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain 중 하나를 사용해야 합니다.

첫 번째 조건은 어렵지 않은 조건이지만 2번, 3번 조건은 까다로운 조건입니다. 2번 조건은 사용자 인증에 사용되는 `Authorization` 헤더도 포함되지 않아 까다로운 조건이며, 3번 조건은 많은 REST API들이 `Content-Type`으로 `application/json`을 사용하기 때문에 지켜지기 어려운 조건입니다.

<br/>

### 2.프리 플라이트(Preflight Request)
Preflight 요청은 서버에 예비 요청을 보내서 안전한지 판단한 후 본 요청을 보내는 방법입니다. 아래 그림은 Preflight 요청 동작을 나타내는 그립입니다.

![image](https://user-images.githubusercontent.com/90454621/231039848-17215a1b-1511-4b4e-bf46-fae91da8abd3.png)

GET, POST, PUT, DELETE 등의 메서드로 API를 요청했는데, 크롬 개발자 도구의 네트워크 탭에 OPTIONS 메서드로 요청이 보내지는 것을 보신 적 있으시다면 CORS를 경험하셨던 것입니다. Preflight 요청은 실제 리소스를 요청하기 전에 OPTIONS라는 메서드를 통해 실제 요청을 전송할지 판단합니다.

OPTIONS 메서드로 서버에 예비 요청을 먼저 보내고, 서버는 이 예비 요청에 대한 응답으로 Access-Control-Allow-Origin 헤더를 포함한 응답을 브라우저에 보냅니다. 브라우저는 단순 요청과 동일하게 Access-Control-Allow-Origin 헤더를 확인해서 CORS 동작을 수행할지 판단합니다.

<br/>

## CORS 에러 해결 방법
### CORS 대응 방법1 - Access-Control-Allow-Origin 설정
보통 CORS 이슈가 발생한다면 서버 측에서 Access-Control-Allow-Origin 헤더에 접근권한을 설정할 수 있습니다.
"*"를 설정하게 된다면 모든 외부 출처에서 접속을 할 수 있게 됩니다. 이 방법은 당장은 편리하여 좋아보이지만 보안적인 이슈에 직면할 수 있기 때문에 이러한 방법은 지양해야겠습니다.
그렇기에 외부에서 사용한다는 요청에 대한 심사를 거친 후 Access-Control-Allow-Origin에 외부 출처를 일일이 적용하는것이 좋습니다. 외부 출처를 추가하는 방법은 origin이 "https://test.com"일 경우 "Access-Control-Allow-Origin: https://testA.com'으로 헤더를 적용하여 주면 됩니다.

![image](https://user-images.githubusercontent.com/90454621/231041652-fdd27786-dad8-45db-8741-5fca8ca22f3f.png)

하지만 무려 서버측 헤더를 수정을 해야하기 때문에 서버측 헤더를 변경할 방법이 없다면 사용할 수 없는 방법입니다.

만약 서버를 수정할 수 있다는 가정하에 Express 서버를 예로 들어 보겠습니다. Express서버에서는 헤더를 직접 추가 하는 방법과 Middleware를 사용하여 Access-Contorl-Allow-Origin을 설정을 할 수 있었습니다.
```
var app = require('express')()
var cors = require('cors')

// Access-Control-Allow-Origin 적용방법1: 직접 헤더에 적용
app.all('/*', function (req, res, next) {
  res.header('Access-Control-Allow-Origin', '*')
  res.header('Access-Control-Allow-Headers', 'X-Requested-With')
  next()
})

// Access-Control-Allow-Origin 적용방법2: cors 미들웨어 사용
app.use(cors())

app.listen(80, function () {
  console.log('http server is listening on port 80')
})
```
cors()를 적용하게 된다면 모든 origin을 허용하게 됩니다. 일부의 origin을 적용하고 싶다면 cors 미들웨어 문서를 참고하시길 바랍니다.

<br/>

### CORS 대응 방법2 - JSONP 설정
다른 도메인에 접근할 수 있는 우회적인 기법 중에 JSONP(JSON with Padding) 방법이 있습니다. 웹 브라우저에서 실행되는 Javascript는 통신을 이용해 외부 출처에서 데이터를 받아오는 것이 불가능하지만, HTML script 요소는 외부 출처로 부터 조회된 내용을 실행하는 것이 허용되고 있습니다. 다만 Javascript 문법 오류가 발생하게 됩니다. 

문법 오류가 발생하는 이유는 Javascript에서 변수, 상수로 정의 되지 않고 json형식이 입력되면서 발생하게 됩니다.

JSONP는 이러한 웹브라우저 특성을 이용하여 json 데이터를 서버가 콜백함수로 감싸 javascript 문법을 유효하게 만들어 전달하여 클라이언트에서 응답을 받을 수 있게 됩니다.

"http://server.example.com/User/1234"요청을 예로 든다면

parseResponse 콜백함수를 JSONP 요청을하기위해 포함을 합니다.
```
<script type="application/javascript"
        src=http://server.example.com/Users/1234?callback=parseResponse">
</script>
```
외부의 서비스인 server.example.com은 JSON 데이터를 패딩하여 클라이언트에 전송합니다.
```
praseResponse({"Name": "Foo", "Id": 1234, "Rank": 7})
```
JSONP 내용을 확인해보시면 아시겠지만 결국 서버에서 패딩을 요청한 콜백함수로 감싸줘 전송을 해야한다는 문제가 발생합니다. 외부 API에서 콜백함수를 제공하지 않는다면 사용할 수 없는 방법이 되겠습니다. 위 JSONP내용은 JSONP문서를 참고 하여 설명해드렸습니다.

<br/>

### CORS 대응 방법3 - Proxy 설정
외부 도메인서버에 접근하고자할 때 바로 외부 도메인 서버를 통하는 것이 아닌 자신의 서버를 매개로 하여 외부서버에 요청하는 방식입니다.

![image](https://user-images.githubusercontent.com/90454621/231042276-6520bf07-0ff2-4b98-a5a8-12c157d72851.png)

서버에서 요청을 하게될 때에는 브라우저의 규약인 CORS 정책에 영향을 받지 않습니다.  그러한 이점을 이용하여 Proxy Server라는 출처를 통하기 때문에 CORS 정책을 위반하지 않게되어 우회 할 수 있게됩니다.

Express 서버일 경우 express-http-proxy 미들웨어를 통해서 간단하게 Proxy Server를 구현할 수 있습니다.
```
var proxy = require('express-http-proxy')
var app = require('express')()

app.use('/proxy', proxy('www.text.com'))
```

## 참고
https://beomy.github.io/tech/browser/cors

https://velog.io/@pwk921110/CORS%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80

https://escapefromcoding.tistory.com/724

https://devport.tistory.com/13

https://velog.io/@jimmy0417/WEB-CORS-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%A0%81%EC%9A%A9-%EB%B0%A9%EB%B2%95
