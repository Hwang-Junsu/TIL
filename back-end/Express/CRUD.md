# Filde Modularization
- 폴더를 만들고 해당 파일에 api 메서드들을 분리해서 관리하는 것이 좋다.
- express의 Router를 import 하여 다른 파일에서 router를 생성할 수 있음.
- export default를 통해 내보내 준 후 app.ts에 적용 시켜줌.
```
app.use(catRouter);
```

# Express CRUD
```
import { Cat, CatType } from './cats.model';
import { Router } from 'express';

const router = Router();

//* READ 고양이 전체 데이터 다 조회
router.get('/cats', (req, res) => {
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
});
//* READ 특정 고양이 데이터 조회
router.get('/cats/:id', (req, res) => {
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
});

//* CREATE 새로운 고양이 추가 api
router.post('/cats', (req, res) => {
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
});

//* UPDATE 고양이 데이터 업데이트 -> PUT
router.put('/cats/:id', (req, res) => {
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
});
//* UPDATE 고양이 데이터 부분 업데이트 -> PATCH
router.patch('/cats/:id', (req, res) => {
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
});
//* DELETE 고양이 데이터 삭제 -> DELETE
router.delete('/cats/:id', (req, res) => {
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
});
export default router;
```

- DB 사용이전에 express의 전체적인 디자인패턴을 알아보기 위함.
- 메서드의 모든 경우가 성공하지는 않기 때문에 try, catch문을 사용해서 에러에 대비해야함.
- res.status(에러번호)를 통해 에러코드를 보내줄 수 있음.

// throw new Error("Error Message") 로 임의로 에러를 만들 수 있음.
