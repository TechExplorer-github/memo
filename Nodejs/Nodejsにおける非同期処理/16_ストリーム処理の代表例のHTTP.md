# ストリーム処理の代表例の HTTP

server.js

```js
const http = require("http");

// http サーバーの生成
http
  .createServer((req, res) => {
    // クライアントに返す内容を書き込み
    res.write("hello world\n");

    // クライアントに内容を送信
    res.end();
  })
  .listen(3000);
```

↓ 書き換え

```js
const http = require("http");

// 独立してリスナーを定義できる
const server = http.createServer();

server.on("request", (req, res) => {
  res.write("hello world\n");
  res.end();
});

server.listen(3000);
```

client.js

```js
const http = require("http");

// サーバーに対してリクエストするオブジェクトを生成
const req = http.request("http://localhost:3000", (res) => {
  // 流れてくるデータをutf-8で解釈する
  res.setEncoding("utf8");

  // data イベントを受け取る
  res.on("data", (chunk) => {
    console.log(`body: ${chunk}`);
  });

  // end イベントを受け取る
  res.on("end", () => {
    console.log("end");
  });
});

// ここではじめてリクエストが送信される
req.end();
```

client.js の http.request の Callback の引数の res は HTTP リクエストのレスポンスを表すストリームオブジェクト
data と end というイベントが発生したことを受け取るリスナーを設定しています
