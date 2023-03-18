# Youtube-clone-coding-express.md

express
use express to use app

### Server

서버는 인터넷에 연결되어 있으며 24시간 꺼지지 않는 컴퓨터이다.

서버는 클라이언트(여기서는 브라우저)에서 보낸 request 를 받고 response 보낸다.

1.app.get(path, callback [, callback ...])

> 지정된 콜백 함수를 사용하여 HTTP GET 요청을 지정된 경로로 라우팅합니다.

1.1Request

> req 객체는 HTTP request를 나타내며 요청 query string, parameters, body, HTTP headers 등에 대한 속성을 가지고 있습니다.

1.2Response

> res 객체는 Express 앱이 HTTP request를 받을 때 보내는 HTTP response를 나타냅니다.

2.middleware

> 모든 controller는 middleware이다.
> app.get에서 (req,res 객체 뿐만 아닌 next 또한 사용한다.)-그러나 사용할 필요가 없기 때문에 사용하지 않았을 뿐.
> next()는 다음 함수를 호출하는 특징을 가지고 있다.

const one = (req,res,next) => {
next();
}
const two = (req,res,next) => {
next();
}
const three = (req,res) => {
console.log("Now three is handling")
}

// app.get will handle users who visit "/" URL with "one" handler
app.get("/", one, two, three)

2.1 controller

> 컨트롤러는 전달받은 request를 처리고 response를 전달하기 위한 콜백함수이다.

3.app.use = global middleware를 만들 수 있게 해주는 함수

What is global middleware?

> 어떠한 url을 들어가도 사용하게 되는 것.

middleware를 먼저 use 해준 후 url을 get 하는 순서를 지켜준다.

> express 또한 위에서 아래로 읽어내려가기 떄문이다.

4.Router

> express app에 자체 내장 되어 있다. 미들웨어 자체처럼 작동하므로
> app.use()에 대한 인수로 또는 다른 라우터의 use() 메서드에 대한 인수로 사용할 수 있다.
> 최상위 익스프레스 객체에는 새로운 라우터 객체를 생성하는 Router() 메서드가 있다.
> Router는 결국 url이 어떻게 시작하는지에 따라 나누는 방법으로 생각하면 된다.
> ex> /users/edit, /users/delete/etc... /videos/edit, /videos/delete/etc...

4.1 Router 사용법

> 1.const videoRouter=express.Router(); //Router 생성
> 2.app.use("/videos",videoRouter);
> 3.const WatchVideo=(req,res)=> res.send("Watch video!");
> 4.videoRouter.get("/watch",watchVideo);
> 5.result -- Wetube.com/videos/watch -- connect this url => Watch video!

5 How can user bring globalRouter?

> 1.export default aaa
> import aaa from "../controllers/userController" --> export default 를 사용하여 하나의 컨트롤러 함수를 사용할 수 있다.
> default 를 사용하여 export 할 경우에는 원하는 이름 어떤 것을 해도 문제가 되지 않는다.

> 2.export aaa
> import { aaa } from "../controllers/userController" --> export 를 사용하여 여러개의 Controller 함수를 사용 할 수 있다.{open Object}/필수는 아님
> export 할 경우에는 실제 이름을 사용해야 문제가 되지 않는다.

6.Parameter

> url 안에 변수를 포함 할 수 있게 한다.
> :parameter (변수 이름은 신경 쓰지 않아도 괜찮다.)
> Like this ->Wetube/videos/1,2,3,4,5..... ❌
> Wetube/videos/:parameter <- 변수가 비디오 번호로 대입 된다.✔
> 6.1Router 분리
> Routing
> https://expressjs.com/ko/guide/routing.html
> 정규식
> https://www.regexpal.com
> use two backslash mean On JS we have to escape the \

7.method-urlencoded()

> form이 body를 이해하기 위해 사용하는 메서드
> option 존재 https://expressjs.com/en/4x/api.html#express.urlencoded
> option:{extended:true} 보기좋게 정렬하는 용도 encoding
