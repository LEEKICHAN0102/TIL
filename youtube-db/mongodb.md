#Youtube-clone-coding-db.md

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
