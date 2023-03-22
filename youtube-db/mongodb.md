# Youtube-clone-coding-db.md

1.mongodb

> Database :서버 연결
> 1.npm i mongoose
> 2.import mongoose >>mongoose.connect("url/serverName");
> 3.const db=mongoose.connection;

# what is CRUD?

> db 파트를 배우는 이유
> Create&Read&Update&Delete

# Schema

> 스키마는 MongoDB 컬렉션 모양의 정의 https://mongoosejs.com/docs/guide.html#schemas
> 스키마가 가질수 있는 type https://mongoosejs.com/docs/schematypes.html

# Models

> mongoose.model(modelName, schema):
> 모델은 스키마 정의에서 컴파일된 생성자이다.
> https://mongoosejs.com/docs/guide.html#models

# query

> Model.find() query 사용 방법 2가지 >Callback >Promise
> 새로운 mongoose에서 Callback은 더 이상 지원하지 않는듯 함..
> promise>await,async
> 차이점:Callback 먼저 실행되는 대로 , Promise : 순차적으로
> Model 앞에 await 작성시 find는 더이상 callback이 필요하지 않다고 판단함.
> error는 어떻게? : try catch 를 사용하여 알 수 있다. try 한 후 error가 있다면 catch 한다.
> await는 function 안에서만 사용할 수 있기 떄문에 사용 되는 것이 바로 async function 이다.

# create & new

> new just creates an instance of a class.
> create will actually put the data on the DB.
> new는 결국 만들고 save() 해주어야 함.

# regular expression

> 이전에 설정해주었던 정규식 id:(+d//)과 같은 형태를 사용할 떄 문제가 생긴다.
> why? mongodb에서 설정해준 id의 값이 숫자와 문자등이 합쳐진 형태기 떄문에, 그래서 정규식을 지워준다.
> 하지만 이때 upload 에도 문제가 생긴다. express는 위에서 아래로 읽어 내려가기 때문에 upload 또한 id와 같다고 판단하기 떄문.
> 해결법 : upload를 최상단으로 올린다.
> https://www.mongodb.com/docs/manual/reference/method/ObjectId/
> hexadecimal :0~9,6개의 기호로 이루어짐 [0-9a-f]{24}로 정규식 설정.

# find()

> 여전히 오류가 있다.
> why? 우리의 videoController watch()에서 id를 찾을 수 없기 때문에
> findById()/findOne()을 사용
> promise 를 return 받고 싶을 떄 exec() 를 사용

# error code

> 먼저 오류 검사를 하고 문제가 없을 시에 원하는 기능을 실행시킨다.
> 항상 return을 해줄 것. return 하지 않으면 javascript는 계속해서 코드를 실행시킬 것이다.

# mongoose middleware

> express 에서의 middleware 는 request 를 가로채 무엇인가를 진행 하는 것. morgan middleware.
> mongoose 또한 동일하게 적용 schema.pre('Name',async function())과 같은형태
> 주의 해야 할 점은 model이 생성되기 전에 선언해주어야한다는 것.
> https://mongoosejs.com/docs/middleware.html

# option.sort()

> SELECT문으로 검색된 데이터를 오름차순(ASC)이나 내림차순(DESC)으로 정렬 시킬 때 사용한다.
> const videos = await Video.find({}).sort({ createdAt: "desc" }); 체작 된 순서 내림차순 정렬

# 정규 표현식

> mongodb 자체 $regex 연산자> regex: new RegExp(keyword, "i")
> search 할 때 항상 정확한 video 명을 찾기 어렵기 떄문에 정규식 연산자를 사용. i 는 대소문자를 구별하지 않기 위해 사용한다.

# bcrypt

> User 계정 설정 시 패스워드가 그대로 DB에 저장 되는데 보안을 위해 password hashing 하였음. hash는 입력 값이 있으면 출력 값은 항상 고정 된 값으로 나오며 알아보기 힘든 불규칙적인 구성을 가지고 있다.

> pre 미들웨어 기능은 각 미들웨어가 다음을 호출할 때 차례로 실행됩니다. https://mongoosejs.com/docs/middleware.html#pre
> userSchema.pre("save", async function () {
> this.password = await bcryptjs.hash(this.password, 5);
> console.log("Hash Password:", this.password);
> });

# status code

> https://developer.mozilla.org/en-US/docs/Web/HTTP/Status 공문
> 100,200,300,400 logger를 통하여 볼 수 있다.
> login을 진행 할 때 DB에 맞지 않는 username이나 password를 입력하여도 브라우저에서 저장 하겠습니까? 라는 alert를 확인할 수 있는데, logger에서 200번에 해당하는 status code를 얻었기 떄문에 문제가 없다고 판단한 것.
> 따라서 return res.status(400).render 를 통해 잘못 입력하였을 때 400 Bad Request 를 받게 설정 400: 서버는 클라이언트 오류로 인식되는 것으로 인해 요청을 처리할 수 없거나 처리하지 않을 것입니다(예: 잘못된 형식의 요청 구문, 잘못된 요청 메시지 프레이밍 또는 사기성 요청 라우팅).
