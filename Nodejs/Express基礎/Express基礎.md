# Express 基礎

## Express の基礎と導入

Express の導入

```sh
mkdir test_server
cd test_server
npm init -y
npm install express
```

Express のサンプルコード

```js
const express = require("express");
const app = express();

// GET '/' （トップ）アクセス時の挙動
app.get("/", (req, res) => {
  res.status(200).send("hello world\n");
});

// GET '/user/:id' に一致するGETの挙動
app.get("/user/:id", (req, res) => {
  res.status(200).send(req.params.id);
});

// ポート: 3000 でサーバーを起動
app.listen(3000, () => {
  // サーバー起動後に呼び出されるCallback
  console.log("start listening");
});
```

実行方法

```sh
node server.js
```

## Express の必須機能

Express の基本機能は 2 つ

- ルーティング
- ミドルウェア

上記に加えて包括的なエラーハンドリングも押さえれておけば OK！

最小の Web サーバーのサンプルコード

```js
const express = require("express");
const app = express();

// ルーティング
app.get("/", (req, res) => {
  res.status(200).send("hello world\n");
});

// 包括的エラーハンドリング
app.use((err, req, res, next) => {
  res.status(500).send("Internal Server Error");
});

app.listen(3000, () => {
  console.log("start listening");
});
```

## ミドルウェア

Express のミドルウェアとは、リクエスト・レスポンス時にリクエストオブジェクト(req)とレスポンスオブジェクト(res)にアクセス(取得・操作)できる関数のこと

```js
(req, res) => {
  // リクエストヘッダー "foo" に渡された値をステータスコード200でクライアントに返す
  res.status(200).send(req.headers["foo"]);
};
```

ミドルウェアは連鎖的に呼び出し可能

```js
// /foo にアクセスがあると middlewareA -> middlewareB -> middlewareC と順番に呼び出される
app.get("/foo", middlewareA, middlewareB, middlewareC);
```

次のミドルウェアを呼び出す場合は第三引数に渡される next()を用いる

```js
(req, res, next) => {
  // APIのトークンがヘッダーになかったらステータスコード403を返す
  if (!req.headers["api-token"]) {
    return res.status(403).send("Forbidden");
  }

  // next（次のミドルウェア）を呼び出す
  next();
};
```

特殊なミドルウェアとして包括的なエラーハンドリングがある
下記のパターン引数は包括的エラーハンドリング以外ではない

- 第一引数: エラー内容
- 第二引数: リクエスト
- 第三引数: レスポンス
- 第四引数: next

```js
(err, req, res, next) => {
  // エラーが発生した場合の処理
  // req: リクエストオブジェクト
  // res: レスポンスオブジェクト
  // next: 次のミドルウェアを呼び出すための関数

  // ここでエラーに対する処理を行います

  // 例えば、エラーレスポンスをクライアントに送信するなど
  res.status(500).send("Internal Server Error");
};
```
