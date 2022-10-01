# Singleton Pattern
- 최초 한번 유연산자를 통해서 객체를 만들 수 있기 때문에 추후 접근을 할 때 메모리 낭비를 방지할 수 있음.
- 다른 클래스간의 데이터 공유가 쉬움.
```
import * as express from 'express';
import catRouter from './cats/cats.route';

class Server {
    public app: express.Application;

    constructor() {
        const app: express.Application = express();
        this.app = app;
    }

    private setRoute() {
        this.app.use(catRouter);
    }

    private setMiddleware() {
        //* logging middleware
        this.app.use((req, res, next) => {
            console.log(req.rawHeaders[5]);
            console.log('this is logging middleware');
            next();
        });
        //* json middleware
        this.app.use(express.json());
        this.setRoute();
        //* 404 middleware
        this.app.use((req, res, next) => {
            console.log('this is error middleware');
            res.send({ error: '404 not found error' });
        });
    }
    public listen() {
        this.setMiddleware();
        this.app.listen(8000, () => {
            console.log(`Example app listening at http://localhost:8000`);
        });
    }
}

function init() {
    const server = new Server();
    server.listen();
}

init();
```

# Service Pattern
- 유지보수를 위해 함수와 라우터 부분을 따로 적용한다.
```
// cats.route.ts
import { Router } from 'express';
import {
    readAllCat,
    readCat,
    createCat,
    updateCat,
    updatePartialCat,
    deleteCat,
} from './cats.service';

const router = Router();

//* READ 고양이 전체 데이터 다 조회
router.get('/cats', readAllCat);
//* READ 특정 고양이 데이터 조회
router.get('/cats/:id', readCat);
//* CREATE 새로운 고양이 추가 api
router.post('/cats', createCat);
//* UPDATE 고양이 데이터 업데이트 -> PUT
router.put('/cats/:id', updateCat);
//* UPDATE 고양이 데이터 부분 업데이트 -> PATCH
router.patch('/cats/:id', updatePartialCat);
//* DELETE 고양이 데이터 삭제 -> DELETE
router.delete('/cats/:id', deleteCat);

export default router;
```
```
// cats.service.ts
import { Request, Response } from 'express';
import { Cat, CatType } from './cats.model';

//* READ 고양이 전체 데이터 다 조회
export const readAllCat = (req: Request, res: Response) => {
    try {
        const cats = Cat;
        res.status(200).send({
            success: true,
            data: {
                cats,
            },
        });
    } catch (error: any) {
        res.status(400).send({
            success: false,
            error: error.message,
        });
    }
};
//* READ 특정 고양이 데이터 조회
export const readCat = (req: Request, res: Response) => {
    try {
        const params = req.params;
        console.log(params);
        const cat = Cat.find(cat => {
            return cat.id === params.id;
        });
        res.status(200).send({
            success: true,
            data: {
                cat,
            },
        });
    } catch (error: any) {
        res.status(400).send({
            success: false,
            error: error.message,
        });
    }
};
//* CREATE 새로운 고양이 추가 api
export const createCat = (req: Request, res: Response) => {
    try {
        const data = req.body;
        console.log(data);
        Cat.push(data);
        res.status(200).send({
            success: true,
            data: { data },
        });
    } catch (error: any) {
        res.status(400).send({
            success: false,
            error: error.message,
        });
    }
};
//* UPDATE 고양이 데이터 업데이트 -> PUT
export const updateCat = (req: Request, res: Response) => {
    try {
        const params = req.params;
        const body = req.body;
        let result;
        Cat.forEach(cat => {
            if (cat.id === params.id) {
                cat = body;
                result = cat;
            }
        });
        res.status(200).send({
            success: true,
            data: {
                cat: result,
            },
        });
    } catch (error: any) {
        res.status(400).send({
            success: false,
            error: error.message,
        });
    }
};
//* UPDATE 고양이 데이터 부분 업데이트 -> PATCH
export const updatePartialCat = (req: Request, res: Response) => {
    try {
        const params = req.params;
        const body = req.body;
        let result;
        Cat.forEach(cat => {
            if (cat.id === params.id) {
                cat = { ...cat, ...body };
                result = cat;
            }
        });
        res.status(200).send({
            success: true,
            data: {
                cat: result,
            },
        });
    } catch (error: any) {
        res.status(400).send({
            success: false,
            error: error.message,
        });
    }
};
//* DELETE 고양이 데이터 삭제 -> DELETE
export const deleteCat = (req: Request, res: Response) => {
    try {
        const params = req.params;
        const newCat = Cat.filter(cat => cat.id !== params.id);
        res.status(200).send({
            success: true,
            data: newCat,
        });
    } catch (error: any) {
        res.status(400).send({
            success: false,
            error: error.message,
        });
    }
};
```
- NestJS가 사용하는 방식이 위와 같기 때문에 간단한 express 개념을 정리하며 파일을 정리했음.
