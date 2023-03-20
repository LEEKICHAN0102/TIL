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
