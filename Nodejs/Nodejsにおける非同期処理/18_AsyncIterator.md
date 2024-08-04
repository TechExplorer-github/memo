# AsyncIterator

AsyncIterator は複数回登場するイベント(data など)を for 文に似た文法で表現できるもの

```js
for await (変数 of 反復可能な対象) {
  // ...
}
```

AsyncIterator を使わない実装
並行に処理が実行されるので順次書き込みを行いたいときには向いていない

```js
const fs = require("fs");
const { writeFile } = require("fs/promises");

// 少し待つ非同期関数
const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const readStream = fs.createReadStream(__filename, {
  encoding: "utf8",
  highWaterMark: 64,
});
const writeFileName = `${__filename}-${Date.now()}`;

const write = async (chunk) => {
  // (Math.random() * 1000) ms待つ
  await sleep(Math.random() * 1000);

  // ファイルに追記モードで書き込む
  await writeFile(writeFileName, chunk, { flag: "a" });
};

let counter = 0;

readStream.on("data", async (chunk) => {
  console.log(counter);
  counter++;
  await write(chunk);
});

readStream.on("close", () => {
  console.log("close");
});
```

AsyncIterator を使った実装
AsyncIterator をうまく導入することで、ストリーム処理と async/await の相性の悪さを解消可能

```js
const fs = require("fs");
const { writeFile } = require("fs/promises");

// 少し待つ非同期関数
const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const writeFileName = `${__filename}-${Date.now()}`;

const write = async (chunk) => {
  // (Math.random() * 1000) ms待つ
  await sleep(Math.random() * 1000);

  // ファイルに追記モードで書き込む
  await writeFile(writeFileName, chunk, { flag: "a" });
};

const main = async () => {
  const stream = fs.createReadStream(__filename, {
    encoding: "utf8",
    highWaterMark: 64,
  });
  let counter = 0;

  // 非同期に発生するイベントを直列的に処理する
  for await (const chunk of stream) {
    console.log(counter);
    counter++;
    await write(chunk);
  }
};

main().catch((e) => console.error(e));
```
