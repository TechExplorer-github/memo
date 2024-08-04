# promisify と promise インターフェース

Callback の時に比べてコード量が増えるが、promisify を使うこと簡略化可能
promisify は標準モジュールの util に実装されている関数

util.promisify は下記の慣例に従った Callback 関数を Promise 化できる
※Node.js のモジュールの多くはこの慣例に従っている

- API の最後の引数が Callback
- Callback の第一引数がエラーオブジェクト
- 処理の完了時に一度だけ呼ばれる Callback 関数

```js
const { promisify } = require("util");
const { readFile, writeFile, chmod } = require("fs");

const readFileAsync = promisify(readFile);
const writeFileAsync = promisify(writeFile);
const chmodAsync = promisify(chmod);
```

現在の LTS バージョンの Node.js には fs のような標準モジュールには最初から Promise のインターフェースが実装されている

```js
const { readFile, writeFile, chmod } = require("fs/promises");

const backupFile = `${__filename}-${Date.now()}`;

readFile(__filename)
  .then((data) => {
    return writeFile(backupFile, data);
  })
  .then(() => {
    return chmod(backupFile, 0o400);
  })
  .catch((err) => {
    console.error(err);
  });
```
