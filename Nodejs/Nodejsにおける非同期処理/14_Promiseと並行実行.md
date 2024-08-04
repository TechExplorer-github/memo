# Promise と並行実行

Promise.all は引数に与えた Promise のリストを並行に実行した結果を Promise として返す関数
複数の非同期処理を同時に処理した結果を、1 つの await で待ち受けることができる

下記は undici を使って同時に 3 つのリクエストを送信するサンプルコード

```js
const { request } = require("undici");

const main = async () => {
  const resArray = await Promise.all([
    request("https://www.yahoo.co.jp/"),
    request("https://shopping.yahoo.co.jp/"),
    request("https://auctions.yahoo.co.jp/"),
  ]);

  for (const res of resArray) {
    const body = await res.body.text();
    const title = body.match(/<title>(.*)<\/title>/g);
    console.log(title);
  }

  return "done";
};

main()
  .then((data) => console.log(data))
  .catch((err) => console.error(err));
```
