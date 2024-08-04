# Callback の API の慣例

- API の最後の引数が Callback
- Callback の第一引数がエラーオブジェクト

第一引数がエラーオブジェクトとなるので、エラーハンドリングは必ず null チェックが必須！！！
※null チェックの if 文で return を書き忘れると後続処理が実行されるので要注意
※try-catch で Callback 内のエラーを補足できないの必ず Callback ごとにエラーの null チェックを行うこと！

```js
const { readFile } = require("fs");

readFile(__filename, (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
```
