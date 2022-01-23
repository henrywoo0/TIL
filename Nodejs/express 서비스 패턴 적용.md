cats.route.ts
```ts
import { Cat, CatType } from "./cats.model";
import { Router } from "express";
import {
  createCat,
  deleteCat,
  readAllCat,
  readCat,
  updateCat,
  updatePartialCat,
} from "./cats.service";

const router = Router();

// READ 고양이 전체 데이터 조회
router.get("/cats", readAllCat);

// READ 특정 고양이 데이터 조회 (동적 라우팅)
router.get("/cats/:id", readCat);

// CREATE 새로운 고양이 추가 api
router.post("/cats", createCat);

// UPDATE 고양이 데이터 업데이트 -> PUT
router.put("/cats/:id", updateCat);

// UPDATE 고양이 데이터 부분적으로 업데이트 -> PATCH
router.patch("/cats/:id", updatePartialCat);

// DELETE 고양이 데이터 삭제 -> DELETE
router.delete("/cats/:id", deleteCat);

export default router;
```

cats.service.ts
```ts
import { Cat, CatType } from "./cats.model";
import { Request, Response } from "express";

export const readAllCat = (req: Request, res: Response) => {
  try {
    const cats = Cat;
    // throw new Error("db connect error");
    res.send({
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

// READ 특정 고양이 데이터 조회 (동적 라우팅)
export const readCat = (req: Request, res: Response) => {
  try {
    const id = req.params.id;
    const cat = Cat.find((cat) => {
      return cat.id === id;
    });
    // throw new Error("db connect error");
    res.send({
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

// CREATE 새로운 고양이 추가 api
export const createCat = (req: Request, res: Response) => {
  try {
    const data = req.body;
    Cat.push(data); // create
    res.send({
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

// UPDATE 고양이 데이터 업데이트 -> PUT
export const updateCat = (req: Request, res: Response) => {
  try {
    const id = req.params.id;
    const body = req.body;
    let result;
    Cat.forEach((cat) => {
      if (cat.id === id) {
        cat = body;
        result = cat;
      }
    });
    res.send({
      success: true,
      data: {
        result,
      },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

// UPDATE 고양이 데이터 부분적으로 업데이트 -> PATCH
export const updatePartialCat = (req: Request, res: Response) => {
  try {
    const id = req.params.id;
    const body = req.body;
    let result;
    Cat.forEach((cat) => {
      if (cat.id === id) {
        cat = { ...cat, ...body };
        result = cat;
      }
    });
    res.send({
      success: true,
      data: {
        result,
      },
    });
  } catch (error: any) {
    res.status(400).send({
      success: false,
      error: error.message,
    });
  }
};

// DELETE 고양이 데이터 삭제 -> DELETE
export const deleteCat = (req: Request, res: Response) => {
  try {
    const id = req.params.id;
    const newCat = Cat.filter((cat) => {
      cat.id !== id;
    });
    res.send({
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
