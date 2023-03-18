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
