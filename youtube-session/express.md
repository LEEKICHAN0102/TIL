# Youtube-clone-coding-session.md

# session

> express-session install / session이란 백엔드와 브라우저 간에 어떤 활동을 했었는지 기억하는 것을 뜻한다./세션은 기간이 지나면 만료 된다.// 노마드코더가 가끔 로그인이 자동적으로 끊기는 것도 이 떄문인듯

> session을 계속해서 보내주더라도 브라우저를 새로 시작하면 잊어버리기 때문에, DB를 이용해서 저장해주어야 한다.-> MongoStore
> session은 브라우저를 방문 하였을 때 생성되는데, 계속해서 세션이 생셩될시 많은 traffic을 불러올 수 있다. 그러므로
> session property / secret / reSave / saveUnInitialized / store
>
> > - reSave : 모든 request마다 세션의 변경사항이 있든 없든 세션을 다시 저장한다.
> >   true: 스토어에서 세션 만료일자를 업데이트 해주는 기능이 따로 없으면 true로 설정하여 매 request마다 세션을 업데이트 해주게 한다.
> >   false: 변경사항이 없음에도 세션을 저장하면 비효율적이므로 동작 효율을 높이기 위해 사용한다. 각각 다른 변경사항을 요구하는 두 가지 request를 동시에 처리할때 세션을 저장하는 과정에서 충돌이 발생할 수 있는데 이를 방지하기위해 사용한다.

> saveUninitialized : uninitialized 상태인 세션을 저장한다. 여기서 uninitialized 상태인 세션이란 request 때 생성된 이후로 아무런 작업이 가해지지않는 초기상태의 세션을 말한다.
> true: 클라이언트들이 서버에 방문한 총 횟수를 알고자 할때 사용한다.
> false: uninitialized 상태인 세션을 강제로 저장하면 내용도 없는 빈 세션이 스토리지에 계속 쌓일수 있다. 이를 방지, 저장공간을 아끼기 위해 사용한다.

# cookie

> session ID를 저장한다. backend 와 frontend 간의 정보를 교환.
> cookie와 session의 다른 점 : cookie는 그저 정보를 주고받는 방법중의 하나일 뿐. cookie의 장점은 automatically 주고받는 과정에서 유저가 해야할 것은 없다.
> session ID는 cookie 그리고 backend 에 저장 된다.

# sessionStore(MongoStore)

> session이 저장되는 곳. 서버가 재시작 될 때 마다 사라진다-> 테스트를 위한 저장소.//유효하지 않다.

> sessionStore에 session을 저장하게 될 경우 서버가 재시작 되어도 동일한 값의 session ID를 cookie에서 확인할 수 있다.

> MongoStore option : URL,

# locals

> locals는 사용자가 뭐든 할 수 있는 object (추가, 제거 , 접근(access))// import등 없이도 pug template에 접근할 수 있음.//middleWares.js
> 사용자가 웹 사이트를 처음 방문하면 서버는 새로운 세션 ID를 생성하고 브라우저에 보내는 응답에서 쿠키로 설정한다.
> 브라우저는 이 쿠키를 local에 저장하고 후속 요청이 있을 때마다 서버로 다시 보낸다.

# .env(환경변수)

> git에 올리기에 부적합한 내용을 환경변수 .env 파일안에 작성
> ex: 설정 값 key 값 ,url link 등 // 관습적으로 env 파일안에들어가는 것은 대문자로 작성할 것.
> 적용 명령어 : process.env.valName
> .env파일에 넣을 뿐 undefined상태이기 떄문에 dotenv를 install 해준 이후 server의 시작지점인 init.js에 dotenv를 추가해주어야 한다.

# github 계정 생성

> https://docs.github.com/en/developers/apps/building-oauth-apps/authorizing-oauth-apps 링크 참고
