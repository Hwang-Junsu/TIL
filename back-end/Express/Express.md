# Express 공식문서
- https://expressjs.com/

# 기본 Setup
```
// app.ts
import * as express from "express";
const app: express.Express = express();
const port: number = 8000;

app.get("/test", (req: express.Request, res: express.Response) => {
    console.log(req);
    res.send({name: "junsu", age: 28, friends: ["ss", "ys"]});
});

app.listen(port, () => {
    console.log(`Example app listening at http://localhost:${port}`);
});

```

- app 뒤에 get이나 post을 통해 해당 url의 req를 받아 send 함수로 res를 반환한다.
- listen은 포트를 열어 서버를 실행하는 함수.

# Middleware
- https://expressjs.com/en/guide/writing-middleware.html
- Client의 요청에서 Router로 진행하기 전에 거치는 중간단계 함수
```
app.use((req, res, next) => {
    console.log(req.rawHeaders[5]);
    console.log('this is logging middleware');
    next();
});

app.get('cats/som', (req, res, next) => {
    console.log('this is som middleware');
    next();
});
```
- use를 사용해서 해당 구문 아래로 전역으로 사용이 가능하다.
- req, res 뒤에 next함수 인자를 받아서 사용할 수 있음.
- 특정 라우터에 대한 미들웨어를 작성하고 싶을 경우에는 get함수를 사용한뒤 인자에 next를 추가해 준다.
