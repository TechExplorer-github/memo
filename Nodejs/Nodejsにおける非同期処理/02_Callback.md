# Callback

Callback は JavaScript の非同期制御で一番古くから利用されている

Node.js のファイルを扱う標準モジュールの fs の例

```js
const { readFile } = require("fs");

console.log("A");

readFile(__filename, (err, data) => {
  console.log("B", data);
});

console.log("C");
```

上記のコードを実行すると「A -> C -> B (+ファイルの内容)」の順で出力される

Callback は「処理が終わったときに呼び出される関数を登録する」インターフェース

readFile なら第二引数に Callback を与える

```js
readFile(ファイル, Callback);
```
