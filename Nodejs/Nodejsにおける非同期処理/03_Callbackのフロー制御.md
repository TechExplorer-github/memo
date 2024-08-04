# Callback のフロー制御

Callback では処理を直列にするためには Callback の中で Callback を呼び必要がある

(例)

1. ファイル自身を読み込み
2. ファイル名をフォーマットして別名で書き込み
3. バックアップしたファイルを ReadOnly にする

```js
const { readFile, writeFile, chmod } = require("fs");

const backupFile = `${__filename}-${Date.now()}`;

readFile(__filename, (err, data) => {
  if (err) {
    return console.error(err);
  }

  writeFile(backupFile, data, (err) => {
    if (err) {
      return console.error(err);
    }

    chmod(backupFile, 0o400, (err) => {
      if (err) {
        return console.error(err);
      }

      console.log("done");
    });
  });
});
```

Callback のデメリットは readFile → writeFile → chmod とどんどんネスト深くなること
Callback Hell とも呼ぶ
