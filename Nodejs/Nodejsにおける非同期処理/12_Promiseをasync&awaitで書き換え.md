# Promise を async/await で書き換え

main 関数を実行すると Promise が返ってくる
↓
async 関数の return で返した結果を then で受け取り、catch で包括的なエラーハンドリングが可能

```js
const { readFile, writeFile, chmod } = require("fs/promises");

const main = async () => {
  const backupFile = `${__filename}-${Date.now()}`;
  const data = await readFile(__filename);
  await writeFile(backupFile, data);
  await chmod(backupFile, 0o400);
  return "done";
};

main()
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    console.error(err);
  });
```
