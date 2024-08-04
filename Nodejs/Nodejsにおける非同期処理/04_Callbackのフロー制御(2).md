# Callback のフロー制御(2)

Callback をループで使いたい場合は、再帰処理等利用

処理が直列に動かない書き方

```js
const fs = require("fs");

for (let i = 0; i < 100; i++) {
  const text = `write: ${i}`;

  fs.writeFile("./data.txt", text, (err) => {
    if (err) {
      console.error(err);
      return;
    }
    console.log(text);
  });
}
```

上記のコードを実行数すると下記のようになる

```sh
write: 0
write: 2
write: 1
write: 4
write: 3
write: 6
write: 5
write: 7
write: 9
...
```

再帰処理を利用して直列に処理する場合

```js
const fs = require("fs");

const writeFile = (i) => {
  if (i >= 100) {
    return;
  }

  const text = `write: ${i}`;

  fs.writeFile("./data.txt", text, (err) => {
    if (err) {
      console.error(err);
      return;
    }

    console.log(text);
    writeFile(i + 1);
  });
};

writeFile(0);
```

上記のコードを実行すると 0 から 99 まで順番通り処理される
