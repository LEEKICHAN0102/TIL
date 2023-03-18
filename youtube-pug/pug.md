# Youtube-clone-coding-express.md

pug
Our project view engine

Pug는 html의 영향을 많이 받은, Node.js 및 브라우저용 JavaScript로 구현된 고성능 템플릿 엔진입니다.

Express와 함께 템플리트 엔진을 사용
Express가 템플리트를 렌더링하려면 다음과 같은 애플리케이션 설정이 필요합니다.

views, 템플리트가 있는 디렉토리.
예: app.set('views', './views')
view engine, 사용할 템플리트 엔진.
예: app.set('view engine', 'pug')
https://expressjs.com/ko/guide/using-template-engines.html

### how to return pug

> export const pugFile = (req,res) => res.render("viewName");
> (process.cwd() + "/src/views") /process.cwd()는 뒤의 내용을 추가하여 파일의 경로를 찾아주는 역할을 한다.

### pug의 장점?

pug의 장점은 반복할 필요가 없다는 것이다.
예를 들어 pug를 사용하여 최신화 된 년도를 return 받는다고 할 때
pug는 javascript를 사용할 수있기 떄문에 new.date().getFullYear()를 사용하여 년도를 return 받을 수 있다. 이것을 모든 템플릿에 똑같이 적용할 때 반복 할 필요 없이

> make partials folder & partial folder inside year.pug
> include partials/year.pug 와 같은 형시으로 사용 할 수 있는 것.

### what is Extending?

> extend를 사용하여 하나의 템플릿을 확장하여 사용할 수있다.
> (base.pug(원본))>>(home.pug(복사해서 사용할 템플릿--extends base.pug))
> 모든 것이 복사 되기 떄문에 쓸모가 없다 이를 위해 사용하는 것이 block이다.

### what is block?

> block like a window of template>>base.pug(block content)
> home.pug(block content->h1 home!) 이떄 block의 이름은 같아야 한다.
> 같은 템플릿을 복사하여 사용하지만 block을 사용하여 원하는 부분을 변경할 수 있다.
> 또한 script를 변경할 수도 있음. block script > script(src="/jquery.js")

### conditional

> https://pugjs.org/language/conditionals.html

### iteration

> https://pugjs.org/language/iteration.html

### Mixin

> 데이터를 받을 수 있는 똑똑한 partial(include)이라 볼 수 있다.
> partial은 그저 html일 뿐이지만 mixin은 mixin mixinName(argument)을 선언해 줘야한다. argument 가 없으면 오류 발생.
> 선언된 mixin을 받을 때 mixinName은 동일하여야 하지만 object는 어떤 이름을 하더라도 상관없다.
> mixins folder>>mixin video(info)...>>base.pug -> +video(anything)
> mixin을 사용할 때 include mixin을 선언 +mixinName을 하지 않으면 단순한 function이 된다.

### 제일앞에 /가있으면 절대경로 absolute & relative url difference

> a(href="/video/edit")--->localhost:4000/video/edit
> a(href="video/edit")--->localhost:4000/videos/video/edit
> a(href=백${video.id}/edit틱)--->localhost:4000/videos/1/edit
